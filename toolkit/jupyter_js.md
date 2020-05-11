# 使用JupyterLab编写javascript代码


* [问题的描述]
    jupyter notebook的代码是在后台的kernel中运行的，这是设计初衷。
    而D3.js的实验代码，特别是在开发可视化的过程中，需要该代码是前端浏览器中运行，并且具有交互特性，这与jupyter的设计目标有差别

* [解决方法]
    写一个前端的kernel，执行单元格中的js代码，并应把结果应用到下一个画布上，当前这些单元格中的代码要位于同一个上下文中，目前没有现成的

# 调研过程    

* [运行node.js kernel](https://www.jianshu.com/p/653c66f0df7c),
据说只能运行一次，因为JS严格模式不能第二次运行相同代码，只能重启内核

* [手写HTML直接写界面](https://mlln.cn/2020/03/26/%E5%A6%82%E4%BD%95%E5%9C%A8jupyter-notebook%E4%B8%AD%E8%BF%90%E8%A1%8Cjavascript%E5%92%8CHTML%E4%BB%A3%E7%A0%81/)
```
%lsmagic
```
内有
```
Available line magics:
    
%alias  %alias_magic  %autoawait  %autocall  %automagic  %autosave  %bookmark  %cd  %clear  %cls  %colors  %config  %connect_info  %copy  %ddir  %debug  %dhist  %dirs  %doctest_mode  %echo  %ed  %edit  %env  %gui  %hist  %history  %killbgscripts  %ldir  %less  %load  %load_ext  %loadpy  %logoff  %logon  %logstart  %logstate  %logstop  %ls  %lsmagic  %macro  %magic  %matplotlib  %mkdir  %more  %notebook  %page  %pastebin  %pdb  %pdef  %pdoc  %pfile  %pinfo  %pinfo2  %popd  %pprint  %precision  %prun  %psearch  %psource  %pushd  %pwd  %pycat  %pylab  %qtconsole  %quickref  %recall  %rehashx  %reload_ext  %ren  %rep  %rerun  %reset  %reset_selective  %rmdir  %run  %save  %sc  %set_env  %store  %sx  %system  %tb  %time  %timeit  %unalias  %unload_ext  %who  %who_ls  %whos  %xdel  %xmode
    
Available cell magics:
    
%%!  %%HTML  %%SVG  %%bash  %%capture  %%cmd  %%debug  %%file  %%html  %%javascript  %%js  %%latex  %%markdown  %%perl  %%prun  %%pypy  %%python  %%python2  %%python3  %%ruby  %%script  %%sh  %%svg  %%sx  %%system  %%time  %%timeit  %%writefile
    
```

* [在此基础上做进一步的封装，做为插件实现了一个新的magic](https://github.com/ResidentMario/py_d3)
D3 block magic for Jupyter notebook.
How it works? Jupyter notebooks allow executing arbitrary JavaScript code using IPython.display.JavaScript, however it makes no effort to restrict the level of DOM objects accessible to executable code. py_d3 works by restricting d3 scope to whatever cell you are running the code in, by monkey-patching the d3.select and d3.selectAll methods (see here for why this works).

* [另一种思路，在%%HTML单元中直接访问结果节点的element](https://www.stefaanlippens.net/jupyter-custom-d3-visualization.html), [同样的思路](https://blog.thedataincubator.com/2015/08/embedding-d3-in-an-ipython-notebook/)

IPython’s %%javascript magic runs code client-side and sets a global JQuery-selected variable, element, to refer to the output cell. This is obviously very convenient – we now have a way to create arbitrary DOM elements in our cell. In particular, we can create SVG canvases and add SVG shapes to that canvas… see where this is going?

```
%%javascript
element.append("<div id='chart1'></div>");
```

```js
%%javascript
(function(element) {
    require(['d3'], function(d3) {   
        var data = [1, 2, 4, 8, 16, 8, 4, 2, 1]

        var svg = d3.select(element.get(0)).append('svg')
            .attr('width', 400)
            .attr('height', 200);
        svg.selectAll('circle')
            .data(data)
            .enter()
            .append('circle')
            .attr("cx", function(d, i) {return 40 * (i + 1);})
            .attr("cy", function(d, i) {return 100 + 30 * (i % 3 - 1);})
            .style("fill", "#1570a4")
            .transition().duration(2000)
            .attr("r", function(d) {return 2*d;})
        ;
    })
})(element);
```

* [另一种实现](https://github.com/mpld3/mpld3)
[D3 Renderings of Matplotlib Graphics](https://blog.thedataincubator.com/2015/08/embedding-d3-in-an-ipython-notebook/). 这就不可能在单元格中写d3代码了