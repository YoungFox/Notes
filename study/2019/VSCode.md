#断点调试

package.json

```
"dev-debug": "NODE_ENV=development node --inspect server/index.js --watch"
```

点击左侧Debug->上方DEBUG下拉菜单->Add Configuration

launch.json
```
{
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "name": "Attach to Nuxt",
      "port": 9229
    }
  ]
}

```

终端启动程序

```
npm run dev-debug
```

启动成功后，在VSCode中点击DEBUG旁边的绿色箭头，成功后终端会有提示，VSCode的DEBUG CONSOLE为可用状态，之后就可以在代码区左侧打断点调试nodejs了