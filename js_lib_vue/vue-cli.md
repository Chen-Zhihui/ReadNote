# overview

@vue/cli， package name
    vue-cli, deprecated, old package name
    vue command 
    vue create
    vue serve
    vue ui

cli service, @vue/cli-service
    development dependency
    built on top of webpack, webpack-dev-server
    vue-cli-service serve|build|inspect

cli plugins
    optional features
    babel/TypeScript transpilation
    eslint
    unit
    end to end testing
    @vue/cli-plugin-*

## reference

[doc](https://cli.vuejs.org/guide/prototyping.html)
    
# install

```bash
npm install -g @vue/cli
#or
yarn global add @vue/cli

#version
vue --version

#update
cnp update -g @vue/cli
#or
yarn global upgrade --latest @vue/cli

#update package tools
vue upgrade
```

# Basic

## Instance Prototyping

安装一些全局包

```bash
npm install -g @vue/cli @vue/cli-service-global
# or
yarn global add @vue/cli @vue/cli-service-global
```

the entry can be one of main.js, index.js, App.vue or app.vue

```bash
vue serve MyComponent.vue
```

## create

```
vue create
```