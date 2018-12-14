用来检测是否支持一些功能?
用来解决兼容性问题?
```
support = $.support;
            for(key in support) {
              document.write('support.' + key + '=' + support[key] + '<br/>');
            }
```
![image.png](https://upload-images.jianshu.io/upload_images/13637909-f15d0ff7c5367550.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
support.checkOn=true 兼容性问题?
support.optSelected=true 下拉菜单? 检测默认值是否选中? 检查第一个option?
support.reliableMarginRight=true 检查marginRight计算是否可靠? 
support.boxSizingReliable=true
support.pixelPosition=false
support.noCloneChecked=true
support.optDisabled=true
support.radioValue=true
support.checkClone=true
support.focusinBubbles=false
support.clearCloneStyle=true
support.cors=true
support.ajax=true
```