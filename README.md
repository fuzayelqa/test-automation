# Test-Automation (Test FB Login) 
# Author- Ozih Uddin Al Fuzayel

import pytest
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time

# Replace with your actual Facebook credentials.
EMAIL = "fuzayelbd5566@gmail.com"
PASSWORD = "My_password"

@pytest.fixture
def driver():
    # Initialize Chrome WebDriver
    options = webdriver.ChromeOptions()
    options.add_argument("--start-maximized")
    driver = webdriver.Chrome(options=options)
    yield driver
    driver.quit()

def test_facebook_login(driver):
    driver.get("https://www.facebook.com/")

    # Find and fill email field
    email_input = driver.find_element(By.ID, "email")
    email_input.send_keys(EMAIL)

    # Find and fill password field
    password_input = driver.find_element(By.ID, "pass")
    password_input.send_keys(PASSWORD)

    # Submit the form
    password_input.send_keys(Keys.RETURN)

    # Wait for a few seconds
    time.sleep(5)

    # Check if the login was successful
    assert "login" not in driver.current_url.lower(), "Login failed - still on login page"
