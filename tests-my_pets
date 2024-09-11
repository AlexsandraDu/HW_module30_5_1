import pytest
from selenium import webdriver
from selenium.webdriver.common.by import By

from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

from selenium.webdriver.firefox.service import Service
from webdriver_manager.firefox import GeckoDriverManager


@pytest.fixture()
def driver():
    driver_service = Service(GeckoDriverManager().install())
    driver = webdriver.Firefox(service=driver_service)
    driver.get('https://petfriends.skillfactory.ru/login')
    driver.maximize_window()
    yield driver
    driver.quit()



def test_my_pets_explicit(driver):
    ### Выполняем проверку явного ожидания ###
    WebDriverWait(driver, 5).until(EC.presence_of_element_located((By.ID, 'email')))
    ### Вводим логин ###
    driver.find_element(By.ID, 'email').send_keys('tests@mail.ru')
    ### Вводим пароль ###
    driver.find_element(By.ID, 'pass').send_keys('159753')
    ### Нажимаем кнопку ввода ###
    driver.find_element(By.CSS_SELECTOR, 'button[type="submit"]').click()
    ### Выполняем проверку, нахождения на главной странице пользователя ###
    assert driver.find_element(By.TAG_NAME, 'h1').text == 'PetFriends'


def test_my_pets_implicit(driver):
    ### Выполняем проверку неявного ожидания ###
    driver.find_element(By.ID, 'email').send_keys('tests@mail.ru')
    driver.find_element(By.ID, 'pass').send_keys('159753')
    driver.implicitly_wait(10)
    driver.find_element(By.CSS_SELECTOR, 'button[type="submit"]').click()
    assert driver.find_element(By.TAG_NAME, 'h1').text == 'PetFriends'
