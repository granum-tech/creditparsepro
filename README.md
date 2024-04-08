<h1 align="center">creditparsepro.io</h1>


<p>
  <img src="images/creditparsepro_logo.png" alt="credit parse pro logo" width="200" style="float: left; margin-right: 20px;">

  Enable next-gen fintech innovations with **creditparsepro.io**:  
  Our API parses fixed-length credit reports from major US bureaus, delivering **ML ready JSON data**.  

  Whether your company is sitting on years of historical fixed-length credit reports or this is the format your operational systems use today, our API can enable modern solutions and insights.

  Visit our website **[creditparsepro.io](https://www.creditparsepro.io/)** to signup.  
  Returning customer billing portal **[stripe.creditparsepro.io](https://billing.stripe.com/p/login/14kaHj8NX5LJ5Ta8ww)**.
</p>  

# Contents
- [About](#about)
- [Getting Started](#getting-started)
    - [Sign Up](#sign-up)
    - [Quick Start](#quick-start)
        - [Example Request](#example-request)
        - [Example Response](#example-response)
- [Authentication](#authentication)
- [Request & Response Formats](#request--response-formats)
    - [Requests](#requests)
    - [Responses](#responses)
- [Endpoints and Operations](#endpoints-and-operations)
    - [Test/Production](#testproduction)
    - [Quota Information (/v1/quota-info)](#quota-information-v1quota-info)
        - [Example Request](#example-request-1)
        - [Example Response](#example-response-1)
    - [Rate Information (/v1/rate-info)](#rate-information-v1rate-info)
        - [Example Request](#example-request-2)
        - [Example Response](#example-response-2)
    - [Parse Credit Report (/v1/parse-report)](#parse-credit-report-v1parse-report)
        - [Example Request](#example-request-3)
        - [Example Response 'analytics' format](#example-response-analytics-format)
        - [Example Response 'ml' format](#example-response-ml-format)        
- [Error Codes and Messages](#error-codes-and-messages)
- [Rate Limiting and SLA](#rate-limiting-and-sla)
- [Feature Roadmap](#feature-roadmap)
- [Support](#support)
- [Appendix](#appendix)
    - [A. Experian AFR Example Report](#a-experian-afr-example-report)
    - [B. TransUnion 4.0 FFR Example Report](#b-transunion-40-ffr-example-report)
    - [C. Field Calculations and Descriptions](#c-field-calculations-and-descriptions)
    - [D. Pricing & Plans](#d-pricing--plans)

## About

Are you stuck with historical and/or operational fixed-length format credit reports and are trying to enable analytics and machine learning for your organization?

Many companies rely on connectors and servicers to handle the process of sending a request to the credit bureaus and presenting the returned reports. Many of these connectors are outdated and still provide only a human-readable and fixed-length format. Until now, fixed-length formats required hundreds of pages of documentation and conditional logic to parse. 

Now with our API you can pull that data and process it in a format that is useful for analytics and machine learning enabling fintech use-cases.

* Automated Underwriting
* Credit Scoring Models
* Fraud Detection
* Risk Assessment
* Bankruptcy Predictions
* Debt Collection Optimization

## Getting Started

### Sign Up

1. Visit our website [creditparsepro.io/pricing](https://www.creditparsepro.io/pricing)
2. Choose a product tier - note that our **test** tier will <u>always</u> be free
3. Upon signing up you will receive an email with your API key

It is critical that you store your API keys securely. If you lose access to them please reach out to info@creditparsepro.io for assistance. 

### Quick Start

Once you've obtained your API key, you can quickly test the API with a sample request. 

The below curl is lengthy because it includes the entirety of a sample credit report in the **credit_report_text** variable. You can set your credit report text to a variable prior and pass the variable instead if you would like. To see example fixed-length credit reports see the [Appendix](#appendix).

Note that **outcome** and **gross_monthly_income** fields are optional. You can read more about this in the [Endpoints and Operations](#endpoints-and-operations) section.

#### Example request:
```bash
curl -X POST "https://api.creditparsepro.io/v1/parse-report" \
     -H "X-API-KEY: yourKeyHere" \
     -H "Content-Type: application/json" \
     -d '{
           "gross_monthly_income": 5000,
           "outcome": 1,
           "credit_report_text": "TU4R062011                        1614F 0459317220240229143215PH0101207000SH01027101Y05N03PEN20210602NM01070F1DAY                      SUNNY                               PI01029F66688567819910601    AD01105F11333         HOPP                         CT     FANTASY ISLAND             IL60750     20221206AD01105F111233      S CARROT                       ST     FANTASY ISLAND             IL60750     20200408EM01100ASDF                               F                                      20240110V          EM01100DEFI SLUTIONS                      FDEVELOPER                             20240110V          TR01288Q 0202V002WLM P & F CU            I44009                   I2020042620240101V                         051000003817000006587         034M000000242                                    US            00         2024010105                                                        00       TR01288B 041PF002FST PREMIER             R38294                   I2022060120240101V                         011000000184000000414000007500                                                               00                   20231201111111111X11                                    120000002TR01288B 09616003DISCOVERBANK            R4                       I2012042520240101V                         011000000093000000093000008000MIN 000000010                                    CC            00                   2023120111111111111111111111111111111                   290000002TR01288Q 06262001PROVDENT FCU            I75500045                I2020100420240101V                         011000000554000001005                                                                        00                   202312011111111111111111111111111                       250000002TR01288B 0848R015WILM TRUST              M698007                  I1995013120240101V                         011000003327000036500         300M000000163                                    RE            00                   20231201111111111111111111111111                        240000002TR01288D 0160Q001BOSCOVS                 R1                       I2007121020231201V                         011000000019000000272         MIN 000000010                                                  00                   202311011XXXXX111111XX1XXX111X1XXXXXXXXXXXX111111XX1X11 470000002TM01040000000000001000000000005000000000IN0106516ORF 04593172NEEDHAM/RECF            I           20240229IN0106540PEY 02462756MIDLAND CRED            I           20240113OB01148TRANSUNION TEST FACILITY                          555 W ADAMS                             CHICAGO, IL 60661            800-888-4213          AO0101700Q8804   SC0103400Q88+696    039013027018  AO010170680004O01AO010170705101M00ENDS010024"
         }'
```
#### Example response
```JSON
{
  "address": {
    "address_changes_per_year": 0.26,
    "change_count": 1,
    "months_at_current_address": 14.78
  },
  "age": 32,
  "date": "2024-02-29",
  "collections": {
    "count": 0
  },
  "delinquencies": {
    "past_due": {
      "open_count": 0,
      "open_sum": 0,
      "total_count": 0
    },
    "times_late": {
      "30_days_sum": 0,
      "60_days_sum": 0,
      "90_days_sum": 0
    }
  },
  "dti": 8.5,
  "employment": {
    "months_at_current_employer": 0
  },
  "inquiries": {
    "past_6_months_count": 2,
    "total_count": 2
  },
  "outcome": 1,
  "public_records": {
    "count": 0
  },
  "score": 696,
  "tradelines": {
    "credit": {
      "open_count": 0,
      "total_count": 0
    },
    "installment": {
      "installment_utilization_ratio": 57.57,
      "open_count": 2,
      "open_sum": 7592,
      "total_count": 2
    },
    "mortgage": {
      "open_count": 1,
      "total_count": 1
    },
    "overall": {
      "oldest_open_date_months": 349,
      "open_accounts": 6,
      "total_accounts": 6,
      "total_monthly_payments": 425
    },
    "revolving": {
      "open_count": 3,
      "open_sum": 15500,
      "revolving_utilization_ratio": 1.91,
      "total_count": 3
    }
  }
}
```

## Authentication

All API requests must be authenticated using your API key provided during the sign-up process. Please note that you will be provided an API key for both the test (test.creditparsepro.io) and production (api.creditparsepro.io) endpoints via email upon signing up. It is okay to share this key within your organization. There are no seat limits just rate limits. Please keep your key secure somewhere.

In the case that a key is lost we will need to verify identity using the email address that initially signed up.

Include your API key in the request header as X-API-KEY.  

Unauthorized requests will be returned with a 401 status code.

## Request & Response Formats

All requests to the creditparsepro.io API must be sent as HTTP requests formatted as JSON with UTF-8 encoding.
Similarly, responses are returned in JSON format.

### Requests
- Content-Type header must be set to `application/json`.
- Ensure your JSON payload is properly formatted and encoded in UTF-8.

### Responses
- Responses will be JSON objects.
- All responses include HTTP status codes to indicate success or failure of the request.
- For detailed response structures, refer to the specific [endpoint documentation](#endpoints-and-operations).

## Endpoints and Operations

### Test/Production

All accounts come with test and production endpoint access.
There is no SLA associated with the test endpoint as it may be used for internal testing purposes and for public user-acceptance testing of new features.

Production endpoint:
```
https://api.creditparsepro.io/v1/parse-report
```

Test endpoint:
```
https://test.creditparsepro.io/v1/parse-report
```


### Quota Information (/v1/quota-info)
- Description: 
    - Retrieves your current quota usage, including the total allowed requests and the reset date. This request does not use up your quota and can be requested an unlimited amount of times.  
- URL:
    - https://api.creditparsepro.io/v1/quota-info
    - https://test.creditparsepro.io/v1/quota-info
- Method: 
    - GET
- Header: 
    - X-API-KEY: yourKeyHere
    - Content-Type: application/json
- Response:
    - **quota_count**: Total of successful requests used this month.
    - **quota_limit**: Your monthly request limit.
    - **quota_reset_date**: {yyyy-MM-dd hh:mm:ss} of when your **quota_count** will reset to 0.

#### Example request
```bash
curl -X GET https://api.creditparsepro.io/v1/quota-info \ 
     -H "X-API-KEY: yourKeyHere" \ 
     -H "Content-Type: application/json"
```
#### Example response
```JSON
{
  "quota_count": 43,
  "quota_limit": 1000,
  "quota_reset_date": "2024-03-24 21:23:47"
}
```

### Rate Information (/v1/rate-info)
- Description: 
    - Provides information on your current rate limit, showing how many requests you can make per minute. This request does not use up your quota and can be requested an unlimited amount of times.  
- URL:
    - https://api.creditparsepro.io/v1/rate-info
    - https://test.creditparsepro.io/v1/rate-info
- Method: 
    - GET
- Header:
    - X-API-KEY: yourKeyHere
    - Content-Type: application/json
- Response:
    - **last_request_minute**: {yyyy-MM-dd hh:mm:ss} this field is set when a successful request is made if there has been more than a minute passed. When it is set the **rate_count** is reset back to 0.
    - **rate_count**: Total of successful requests used this minute.
    - **rate_limit**: Your per minute request limit.

#### Example request
```bash
curl -X GET https://api.creditparsepro.io/v1/rate-info \ 
     -H "X-API-KEY: yourKeyHere" \ 
     -H "Content-Type: application/json"
```

#### Example response
```JSON
{
  "last_request_minute": "2024-03-12 19:30:15",
  "rate_count": 0,
  "rate_limit": 30
}
```

### Parse Credit Report (/v1/parse-report)
- Description: 
    - Parses the credit report text provided and returns a structured summary suitable for machine learning applications.
- URL:
    - https://api.creditparsepro.io/v1/parse-report
    - https://test.creditparsepro.io/v1/parse-report
- Method: 
    - POST
- Header:
    - X-API-KEY: yourKeyHere
    - Content-Type: application/json
- Request Body: 
    - **credit_report_text**: (required) The fixed-length credit report from the bureau.
    - **gross_monthly_income**: (optional) INT/FLOAT of income used to optionally calculate DTI
    - **outcome**: (optional) BIT 1/0 used in machine learning models to determine whether the record was "successful" or not. For example, in underwriting, credit reports associated with funded loans that did not default could be a 1 where those that were declined or funded and defaulted could be 0.
    - **format**: (oprtional) Specifies the output format of the summary. Valid values are 'analytics' (default) and 'ml'. 'ml' option will remove address.zip, standardize adress.state into address.state_bit_{n} where n = [1,2,3,4,5,6]. Normalizes score from range 300-850.
- Response:
    - for a full description of the fields see [Appendix C. Field Calculations and Descriptions](#c-field-calculations-and-descriptions)

#### Example request

```bash
curl -X POST "https://api.creditparsepro.io/v1/parse-report" \ 
     -H "X-API-KEY: yourKeyHere" \ 
     -H "Content-Type: application/json" \ 
     -d '{
           "gross_monthly_income": 5000,
           "outcome": 1,
           "format": "analytics",
           "credit_report_text": "Sample credit report text here... 
           feel free to use an example report that has been provided in the Appendix"
         }'
```

#### Example response 'analytics' format
```JSON
{
  "address": {
    "address_changes_per_year": 0.26,
    "change_count": 1,
    "months_at_current_address": 14.78,
    "state": "il",
    "zip": 60750
  },
  "age": 32,
  "date": "2024-02-29",
  "collections": {
    "count": 0
  },
  "delinquencies": {
    "past_due": {
      "open_count": 0,
      "open_sum": 0,
      "total_count": 0
    },
    "times_late": {
      "30_days_sum": 0,
      "60_days_sum": 0,
      "90_days_sum": 0
    }
  },
  "dti": 7.08,
  "employment": {
    "months_at_current_employer": 0
  },
  "inquiries": {
    "past_6_months_count": 2,
    "total_count": 2
  },
  "public_records": {
    "count": 0
  },
  "score": 696,
  "tradelines": {
    "credit": {
      "open_count": 0,
      "total_count": 0
    },
    "installment": {
      "installment_utilization_ratio": 57.57,
      "open_count": 2,
      "open_sum": 7592,
      "total_count": 2
    },
    "mortgage": {
      "open_count": 1,
      "total_count": 1
    },
    "overall": {
      "oldest_open_date_months": 349,
      "open_accounts": 6,
      "total_accounts": 6,
      "total_monthly_payments": 425
    },
    "revolving": {
      "open_count": 3,
      "open_sum": 15500,
      "revolving_utilization_ratio": 1.91,
      "total_count": 3
    }
  }
}
```

### Example response 'ml' format
```JSON
{
  "address": {
    "address_change_count_per_year_of_life": 0.0312,
    "address_changes_per_year_scaled": 0.0217,
    "state_bit_1": 0,
    "state_bit_2": 0,
    "state_bit_3": 1,
    "state_bit_4": 1,
    "state_bit_5": 0,
    "state_bit_6": 1
  },
  "age": 0.1707,
  "collections": {
    "collections_exist": 0,
    "normalized_count": 0
  },
  "date": "2024-02-29",
  "delinquencies": {
    "past_due": {
      "normalized_open_count_per_tradeline": 0,
      "normalized_past_due_open_sum": 0,
      "normalized_total_count_per_tradeline": 0
    },
    "times_late": {
      "normalized_30_days_per_tradeline": 0,
      "normalized_30_days_per_year": 0,
      "normalized_60_days_per_tradeline": 0,
      "normalized_60_days_per_year": 0,
      "normalized_90_days_per_tradeline": 0,
      "normalized_90_days_per_year": 0
    }
  },
  "dti": 0.0708,
  "employment": {
    "employment_stability_score": 1
  },
  "inquiries": {
    "normalized_total_count_per_year": 0.0688,
    "recent_inquiry_ratio": 1
  },
  "outcome": 1,
  "public_records": {
    "normalized_count": 0,
    "public_records_exist": 0
  },
  "score": 0.72,
  "tradelines": {
    "credit": {
      "normalized_open_count_per_total_tradelines": 0,
      "normalized_open_count_per_year": 0,
      "normalized_total_count_per_total_tradelines": 0,
      "normalized_total_count_per_year": 0
    },
    "installment": {
      "installment_utilization_ratio": 0.5757,
      "normalized_open_count_per_total_tradelines": 0.3333,
      "normalized_open_count_per_year": 0.0688,
      "normalized_total_count_per_total_tradelines": 0.3333,
      "normalized_total_count_per_year": 0.0688
    },
    "mortgage": {
      "normalized_open_count_per_total_tradelines": 0.1667,
      "normalized_open_count_per_year": 0.0344,
      "normalized_total_count_per_total_tradelines": 0.1667,
      "normalized_total_count_per_year": 0.0344
    },
    "overall": {
      "normalized_open_count_per_total_tradelines": 0,
      "normalized_open_count_per_year": 0,
      "normalized_total_count_per_total_tradelines": 0,
      "normalized_total_count_per_year": 0
    },
    "revolving": {
      "normalized_open_count_per_total_tradelines": 0.5,
      "normalized_open_count_per_year": 0.1032,
      "normalized_total_count_per_total_tradelines": 0.5,
      "normalized_total_count_per_year": 0.1032,
      "revolving_utilization_ratio": 0.0191
    }
  }
}
```

## Error Codes and Messages

creditparsepro.io API uses conventional HTTP response codes to indicate the success or failure of an API request. Here are some of the common codes:

- `200 OK` - The request was successful.
- `400 Bad Request` - The request was malformed. This could be due to a missing required parameter or a parameter with an invalid value.
- `401 Unauthorized` - The API key was missing or invalid.
- `403 Forbidden` - The request was valid, but you do not have the necessary permissions.
- `404 Not Found` - The requested resource does not exist.
- `500 Internal Server Error` - Likely an issue with the **credit_report_text** parameter formatting. Make sure the reports match the format in the [Appendix](#appendix).

## Rate Limiting and SLA

Rate limiting is carried out via monthly and per-minute quotas. They are determined by the count of successful requests in that time period. The limits are determined based on your product tier.

- monthly quota
    - test: 100
    - basic: 10,000 
    - professional: 100,000
    - enterprise: Unlimited

- per-minute rate limit
    - test: 5
    - basic: 30
    - professional: 60 
    - enterprise: 150

All production endpoints (api.creditparsepro.io) regardless of tier offer 99.95% SLA.

In the case that there are multiple open requests from customers, the requests will be prioritized by the product tier.

## Feature Roadmap

COMING SOON!

## Support

For support and queries or feedback, please contact us at info@creditparsepro.io.

## Appendix

### A. Experian AFR Example Report

Please note that the example reports provided are **NOT** real credit reports.  
They are example reports used by the bureaus and contain **NO PII**.

Experian
```
1100028022924144736TTXA0700@13000230670P10113033AG@3220018*666048258@335004216/JOE/M/EARNEST//1928E61208161928@335004324/JOSEPH/MARCEL/EARNEST//    E105N@3360078080609232163182310S        41/1101/CORRAL/ST///SWEETWATER/TX/795566611@336007304230423600                36/CORRAL COVE/////SWEETWATER/TX/79556@337008608130813223SIEMENS STROMBERG CARLS15400 RINEHART RD12LAKE MARY FL01 32746     @357018931N06221023    07REV100000600L00000023H100323        11          CR0001 A913117600189B2141600000000B420B00000000000000CB520          071222B6261389998DC11THE BON TONF316102305110740@3570185  P01210223    26360100067400O         020723        05          CI0001 A9118005758B2142300000000B427BCCCCCCCCCCCCCCCCCCCCCCB6372991785FM22PRINCIPAL RESIDENTL MTF3160223051126  @357016619N04971022    15REV100003000L00002048H101122        12          CR0001 A9082830B2149900000000B429B000000000000000000000000B6191102240BB04BANKF3161022A2111519@357018418N04021221    18REV100003200L         121621        12          CR0001 A916542418054042B2149900000000B429B-------------00-000-----B6291240000BC14CITICARDS CBNAF3161221A2111818@357018419N09051221    18REV100000000L         121521        12          CR0001 A916542418053826B2149900000000B429B--------------000-----00B6291240000BC14CITICARDS CBNAF3161221A2111819@357018419N10040621    18REV100005400L00004885H061321        12          CR0001 A916545715001233B2148500000000B429B000000CC00000000CCCC000CB6293278165BC14CITICARDS CBNAF3160621A2111819@357016519N08010920    18REV100000800L00000025H091120        12          CR0001 A9147791556597B2141200000000B416B000000000C0B6251232920BC10SHELL/CBNAF3160920A2111819@357018319N05040520    18REV200007500L00004569H051320        12          CR0001 A916601100462050B2142900000000B429B000000000CCCCCCCCCCCCCCCB6283276502BC13DISCOVER BANKF3160520A2111819@357016519N04970320    15REV100003000L00002048H031120        12          CR0001 A907383B2142500000000B429BCCCCCCCCCCCCCCCCCCCCCCCCB6191102240BB04BANKF3160320A2111519@357018118N11950519    18REV100002831H         051319        12          CR0001 A916529107125292B2149900000000B429BCCCCCCCCCCCCCCCCCCCCCCCCB6261270246BC11CAPITAL ONEF3160519A2111818@3570180  P11130515    27014200032000O         052815        12          CI0001 A9149590103426B2142000000000B423BCCCCCCCC---CCCCCCCB6332184720BB18HOME LOAN SERVICESF3160515A21127  @3570197  P05931223    07REV100000200L00000959H1225230000000011          OR0001 A9141687725307B2149900000000B4290000000000000000000000000B520          121714B6243321860DC09SYNCB/JCPF3161223A11107  @3570204  P05011223    18REV200010200L00010389H1222230001038911          OR0001 A9204118160281358112B2147400000000B429CCCCCCCCCCCCCCCCCCCCCCCCCB52000000273S 110923B6253182310BC10JPMCB CARDF3161223A11118  @3570191  P09221223    07REV100002150L00000037H1217230000000011          OR0001 A916504994014753B2141600000000B420000000000000000CB520          092822B6251323180DC10SEARS/CBNAF3161223A11107  @3570197  P11861223    18REV200005200L00013887H1216230000539811          OR0001 A9087264B2146600000000B429CCCCCCCCCCCCCCCCCCCCCCCCCB52000000171S 110523B6301230206BC15BANK OF AMERICAF3161223A11118  @3570205  P07951223    18REV100008500L00008398H1214230000838311          OR0001 A916433600615056B2144800000000B429CCCCCCCCCCCCCCCCCCCCCCCCCB52000000132S 120623B6303202754BC15BANK OF AMERICAF3161223A11118  @3570197  P05011223    18REV200011400L00011330H1211230001131311          OR0001 A9084394B2149000000000B429CCCCCCCCCCCCCCCCCCCCCCCCCB52000000343S 120623B6301213727BC15BANK OF AMERICAF3161223A11118  @3570204  P05031223    18REV100008000L00007635H1210230000746011          OR0001 A9205323510002673205B2149900000000B429CCCCCCCCCCCCCCCCCCCCCCCCCB52000000149S 120623B6251240338BC10JPMCB CARDF3161223A11118  @3570202  P11041223    18REV100005000L00005029H1209230000490211          OR0001 A919324131017164644B2149900000000B429CCCCCCCCCCCCCCCCCCCCCC000B52000000132S 120523B6240203010BC09FNB OMAHAF3161223A11118  @3570204  P11911223    18REV100015000L00014669H1205230001111811          OR0001 A9205121071814310177B2149900000000B429CCCCCCCCCCCCCCCCCCCCCCCCCB52000000232S 120223B6251230750BC10SEARS/CBSDF3161223A11118  @3570187  P12201223    26360100067400O         1205230005491011          OI0001 A9118005758B2141100000000B415CCCCCCCCCCCB52000000595S       B6312570635FM16CITIMORTGAGE INCF3161223A11126  @3570181  P07231223    18REV100001000L00000018H1203230000000011          OR0001 A916042378879907B2140500000000B4090CCCCB520          081123B6262310220DC11KOHLS/CHASEF3161223A11118  @3570199  P12201123    18REV100003500L00003509H1128230000349711          OR0001 A9140007161206B2143600000000B429CCCCCCCC-0000000000000000B52000000121S 110423B6263279024BC11CAPITAL ONEF3161123A11118  @3570188  P04211221    07REV100000118L00000118H1201210000000011          OR0001 A913211478102B2140800000000B4120000000CB520          050721B6331362760ZR18BOSCOVS DEPT STOREF3161221A11107  @3590050081123 UNKNOWN31UNKB6231219240BC08INFIBANK@3590053070823 UNKNOWN31UNKB6261352920DC11KOHLS/CHASE@3590062102722 UNKNOWN31UNKB6351252660AU20700 CREDIT/AA MOTORS@3590063090422 UNKNOWN31UNKB6361352085DC21COMPLETE DEPT. STORES@361005457420335 AG08TOO MANY INQUIRIES LAST 12 MONTHS@361003757251202 OFAC NO RECORD FOUND@361003657241204 MLA NO RECORD FOUND@8500101000000N/A     00054910000624600000000000001553 00000595 011 004001024011024000000118600000000@950001604105385@
```

### B. TransUnion 4.0 FFR Example Report

Please note that the example reports provided are **NOT** real credit reports.  
They are example reports used by the bureaus and contain **NO PII**.

TransUnion
```
TU4R062011                        1614F 0459317220240229143215PH0101207000SH01027101Y05N03PEN20210602NM01070F1DAY                      SUNNY                               PI01029F66688567819910601    AD01105F11333         HOPP                         CT     FANTASY ISLAND             IL60750     20221206AD01105F111233      S CARROT                       ST     FANTASY ISLAND             IL60750     20200408EM01100ASDF                               F                                      20240110V          EM01100DEFI SLUTIONS                      FDEVELOPER                             20240110V          TR01288Q 0202V002WLM P & F CU            I44009                   I2020042620240101V                         051000003817000006587         034M000000242                                    US            00         2024010105                                                        00       TR01288B 041PF002FST PREMIER             R38294                   I2022060120240101V                         011000000184000000414000007500                                                               00                   20231201111111111X11                                    120000002TR01288B 09616003DISCOVERBANK            R4                       I2012042520240101V                         011000000093000000093000008000MIN 000000010                                    CC            00                   2023120111111111111111111111111111111                   290000002TR01288Q 06262001PROVDENT FCU            I75500045                I2020100420240101V                         011000000554000001005                                                                        00                   202312011111111111111111111111111                       250000002TR01288B 0848R015WILM TRUST              M698007                  I1995013120240101V                         011000003327000036500         300M000000163                                    RE            00                   20231201111111111111111111111111                        240000002TR01288D 0160Q001BOSCOVS                 R1                       I2007121020231201V                         011000000019000000272         MIN 000000010                                                  00                   202311011XXXXX111111XX1XXX111X1XXXXXXXXXXXX111111XX1X11 470000002TM01040000000000001000000000005000000000IN0106516ORF 04593172NEEDHAM/RECF            I           20240229IN0106540PEY 02462756MIDLAND CRED            I           20240113OB01148TRANSUNION TEST FACILITY                          555 W ADAMS                             CHICAGO, IL 60661            800-888-4213          AO0101700Q8804   SC0103400Q88+696    039013027018  AO010170680004O01AO010170705101M00ENDS010024
```

### C. Field Calculations and Descriptions

COMING SOON!

### D. Pricing & Plans

Please note that this section can become out-of-date and is to serve only as a reference. For accurate pricing and product details visit our website pricing page [creditparsepro.io/pricing](https://www.creditparsepro.io/pricing),

#### Test

Explore the capabilities of CreditParsePro.io with our free Test tier, designed for initial testing and development with limited monthly requests and a dedicated test environment.

- Price: Free
- Monthly Quota: 100 requests
- Rate Limit: 5 requests per minute
- Endpoints: Access to test endpoint
- SLA: N/A
- Response Time: Low (3+ days)
- Features: Basic access for testing and development.

#### Basic

Ideal for small projects and startups, the Basic tier offers an increased quota and rate limit, plus a 99.95% SLA guarantee, ensuring reliable access to our production API.

- Price: $20/month or $200/year
- Monthly Quota: 10,000 requests
- Rate Limit: 30 requests per minute
- Endpoints: Test and production endpoints
- SLA: 99.95%
- Response Time: Medium (1-3 days)
- Features: Ideal for small projects and startups.

#### Professional

Tailored for growing businesses, the Professional tier boosts your monthly quota and rate limit significantly, includes feature request privileges, and maintains our 99.95% SLA with faster response times.

- Price: $100/month or $1,000/year
- Monthly Quota: 100,000 requests
- Rate Limit: 60 requests per minute
- Endpoints: Test and production endpoints
- SLA: 99.95%
- Response Time: High (<1 day)
- Features: Includes feature requests, suitable for growing businesses.

#### Enterprise

Our Enterprise tier is designed for large-scale operations requiring the highest level of service, including unlimited access, the fastest response times, the ability to make feature requests, and personalized custom services to meet your needs.

- Price: $250/month or $2,500/year
- Monthly Quota: Unlimited
- Rate Limit: 150 requests per minute
- Endpoints: Test and production endpoints
- SLA: 99.95%
- Response Time: Critical (<1 hour)
- Features: Includes feature requests and custom services such as integrations.