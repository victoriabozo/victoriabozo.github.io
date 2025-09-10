---
layout: default
---

# QA ENGINEER | QUALITY ASSURANCE ANALYST
I’m a QA Engineer with a background in screenwriting, translation, and content development, which has given me a sharp eye for detail and clarity. I don’t just look for bugs—I put myself in the end user’s shoes, making apps intuitive, clear, and enjoyable to use.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-6A8EDD?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/victoriabozo/)

## Technical Skills
Testing: Functional, Regression, Smoke, Non-functional | REST | JSON | SQL | Agile/Scrum | DevTools | Technical Writing

![Postman](https://img.shields.io/badge/Postman-3FB500?style=for-the-badge&logo=postman&logoColor=white)
![Jira](https://img.shields.io/badge/Jira-55B033?style=for-the-badge&logo=jira&logoColor=white)
![Python](https://img.shields.io/badge/Python-70C066?style=for-the-badge&logo=python&logoColor=white)
![Pytest](https://img.shields.io/badge/Pytest-85D099?style=for-the-badge&logo=pytest&logoColor=white)
![Selenium](https://img.shields.io/badge/Selenium-9AD0CC?style=for-the-badge&logo=selenium&logoColor=white)
![PyCharm](https://img.shields.io/badge/PyCharm-9FD8E0?style=for-the-badge&logo=pycharm&logoColor=white)
![Android Studio](https://img.shields.io/badge/Android%20Studio-93C1D6?style=for-the-badge&logo=android%20studio&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-7FA5C0?style=for-the-badge&logo=github&logoColor=white)
![Windows Terminal](https://img.shields.io/badge/Windows%20Terminal-6689A0?style=for-the-badge&logo=windows-terminal&logoColor=white)
![Canva](https://img.shields.io/badge/Canva-4F6B80?style=for-the-badge&logo=Canva&logoColor=white)
![Asana](https://img.shields.io/badge/Asana-3F587A?style=for-the-badge&logo=asana&logoColor=white)
![Trello](https://img.shields.io/badge/Trello-3F587A?style=for-the-badge&logo=Trello&logoColor=white)


# Projects
## Automated Taxi Booking – Urban Routes
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
- Setting origin and destination.
- Selecting Comfort fare.
- Entering and confirming phone number.
- Adding payment details and message for driver.
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

# 1. Set address:
    def test_set_route(self):
        address_from = data.address_from
        address_to = data.address_to
        self.routes_page.set_route(address_from, address_to)
        assert self.routes_page.get_from() == address_from
        assert self.routes_page.get_to() == address_to

# 2. Choose Comfort fare:
    def test_select_comfort_rate(self):
        self.routes_page.click_request_taxi_button()
        self.routes_page.click_comfort_rate_icon()
        assert self.routes_page.is_comfort_rate_selected()

# 3. Set and confirm phone number:
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


## Automated API Testing – Urban Grocers
[View Full Project on GitHub](https://github.com/victoriabozo/qa-project-Urban-Grocers-app-es)

**Overview:**
Automated validation of the name field in product kits for the Urban Grocers app. Ensured that kit names meet length and formatting criteria, catching invalid inputs before they reach production.

**Tools & Methods:**
- Python & pytest for test automation.
- *requests* library for HTTP API testing.
- Positive and negative tests for the "name" field.
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


# Work Samples
## Log Analysis & Error Classification
**Goal:** Save server logs for a specific time period and separate errors by code (400 and 500) into individual files for easier analysis.

**Commands used (exact sequence):**
```bash
cd ~ 
mkdir bug1

cd ~/bug1
mkdir events

touch main.txt

# Collect logs for the specified day and store them in main.txt
cat  ~/logs/2019/12/apache_2019-12-30.txt > ~/bug1/main.txt

# Filter 400 and 500 errors from main.txt into separate files
grep ' 400 ' ~/bug1/main.txt > ~/bug1/events/400.txt
grep ' 500 ' ~/bug1/main.txt > ~/bug1/events/500.txt
```

**Step-by-step explanation:**
- mkdir bug1 / mkdir events → create the working directory and the subdirectory where error files will be stored.
- touch main.txt and cat ... > ~/bug1/main.txt → ensure the file exists and load the logs for the specified day into it.
- grep ' 400 ' ... and grep ' 500 ' ... → extract lines containing status codes 400 and 500, saving them into separate files.

**Results Sample (real excerpts from the output files):**
```bash
~/bug1/events/400.txt
80.57.170.51 - - [30/12/2019:21:35:12 +0000] "DELETE /users HTTP/1.1" 400 3623
204.235.176.118 - - [30/12/2019:21:35:13 +0000] "POST /users HTTP/1.1" 400 4704
82.95.203.67 - - [30/12/2019:21:35:19 +0000] "DELETE /lists HTTP/1.1" 400 3737
155.242.215.46 - - [30/12/2019:21:35:38 +0000] "POST /playbooks HTTP/1.1" 400 4450
189.176.85.0 - - [30/12/2019:21:35:39 +0000] "PATCH /alerts HTTP/1.1" 400 2732
13.108.71.71 - - [30/12/2019:21:35:43 +0000] "PATCH /events HTTP/1.1" 400 3410
...

~/bug1/events/500.txt
64.250.112.189 - - [30/12/2019:21:35:13 +0000] "PUT /parsers HTTP/1.1" 500 4639
193.253.101.180 - - [30/12/2019:21:35:31 +0000] "PATCH /alerts HTTP/1.1" 500 2944
197.106.117.194 - - [30/12/2019:21:35:31 +0000] "PATCH /parsers HTTP/1.1" 500 3519
247.124.71.67 - - [30/12/2019:21:35:45 +0000] "PUT /alerts HTTP/1.1" 500 2746
62.88.204.119 - - [30/12/2019:21:35:51 +0000] "PUT /auth HTTP/1.1" 500 2666
125.156.142.26 - - [30/12/2019:21:36:01 +0000] "PATCH /events HTTP/1.1" 500 3460
...
```

**Outcome:** A structured directory ~/bug1 containing main.txt (logs for the chosen period) and ~/bug1/events/400.txt / ~/bug1/events/500.txt with lines filtered by error type — ready for developers or QA engineers to investigate root causes.


## Database | SQL
**Goal:** Retrieve the number of trips per taxi company for November 15–16, 2017, to verify discrepancies in reported earnings. Return company_name and trips_amount, ordered descending by trips_amount.

**Results Sample:**
```
company_name                                 | trips_amount
---------------------------------------------+--------------
Flash Cab                                     | 19558
Taxi Affiliation Services                     | 11422
Medallion Leasin                              | 10367
Yellow Cab                                    |  9888
Taxi Affiliation Service Yellow               |  9299
Chicago Carriage Cab Corp                     |  9181
City Service                                  |  8448
Sun Taxi                                      |  7701
Star North Management LLC                     |  7455
Blue Ribbon Taxi Association Inc.             |  5953
...
```

**SQL query used:**
```bash
SELECT
    cabs.company_name AS company_name,
    COUNT(DISTINCT trip_id) AS trips_amount
FROM
    trips
INNER JOIN weather_records ON trips.start_ts = weather_records.ts
INNER JOIN cabs ON trips.cab_id = cabs.cab_id
WHERE 
    weather_records.ts BETWEEN '2017-11-15 00:00:00' 
    AND '2017-11-16 23:59:59'
GROUP BY
    company_name
ORDER BY
    trips_amount DESC;
```

## Bug Report – Urban Scooter Push Notification
Critical issue where scheduled push notifications for upcoming deliveries did not appear. Reproduced the bug by creating a courier and order via Postman, then simulating delivery time on an Android Studio emulator. Documented steps, expected vs. actual results, environment details, and severity for a clear, actionable report.

**Preconditions:**
- Postman account.
- Android Studio installed.
- Urban Scooter installed on an Android Studio device.
- Environment configured.

**Steps to Reproduce:**
1. Restart the server if it was active.
2. Open Postman.
3. Create a courier:<br/>
   a. Request Type: POST<br/>
   b. Endpoint: /api/v1/courier<br/>
   c. Body:<br/>
```json
{
  "login": "ninja",
  "password": "1234",
  "firstName": "saske"
}
```

4. Create an order:<br/>
   a. Request Type: POST<br/>
   b. Endpoint: /api/v1/orders<br/>
   c. Body: (deliveryDate must be at least 2 days in the future)<br/>
```json
{
  "firstName": "Naruto",
  "lastName": "Uchiha",
  "address": "2 Alton Lane",
  "metroStation": 4,
  "phone": "+7 800 355 35 35",
  "rentTime": 5,
  "deliveryDate": "2025-08-14",
  "comment": "Saske, come back to Konoha. Saske, come back to Konoha.",
  "color": ["BLACK"]
}
```
5. Accept the order:<br/>
   a. Request Type: PUT<br/>
   b. Endpoint: /api/v1/orders/accept/1?courierId=1<br/>
6. Open the Urban Scooter mobile app.
7. Log in with the courier account created.
8. Close the app but leave the session active.
9. Set the device date to the delivery day (August 14, 2025).
10. Set the device time to 21:58.
11. Lock the device and wait until 21:59.

**Expected Result:** A push notification appears 2 hours before the delivery deadline (23:59).

**Actual Result:** No push notification is received.

**Severity:** Critical. <br/> 
**Priority:** Highest.

**Environment:**
- Android Studio Emulator
- OS: Android 9.0 Pie
- Resolution: 1080 x 1920 px
- Screen: 5.5”
- RAM: 1GB
- Internal Storage: 3GB

**Active server URL at time of testing:** [URL]

**Attachments:**  
![Notifications ON](assets/reporte/US1%20Notificaciones%20activadas.jpg)  
![Data base](assets/reporte/US1%20base%20de%20datos.jpg)  
![Test input](assets/reporte/US1%20datos%20de%20la%20prueba.jpg) 
![Courier app](assets/reporte/US1%20prueba%20aceptada%20por%20repartidor.jpg)
[No push notifications](assets/reporte/US1%20no%20hay%20notificación%20push.%20pruebas%20en%20limites.mp4)  
