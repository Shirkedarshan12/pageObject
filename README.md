from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
import time
import unittest
from sampleProjects.POMProjectDemo.Pages.loginPage import LoginPage  #(class)
from sampleProjects.POMProjectDemo.Pages.homePage import HomePage



class LoginTEst(unittest.TestCase):

    @classmethod
    def setUpClass(cls):
        options = webdriver.ChromeOptions()
        options.add_experimental_option("detach", True)
        serv_obj = Service("C:\Drivers\chromedriver_win32\chromedriver.exe")
        cls.driver = webdriver.Chrome(options=options, service=serv_obj)
        cls.driver.implicitly_wait(10)
        cls.driver.maximize_window()

    def test_login_valid(self):
        driver = self.driver
        driver.get("https://opensource-demo.orangehrmlive.com/web/index.php/auth/login")

        login= LoginPage(driver)
        login.enter_username("Admin")
        login.enter_password("admin123")
        login.click_login()

        homepage=HomePage(driver)
        homepage.click_welcome()
        homepage.click_logout()
        time.sleep(2)


        @classmethod
        def tearDownClass(cls):
            cls.driver.close()
            print("Test completed")





