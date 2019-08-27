 ":CFBundleIdentifier", Does Not Exist !!
 报这个错误，升级系统、xcode等。
 
 
 Cannot find entry file index.ios.js in any of the roots
 
```
lsof -n -i4TCP:8081

kill -9 <PID>
```

##AsyncStorage的使用

类似localStorage
```
AsyncStorage.setItem(storageId, JSON.stringify(tasks), () => {
        this.setState({tasks: tasks},()=>{
          resolve();
        });
      });
      
 AsyncStorage.getItem(storageId,(err ,res)=>{
      if(!err){
        this.setState({tasks:JSON.parse(res)});
      }
    });
```




##使用await
To use, simply npm install babel-preset-react-native-stage-0 --save and put
```
{ presets: ['react-native-stage-0'] }
```
in your .babelrc.

```
watchman watch-del-all
node_modules/react-native/packager/packager.sh --reset-cache
```

清除包依赖缓存
```
node_modules/react-native/packager/packager.sh --reset-cache
```



Navigator

