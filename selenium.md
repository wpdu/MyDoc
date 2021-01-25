```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.action_chains import ActionChains


# 创建driver
driver = webdriver.Chrome()
# 创建driver 修改下载地址，一个链接下载多个文件时不提醒
options = webdriver.ChromeOptions()
prefs = {'profile.default_content_settings.popups': 0,
         'download.default_directory': download_path,
         'profile.default_content_setting_values.automatic_downloads': 1}
options.add_experimental_option('prefs', prefs)
driver = webdriver.Chrome(chrome_options=options)

# 最大化, 刷新，关闭
driver.maximize_window()
driver.get(url)
driver.refresh()
driver.close()

# 滚动到目标控件
actions = ActionChains(driver)
actions.move_to_element(element).perform()
# 用js滚动
driver.execute_script('arguments[0].scrollIntoView();', el)

# 粘贴
actions = ActionChains(driver)
actions.move_to_element(input_el)
actions.click(input_el)
actions.key_down(Keys.CONTROL)
actions.send_keys('v')
actions.key_up(Keys.CONTROL)
actions.perform()

# 偏差点击
actions = ActionChains(driver)
actions.move_to_element_with_offset(element, off_x, off_y)
action.click()
action.perform()

# 处理弹窗
driver.switch_to.alert.accept()

# 切换窗口
driver.switch_to_window(driver.window_handles[0])

# 切换到Frame
driver.switch_to.frame('frame1')

# 等待
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By

wait = WebDriverWait(driver, 10)
wait.until_not(EC.presence_of_element_located((By.CLASS_NAME, 'c1')))
wait.until(EC.presence_of_element_located((By.CLASS_NAME, 'c1')))

# 元素查找
driver.find_element_by_class_name('c1')
# 按标签查找
driver.find_element_by_tag_name('li')
# 根据 xpath 查找
driver.find_elements_by_xpath('.//ul[@class="c1"]/li[@id="id1"]')
# 根据 xpath 字符查找 元素
driver.find_element_by_xpath('./div/span[contains(text(), "查找这个字符")])

# 选择框
from selenium.webdriver.support.ui import Select
selector = Select(select_element)
selector.select_by_visible_text('item1')

# 输入框
el.clear()
el.send_keys('inputstr')

# 执行 js
driver.execute_script('''downloadBack()''')
# 写入html
driver.execute_script('arguments[0].insertHTML=argument[1]', el, 'html')
```