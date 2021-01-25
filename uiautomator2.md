## 安装
adb -s [sn] install ui2/app-uiautomator.apk
adb -s [sn] install ui2/app-uiautomator-test.apk
adb -s [sn] push ui2/minicap data/local/tmp/
adb -s [sn] push ui2/minitouch data/local/tmp/
adb -s [sn] push ui2/atx-agent data/local/tmp/
adb -s [sn] chmod 777 data/local/tmp/atx-agent
adb -s [sn] "nohup /data/local/tmp/atx-agent server -d &"

## 常用接口
```python
import uiautomator2 as ui2
# 连接设备
u = ui2.connect_adb_wifi([ip:5555])
u = ui2.connect_usb(sn)
# home back
u.press('back')
u.press('home')
# 查找元素
el = u(resourceId=resourceId)
el = u(text=text)
succ = el.exists()
el.wait_gone(20)    # 等待消失

el = u.xpath('//*[@resource-id="id1"]/android.widget.LinearLayout[1])
succ = el.exists
succ = el.click_exists(timeout=1)
el_arr = u.xpath('//android.widget.LinerLayout').all()
infos = el.info

editor.cliear_text()
editor.send_keys('abc')

# 点击
el.click()
succ = el.click_exists(timeout=4) # 成功返回True

# 截图
u.screenshot(img_path)
img = cv2.imread(img_path)

# 启动，关闭 app
u.app_start(appname, activity=activity, stop=True)
u.app_stop(appname)
# 检查app是否存在
applist = 'adb -s [sn] shell pm list packages'
if appname in applist:
    return True
```

## 卸载
adb -s [sn] shell /data/local/tmp/atx-agent server -stop
adb -s [sn] remount
adb -s [sn] rm /data/local/tmp/minicap
adb -s [sn] rm /data/local/tmp/minitouch
adb -s [sn] rm /data/local/tmp/atx-agent
adb -s [sn] uninstall com.github.uiautomator.test
adb -s [sn] uninstall com.github.uiautomator
