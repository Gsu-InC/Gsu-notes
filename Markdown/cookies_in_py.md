```
class CookieManager:
    def __init__(self, driver):
        self.driver = driver
    
    def save_cookies(self, filename):
        """保存当前所有cookies到文件"""
        cookies = self.driver.get_cookies()
        with open(filename, 'w') as f:
            json.dump(cookies, f, indent=2)
        print(f"Cookies saved to {filename}")
    
    def load_cookies(self, url, filename):
        """从文件加载cookies"""
        # 先访问目标网站
        self.driver.get(url)
        
        # 删除现有cookies
        self.driver.delete_all_cookies()
        
        # 加载cookies
        with open(filename, 'r') as f:
            cookies = json.load(f)
        
        for cookie in cookies:
            # 处理可能的类型问题
            if 'sameSite' in cookie and cookie['sameSite'] == 'None':
                cookie['sameSite'] = 'Strict'
            self.driver.add_cookie(cookie)
        
        # 刷新页面
        self.driver.refresh()
        print("Cookies loaded successfully")
    
    def is_logged_in(self, check_element):
        """检查是否已登录"""
        try:
            self.driver.find_element(*check_element)
            return True
        except:
            return False

# 使用示例
driver = webdriver.Chrome()
cookie_manager = CookieManager(driver)

# 加载cookie保持登录
cookie_manager.load_cookies(
    "https://www.example.com",
    "cookies.json"
)

```