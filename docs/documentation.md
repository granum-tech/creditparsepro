<h1 align="center">creditparsepro.io</h1>

<p align="center">
  <img src="../images/creditparsepro_logo.png" alt="credit parse pro logo" width="200">
</p>

<p align="center">
  Enable next-gen fintech innovations with <strong>creditparsepro.io</strong>:  
  Our API parses fixed-length credit reports from major US bureaus, delivering <strong>ML ready JSON data</strong>.
</p>

<p align="center">
  <a href="https://www.creditparsepro.io/">Website</a> | 
  <a href="https://x.com/granum_tech">Twitter</a> | 
  <a href="https://github.com/granum-tech/creditparsepro/blob/main/README.md">GitHub</a> |   
  <a href="https://github.com/granum-tech/creditparsepro/blob/main/docs/documentation.md">Docs</a> | 
  <a href="https://www.postman.com/creditparsepro/creditpasrepro-demo/collection/fzq473l/api-endpoints?action=share&creator=34164250">Postman</a> | 
  <a href="https://billing.stripe.com/p/login/14kaHj8NX5LJ5Ta8ww">Stripe Billing Portal</a>
</p>

# **Documentation**

## **Overview**
This document is a comprehensive guide covering getting started, authentication, the API endpoints and responses, and the data provided. It serves as a reference for developers, data analysts, and other stakeholders to understand the formats and structures of the extracted credit report data.

