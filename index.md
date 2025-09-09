---
layout: default
---

# QA ENGINEER | QUALITY ASSURANCE ANALYST

I’m a QA Engineer with a background in screenwriting, translation, and content development, which has given me a sharp eye for detail and clarity. I don’t just look for bugs—I put myself in the end user’s shoes, making apps intuitive, clear, and enjoyable to use.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-6A8EDD?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/victoriabozo/)

## Technical Skills
Testing: Functional, Regression, Smoke, Non-functional | REST | JSON | SQL | Agile/Scrum | DevTools | Technical Writing

![Postman](https://img.shields.io/badge/Postman-3F587A?style=for-the-badge&logo=postman&logoColor=white)
![Jira](https://img.shields.io/badge/jira-4A6FA5?style=for-the-badge&logo=jira&logoColor=white)
![Python](https://img.shields.io/badge/python-597CBF?style=for-the-badge&logo=python&logoColor=white)
![Pytest](https://img.shields.io/badge/pytest-6A8EDD?style=for-the-badge&logo=pytest&logoColor=white)
![Selenium](https://img.shields.io/badge/selenium-7B9FEB?style=for-the-badge&logo=selenium&logoColor=white)
![PyCharm](https://img.shields.io/badge/pycharm-8CAFFF?style=for-the-badge&logo=pycharm&logoColor=white)
![Android Studio](https://img.shields.io/badge/android%20studio-7B9FEB?style=for-the-badge&logo=android%20studio&logoColor=white)
![GitHub](https://img.shields.io/badge/github-6A8EDD?style=for-the-badge&logo=github&logoColor=white)
![Windows Terminal](https://img.shields.io/badge/Windows%20Terminal-597CBF?style=for-the-badge&logo=windows-terminal&logoColor=white)
![Canva](https://img.shields.io/badge/Canva-4A6FA5?style=for-the-badge&logo=Canva&logoColor=white)
![Asana](https://img.shields.io/badge/asana-3F587A?style=for-the-badge&logo=asana&logoColor=white)
![Trello](https://img.shields.io/badge/Trello-3F587A?style=for-the-badge&logo=Trello&logoColor=white)

## Projects
### Automated Taxi Booking – Urban Routes
[View Full Project on GitHub](https://github.com/victoriabozo/qa-project-Urban-Routes-es)

**Overview:**
Automated the end-to-end taxi booking workflow in the Urban Routes app, simulating real user interactions from route selection to order confirmation. Ensured that the application behaves correctly according to functional requirements.

**Tools & Methods:**
- Python & Selenium WebDriver for UI automation.
- pytest for test structuring and execution.
- Page Object Model (POM) for maintainable and scalable test code.
- Selectors & Synchronization: XPATH, CSS Selectors, IDs, Class Names, WebDriverWait, and Expected Conditions.
- Assertions for validating inputs, visual elements, and component states.

**Workflow Tested:**
- Configuring origin and destination.
- Selecting Comfort fare.
- Entering and confirming phone number.
- Adding payment details and messages for driver.
- Ordering extras (blanket, tissues, ice creams).
- Confirming order status modal.

**Outcome:**
Streamlined regression testing for Urban Routes, reducing manual effort and improving confidence in the app’s booking workflow.

**Code Sample:**
```python 
from data import data
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from pages import urban_routes_page as urp
from utils import retrieve_code

class TestUrbanRoutes:

    driver = None

    @classmethod
    def setup_class(cls):
        chrome_options = webdriver.ChromeOptions()
        chrome_options.set_capability("goog:loggingPrefs", {'performance': 'ALL'})
        cls.driver = webdriver.Chrome(service=Service(), options=chrome_options)
        cls.driver.get(data.urban_routes_url)
        cls.routes_page = urp.UrbanRoutesPage(cls.driver)

# 1. Configurar la dirección:
    def test_set_route(self):
        address_from = data.address_from
        address_to = data.address_to
        self.routes_page.set_route(address_from, address_to)
        assert self.routes_page.get_from() == address_from
        assert self.routes_page.get_to() == address_to

# 2. Seleccionar la tarifa Comfort:
    def test_select_comfort_rate(self):
        self.routes_page.click_request_taxi_button()
        self.routes_page.click_comfort_rate_icon()
        assert self.routes_page.is_comfort_rate_selected()

# 3. Rellenar el número de teléfono:
    def test_set_phone_number(self):
        phone = data.phone_number
        self.routes_page.click_phone_number_button()
        self.routes_page.set_phone_number(phone)
        self.routes_page.click_phone_form_next_button()
        code = retrieve_code.retrieve_phone_code(self.driver)
        self.routes_page.set_confirmation_code(code)
        self.routes_page.click_confirm_code_button()
        assert self.routes_page.get_phone_number() == phone

# ...rest of the tests...

    @classmethod
    def teardown_class(cls):
        cls.driver.quit()
  ```

### Automated API Testing – Urban Grocers
[View Full Project on GitHub](https://github.com/victoriabozo/qa-project-Urban-Grocers-app-es)

**Overview:**
Automated validation of the name field in product kits for the Urban Grocers app. Ensured that product names meet length and formatting criteria, catching invalid inputs before they reach production.

**Tools & Methods:**
- Python & pytest for test automation.
- Requests library for HTTP API testing.
- Positive and negative tests on field name.
- Status code assertions (201, 400) and JSON content validation.
- Test cases included minimum/maximum length, special characters, spaces, numbers, and missing/invalid values.

**Outcome:**
Improved API reliability and reduced potential errors in product creation by automating key validation checks.

**Code Sample:**
```python
import sender_stand_request
import data

def get_kit_body(name):
    current_kit_body = data.kit_body.copy()
    current_kit_body["name"] = name
    return current_kit_body

def get_new_user_token():
    response = sender_stand_request.post_new_user(data.user_body)
    return response.json()["authToken"]

def positive_assert(kit_body):
    response = sender_stand_request.post_new_client_kit(kit_body, get_new_user_token())
    assert response.status_code == 201
    assert response.json()["name"] == kit_body["name"]

def negative_assert_code_400(kit_body):
    response = sender_stand_request.post_new_client_kit(kit_body, get_new_user_token())
    assert response.status_code == 400

def test_kit_name_1_character(): #Prueba 1
    new_kit_body = get_kit_body("a")
    positive_assert(new_kit_body)

# ...rest of the tests...
```

## Other Projects
Before moving into tech, I worked as a screenwriter and creative lead, writing for film, branded content, and media. I see these projects as part of my portfolio too—they show my ability to build narratives, analyze details, and create clear, engaging communication.