## **Table of Contents**
1. [About](#about)
2. [Version](#version)
3. [Getting Started](#getting-started)
4. [Support](#support)
5. [Authentication](#authentication)
6. [Quota & Rate Limits](#quota--rate-limits)
7. [Error & Response Messages](#error--response-messages)
8. [Endpoints](#endpoints)
   - [POST v1/parse-report](#post-v1parse-report)
     - [Response](#response)
     - [Request Headers](#request-headers)
     - [Body](#body)
     - [Examples](#examples)          
   - [GET v1/quota-info](#get-v1quota-info)
     - [Response](#response-1)   
     - [Request Headers](#request-headers-1)
     - [Examples](#examples-1)      
   - [GET v1/rate-info](#get-v1rate-info)
     - [Response](#response-2)   
     - [Request Headers](#request-headers-2)
     - [Examples](#examples-2)        
9. [Data Dictionary](#data-dictionary)
   - [Field Format Convetions](#field-format-conventions)
   - [Inquiries](#inquiries)
   - [Personal Information](#personal-information)
   - [Public Records](#public-records)
   - [Score](#score)
   - [Tradelines](#tradelines)
   - [Summary](#summary)

---

## About

Are you struggling to leverage credit report data effectively for analytics and machine learning? Many loan origination systems provide credit report data in a cumbersome, fixed-format text. This not only hampers your ability to perform in-depth analysis but also requires navigating through extensive documentation and complex logic to parse the data.

Introducing our API solution – the bridge to transforming traditional credit report data into a dynamic format ready for advanced fintech applications. Our software parses curated fields for both analytics and machine learning use-cases in a ready-to-use JSON format.

Unlock the full potential of your data with our API, and step into a new era of financial technology applications. Say goodbye to outdated processes and embrace a future where your data works for you, enabling faster, more accurate decision-making.

## **Version**
- **Current Version**: 1.0.0

## Getting Started

1. Use our [Postman](https://www.postman.com/creditparsepro/creditpasrepro-demo/collection/fzq473l/api-endpoints?action=share&creator=34164250) collection to test our API endpoints to ensure our product is right for you. And if you have further questions reach out to info@creditparsepro.io.
2. Visit our [website](https://www.creditparsepro.io/) and pick a free or paid subscription plan via our Stripe integration.
3. Receive an automated email with your API key via our SendGrid integration.
4. Review our [documentation](/docs/documentation.md).

## Support

Please contact us at [info@creditparsepro.io](mailto:info@creditparsepro.io) for suppoer and inquiries.


## **Authentication**

Authenticate each request by including the request header `x-api-key`. This was sent to you via Email when signing up.

It is okay to share your API key within your organization as there are no seat limits imposed only rate and quota limits.

In the case that a key is lost please email us from the email used to signup at info@creditparsepro.io.

If an API key is missing, malformed, or invalid, you will receive an HTTP 401 Unauthorized response code.


## **Quota & Rate Limits**

API access rate and quota limits apply at a per-API key basis in unit time. The rate and quota you are offered depends on the product subscription tier that you chose. If you would like to upgrade you can do so at any time in the [Stripe billing portal](https://billing.stripe.com/p/login/14kaHj8NX5LJ5Ta8ww). You can see our detailed product offerings on our [website](https://www.creditparsepro.io/pricing).

You can check your current rate and quota limits using the GET requests [GET v1/quota-info](#get-v1quota-info) and [GET v1/rate-info](#get-v1rate-info).

If you either reach your quota or rate limit you will receive a 401 error message.

## **Error & Response Messages**

If you receive a 200 response your request was successful. Otherwise potential errors are shown in the table below.

| Error                | Description                                                                   |
|----------------------|-------------------------------------------------------------------------------|
| 400       | Bad Request: The request was malformed. Possibly due to a missing required parameter or a required parameter with an invalid value/data type.|
| 401       | Unauthorized: The API key was missing or invalid. The rate or quota limit is at maximum.|
| 500       | Internal Server Error: Likely an issue with the credit_report_text parameter formatting.|

## **Endpoints**

### **POST v1/parse-report**

**Production:** `https://api.creditparsepro.io/v1/parse-report`  
**Test:** `https://test.creditparsepro.io/v1/parse-report`

Parses fixed-format credit reports from major bureaus - automatically detecting the bureau and report version and returning data in JSON format. Successful POST requests do affect your quota and rate limits based on your product tier.

#### **Response**

See the [Data Dictionary](#data-dictionary) below for details or view and run examples directly in your browser on our [Postman](https://www.postman.com/creditparsepro/creditpasrepro-demo/request/jucxwj6/v1-parse-report).

#### **Request Headers**

* `Content-Type: application/json`  
* `x-api-key: {{x-api-key}}`

#### **Body**

* `credit_report_text` - REQUIRED - Full text of the credit report.
* `format` - OPTIONAL - Defaults to `complete` which includes `summary`. You can request `summary` on it's own.
* `gross_monthly_income` - OPTIONAL - Used in calculating the `dti` field in the `summary` if provided.
* `outcome` - OPTIONAL - Outcome indicator `0` or `1` accepted values.

#### **Examples**

View and run examples directly in your browser on our [Postman](https://www.postman.com/creditparsepro/creditpasrepro-demo/request/jucxwj6/v1-parse-report).

### **GET v1/quota-info**

**Production:** `https://api.creditparsepro.io/v1/quota-info`  
**Test:** `https://test.creditparsepro.io/v1/quota-info`

This GET request retrieves your current quota usage, including the total allowed requests and the reset date. This request does not use up your quota and can be requested an unlimited amount of times.

#### **Response**

* `quota_count` - Total of successful requests used this month.
* `quota_limit` - Your monthly request limit.
* `quota_reset_date` - {yyyy-MM-dd hh:mm:ss} of when your quota_count will reset to 0.

#### **Request Headers**

* `Content-Type: application/json`  
* `x-api-key: {{x-api-key}}`

#### **Examples**

View and run examples directly in your browser on our [Postman](https://www.postman.com/creditparsepro/creditpasrepro-demo/request/xfrvhg1/v1-quota-info).

### **GET v1/rate-info**

**Production:** `https://api.creditparsepro.io/v1/rate-info`  
**Test:** `https://test.creditparsepro.io/v1/rate-info`

This GET request provides information on your current rate limit, showing how many requests you can make per minute. This request does not use up your quota and can be requested an unlimited amount of times.

#### **Response**

* `last_request_minute` - {yyyy-MM-dd hh:mm:ss} this field is set when a successful request is made if there has been more than a minute passed. When it is set the rate_count is reset back to 0.
* `rate_count` - Total of successful requests used this minute.
* `rate_limit` - Your per minute request limit.

#### **Request Headers**

* `Content-Type: application/json`  
* `x-api-key: {{x-api-key}}`

#### **Examples**

View and run examples directly in your browser on our [Postman](https://www.postman.com/creditparsepro/creditpasrepro-demo/request/1akduyg/v1-rate-info).

## **Data Dictionary**

### **Field Format Conventions**
- **Date Fields**: All date fields are ISO8601 format (`YYYY-MM-DD`).
- **Currency Fields**: Represented as integers (e.g., `10000` for $100.00).
- **Boolean Fields**: Represented as `true` or `false`.
- **Categorical Fields**: Represented as string values from a predefined list.
---

### **Inquiries**

| Field Name           | Type      | Description                                                                 | Example           | Notes                                  |
|----------------------|-----------|-----------------------------------------------------------------------------|-------------------|----------------------------------------|
| `inquiry_date`       | Date      | The date of the inquiry, formatted as `YYYY-MM-DD`.                         | `2025-01-01`      | Parsed from segment-specific formats.  |
| `amount`             | Integer   | The amount associated with the inquiry, if applicable.                      | `5000`            | May be `null` if no amount is provided.|
| `inquiry_type.key`   | String    | The code representing the industry type of inquiry or portfolio.            | `F`               | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `inquiry_type.value` | String    | The descriptive value corresponding to `inquiry_type.key`.                  | `Finance/personal`| Mapped from `inquiry_type.key`.       |
| `industry_type.key`  | String    | The code representing the industry type of the inquiry.                     | `07`              | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `industry_type.value`| String    | The descriptive value corresponding to `industry_type.key`.                 | `Charge Account`  | Mapped from `industry_type.key`.   |
| `subscriber_name`    | String    | The name of the subscriber (creditor) that initiated the inquiry.           | `CAPITAL ONE`     | Extracted from subsegments or fields.  |


### **Personal Information**

| Field Name                      | Type      | Description                                       | Example              | Notes                                  |
|---------------------------------|-----------|---------------------------------------------------|----------------------|----------------------------------------|
| `social_security_number`        | String    | Social Security Number of the individual.         | `123456789`               |                                        |
| `date_of_birth`                 | Date      | The date of birth of the individual.              | `1985-07-15`              | Format: ISO8601 (`YYYY-MM-DD`).        |
| `names.first_name`              | String    | First name of the individual.                     | `JOHN`                    | All capitalized.                       |
| `names.middle_name`             | String    | Middle name of the individual.                    | `A`                       | All capitalized.                       |
| `names.last_name`               | String    | Last name of the individual.                      | `DOE`                     | All capitalized.                       |
| `names.suffix`                  | String    | Suffix of the individual (e.g., Jr., Sr.).        | `JR`                      | All capitalized.                       |
| `names.is_primary`              | Boolean   | Indicates if this is the primary name.            | `1`                       | `1` for primary, `0` otherwise.        |
| `addresses.first_reported_date` | Date      | The first date the address was reported.          | `2020-01-01`              | Format: ISO8601 (`YYYY-MM-DD`).        |
| `addresses.dwelling_type.key`   | String    | Code for the dwelling type.                       | `S`                       | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `addresses.dwelling_type.value` | String    | Description of the dwelling type.                 | `Single-family dwelling`  | Mapped from `dwelling_type.key`. |
| `addresses.street_number`       | String    | Street number of the address.                     | `123`                     |                                        |
| `addresses.prefix`              | String    | Prefix direction of the street (e.g., N, S).      | `N`                       | All capitalized.                       |
| `addresses.street`              | String    | Street name of the address.                       | `MAIN ST`                 |                                        |
| `addresses.suffix`              | String    | Suffix direction of the street (e.g., Ave, Blvd). | `DR`                      | All capitalized.                       |
| `addresses.unit`                | String    | Unit or apartment number.                         | `APT 4B`                  | All capitalized.                       |
| `addresses.city`                | String    | City of the address.                              | `SPRINGFIELD`             | All capitalized.                       |
| `addresses.state`               | String    | State of the address.                             | `IL`                      | Format: 2-character state code. All capitalized.        |
| `addresses.zip`                 | String    | ZIP code of the address.                          | `15211` or `152119998`    | May include extended format.           |
| `addresses.is_most_recent`      | Boolean   | Indicates if this is the most recent address.     | `1`                       | `1` for most recent, `0` otherwise.    |
| `employment.employer_name`      | String    | Name of the employer.                             | `ACME CORP`               | All capitalized. Defaults to `Unknown` if not available.|
| `employment.occupation`         | String    | Occupation or job title.                          | `SOFTWARE ENGINEER`       | All capitalized. Defaults to `Unknown` if not available.|
| `employment.reported_date`      | Date      | The date the employment was reported.             | `2021-06-01`              | Format: ISO8601 (`YYYY-MM-DD`).        |
| `employment.income`             | Integer   | Income reported for the job.                      | `75000`                   | Defaults to `null` if not available.   |
| `employment.pay_basis.key`      | String    | Code for the pay basis (e.g., H for Hourly).      | `M`                       | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `employment.pay_basis.value`    | String    | Description of the pay basis.                     | `Monthly`                 | Mapped from `pay_basis.key`.     |
| `employment.is_most_recent`     | Boolean   | Indicates if this is the most recent employment.  | `1`                       | `1` for most recent, `0` otherwise.    |


### **Public Records**
| Field Name                                      | Type      | Description                                                        | Example              | Notes                                  |
|-------------------------------------------------|-----------|--------------------------------------------------------------------|----------------------|----------------------------------------|
| `public_record_type.key`                        | String    | Code for the type of public record.                                | `1X`                 | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `public_record_type.value`                      | String    | Description of the public record type.                             | `Bankruptcy`         | Mapped from `public_record_type.key`. |
| `reference_number`                              | String    | Reference number associated with the public record.                | `125431`             | May be masked or truncated.            |
| `plaintiff`                                     | String    | Name of the plaintiff or party associated with the public record.  | `John Doe`           | Defaults to `Unknown` if not available. |
| `file_date`                                     | Date      | Date the public record was filed.                                  | `2023-07-01`         | Format: ISO8601 (`YYYY-MM-DD`).                  |
| `amount`                                        | Integer   | Monetary amount associated with the public record (e.g., judgment amount).| `15000`              | May be `null` if not applicable.        |
| `equal_credit_opportunity_act_designator.key`   | String    | Code for the ECOA (Equal Credit Opportunity Act) designator.       | `I`                  | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `equal_credit_opportunity_act_designator.value` | String    | Description of the ECOA designator.                                | `Individual`         | Mapped from `equal_credit_opportunity_act_designator.key`. |


### **Score**
| Field Name                  | Type     | Description                                                                | Example            | Notes                                  |
|-----------------------------|----------|----------------------------------------------------------------------------|--------------------|----------------------------------------|
| `score`                     | Integer  | The calculated credit score.                                               | `750`              | May vary by bureau and score model.    |
| `sign`                      | String   | Indicates whether the score is positive (+) or negative (-).               | `+`                | Can be `+` or `-`        |
| `score_factor_1.key`        | String   | Code for the first score factor.                                           | `01`               | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `score_factor_1.value`      | String   | Description of the first score factor.                                     | `HIGH CREDIT USAGE`| Mapped from `score_factor_1.key`.      |
| `score_factor_2.key`        | String   | Code for the second score factor.                                          | `02`               | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `score_factor_2.value`      | String   | Description of the second score factor.                                    | `MISSED PAYMENTS`  | Mapped from `score_factor_2.key`.      |
| `score_factor_3.key`        | String   | Code for the third score factor.                                           | `03`               | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `score_factor_3.value`      | String   | Description of the third score factor.                                     | `LIMITED HISTORY`  | Mapped from `score_factor_3.key`.      |
| `score_factor_4.key`        | String   | Code for the fourth score factor.                                          | `04`               | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `score_factor_4.value`      | String   | Description of the fourth score factor.                                    | `NEW ACCOUNTS`     | Mapped from `score_factor_4.key`.      |
| `service_model`             | String   | Code indicating the service or model used to calculate the score.          | `P00W40`           | Prefixed `P` for certain codes.        |


### **Tradelines**
| Field Name                       | Type     | Description                                                            | Example               | Notes                                  |
|----------------------------------|----------|------------------------------------------------------------------------|-----------------------|----------------------------------------|
| `account_number`                 | String   | The account number associated with the tradeline.                      | `1234567890`          |                                        |
| `open_date`                      | Date     | The date when the account was opened.                                  | `2021-01-01`          | Format: ISO8601 (`YYYY-MM-DD`).        |
| `close_date`                     | Date     | The date when the account was closed.                                  | `2022-12-31`          | Format: ISO8601 (`YYYY-MM-DD`). Empty if the account is still open.|
| `is_open`                        | Boolean  | Indicates if the account is currently open.                            | `1`                   | `1` for open, `0` for closed.          |
| `portfolio_type.key`             | String   | Code for the portfolio type of the tradeline.                          | `R`                   | Specific to each bureau's mapping, reach out to info@creditparsepro.io for details.|
| `portfolio_type.value`           | String   | Description of the portfolio type.                                     | `Revolving`           | Mapped from `portfolio_type.key`.      |
| `current_balance`                | Integer  | The current balance on the account.                                    | `5000`                | May be `0` if account is paid off.     |
| `original_balance`               | Integer  | The original balance on the account.                                   | `10000`               | Not applicable for all types. `0` if not applicable. |
| `high_balance_amount`            | Integer  | The highest balance ever recorded on the account.                      | `8000`                | Not applicable for all types. `0` if not applicable. |
| `credit_limit_amount`            | Integer  | The credit limit for the account.                                      | `10000`               | Not applicable for all types. `0` if not applicable. |
| `past_due_amount`                | Integer  | The amount currently past due.                                         | `200`                 | May be `0` if no past due balance.     |
| `maximum_delinquency_date`       | Date     | The date of the most severe delinquency recorded on the account.       | `2022-06-01`          | Format: ISO8601 (`YYYY-MM-DD`). Can be empty.|
| `maximum_delinquency_amount`     | Integer  | The highest past due amount recorded on the account.                   | `300`                 |                                        |
| `times_30_days_late`             | Integer  | Number of times the account was 30 days late on payments.              | `2`                   | Defaults to `0`.                       |
| `times_60_days_late`             | Integer  | Number of times the account was 60 days late on payments.              | `1`                   | Defaults to `0`.                       |
| `times_90_days_late`             | Integer  | Number of times the account was 90+ days late on payments.             | `0`                   | Defaults to `0`.                       |
| `term`                           | Integer  | The repayment term for accounts in months.                             | `60`                  | Defaults to `0`.                       |
| `monthly_payment`                | Integer  | The scheduled monthly payment amount for the account.                  | `200`                 | Defaults to `0`.                       |
| `last_payment_date`              | Date     | The date of the last payment made on the account.                      | `2022-11-01`          | Format: ISO8601 (`YYYY-MM-DD`). Can be empty.|


### **Summary**

| Field Name                                        | Type       | Description                                                                  | Example             | Notes                        |
|---------------------------------------------------|------------|------------------------------------------------------------------------------|---------------------|------------------------------|
| `date`                                            | String     | The date the credit report was generated.                                    | `2025-01-01`        | Format: ISO8601 (`YYYY-MM-DD`).|
| `age`                                             | Integer    | The individual's age, calculated from the date of birth.                     | `35`                | Based on the report's date.  |
| `score`                                           | Integer    | Credit score of the individual.                                              | `750`               |                              |
| `dti`                                             | Float      | Debt-to-income ratio, calculated if `gross_monthly_income` is provided.      | `25.5`              | Rounded to 2 decimal places. |
| `tradelines.overall.total_accounts`               | Integer    | Total number of tradelines in the credit report.                             | `15`                |                              |
| `tradelines.overall.open_accounts`                | Integer    | Number of open tradelines in the report.                                     | `5`                 |                              |
| `tradelines.overall.total_monthly_payments`       | Float      | Total monthly payment amounts across all tradelines.                         | `1200.50`           |                              |
| `tradelines.overall.oldest_open_date_months`      | Integer    | Age of the oldest open tradeline, in months.                                 | `120`               |                              |
| `tradelines.revolving.open_sum`                   | Float      | Total credit limit for open revolving tradelines.                            | `20000.00`          |                              |
| `tradelines.revolving.open_count`                 | Integer    | Number of open revolving tradelines.                                         | `3`                 |                              |
| `tradelines.revolving.total_count`                | Integer    | Total number of revolving tradelines.                                        | `5`                 |                              |
| `tradelines.revolving.revolving_utilization_ratio`| Float      | Credit utilization ratio for revolving tradelines.                           | `30.0`              | Percentage value.            |
| `tradelines.installment.open_count`               | Integer    | Number of open installment tradelines.                                       | `2`                 |                              |
| `tradelines.installment.total_count`              | Integer    | Total number of installment tradelines.                                      | `4`                 |                              |
| `tradelines.installment.installment_utilization_ratio` | Float | Utilization ratio for installment tradelines.                                | `70.0`              | Percentage value.            |
| `tradelines.installment.open_sum`                 | Float      | Total balance for open installment tradelines.                               | `5000.00`           |                              |
| `tradelines.mortgage.open_count`                  | Integer    | Number of open mortgage tradelines.                                          | `1`                 |                              |
| `tradelines.mortgage.total_count`                 | Integer    | Total number of mortgage tradelines.                                         | `1`                 |                              |
| `tradelines.credit.open_count`                    | Integer    | Number of open credit tradelines.                                            | `4`                 |                              |
| `tradelines.credit.total_count`                   | Integer    | Total number of credit tradelines.                                           | `6`                 |                              |
| `address.change_count`                            | Integer    | Number of address changes recorded.                                          | `3`                 | Excludes current address.    |
| `address.months_at_current_address`               | Float      | Duration of stay at the current address, in months.                          | `24.5`              | Rounded to 2 decimal places. |
| `address.address_changes_per_year`                | Float      | Average number of address changes per year.                                  | `0.5`               |                              |
| `address.state`                                   | String     | The state abbreviation of the current address.                               | `CA`                | Lowercased.                  |
| `address.zip`                                     | String     | The ZIP code of the current address.                                         | `90210`             |                              |
| `employment.months_at_current_employer`           | Float      | Duration of employment at the current job, in months.                        | `18.5`              | Rounded to 2 decimal places. |
| `delinquencies.past_due.open_count`               | Integer    | Number of open past-due tradelines.                                          | `1`                 |                              |
| `delinquencies.past_due.total_count`              | Integer    | Total number of past-due tradelines.                                         | `3`                 |                              |
| `delinquencies.past_due.open_sum`                 | Float      | Total balance of open past-due tradelines.                                   | `2000.00`           |                              |
| `delinquencies.times_late.30_days_sum`            | Integer    | Total count of 30-day late payment instances.                                | `2`                 |                              |
| `delinquencies.times_late.60_days_sum`            | Integer    | Total count of 60-day late payment instances.                                | `1`                 |                              |
| `delinquencies.times_late.90_days_sum`            | Integer    | Total count of 90-day late payment instances.                                | `0`                 |                              |
| `public_records.count`                            | Integer    | Total number of public records reported.                                     | `1`                 |                              |
| `public_records.bankruptcy_count`                 | Integer    | Number of bankruptcy records reported.                                       | `1`                 |                              |
| `collections.count`                               | Integer    | Total number of collection records.                                          | `2`                 |                              |
| `inquiries.total_count`                           | Integer    | Total number of credit inquiries.                                            | `6`                 |                              |
| `inquiries.past_6_months_count`                   | Integer    | Number of inquiries in the past 6 months.                                    | `3`                 |                              |


---
