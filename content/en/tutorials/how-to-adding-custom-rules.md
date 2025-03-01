---
title: How to add custom rules on Horusec-CLI?
weight: 10
description: In this section, you will find how to add custom rules to Horusec.
---

---

You are able to dynamically add custom rules that will be executed in the Horusec's engines. 

## **How can you do it?** 

Follow the steps below to configure the custom rules and add them to Horusec: 


## **Step 1. Create a customized rules JSON file** 

In order to run custom JSON rules in Horusec, you'll have to create a **.json** with the default code below:


```json
[
  {
     "id": "uuid v4 aleatory",
     "name": "Vulnerability Name",
     "description": "Description of the vulnerability with CWE link",
     "language": "Vulnerability language choice one into: C#, Dart, Java, Kotlin, YAML, Leaks, JavaScript, Nginx",
     "severity": "Vulnerability severity choice one into: CRITICAL, HIGH, MEDIUM, LOW, UNKNOWN, INFO",
     "confidence": "Vulnerability confidence choice one into: HIGH, MEDIUM, LOW",
     "type": "Vulnerability math type choice one into: Regular, OrMatch, AndMatch, NotMatch",
     "expressions": [
        "Regex to respective found vulnerability"
     ]
  },
  {
     "id": "837c504d-38b4-4ea6-987b-d91e92ac86a2",
     "name": "Cookie Without HttpOnly Flag",
     "description": "It is recommended to specify the HttpOnly flag to new cookie. For more information access: (https://security-code-scan.github.io/#SCS0009) or (https://cwe.mitre.org/data/definitions/1004.html).",
     "language": "C#",
     "severity": "MEDIUM",
     "confidence": "LOW",
     "type": "OrMatch",
     "expressions": [
          "httpOnlyCookies\\s*=\\s*['|\"]false['|\"]",
"(new\\sHttpCookie\\(.*\\))(.*|\n)*(\\.HttpOnly\\s*=\\s*false)",
"(new\\sHttpCookie)(([^H]|H[^t]|Ht[^t]|Htt[^p]|Http[^O]|HttpO[^n]|HttpOn[^l]|HttpOnl[^y])*)(})"
     ]
  }
]

```

## **Step 2. Define JSON's attributes**

Check the following table to get to know more about each JSON's field:  


| **Field** | Type | **Description** |
| :--- | :--- | :--- |
| ID |  | Random UUID used to identify the vulnerability in your code. Your rules should not duplicate this ID. |
| Name |  | The name of the vulnerability. |
| Description | String | The description of the vulnerability. |
Language    | String | It shows the engine's language that it will be executed in the vulnerabilities analysis, it can be: C#, Dart, Java, Kotlin, YAML, Leaks, JavaScript, Nginx. |
| Severity | String | The severity of the vulnerability with its possible values: \(INFO, AUDIT, LOW, MEDIUM, HIGH\). |
| Confidence | String | The confidence of the vulnerability report with its possible values: \(LOW, MEDIUM, HIGH\). |
| Type | String | Regex type containing these possible values: Regular, OrMatch, AndMatch. |
| Tool | String | Regex type containing these possible values: HorusecCsharp, HorusecJava, HorusecKotlin, HorusecKubernetes, HorusecLeaks, HorusecNodejs. |
| Expressions | Array | Array of string containing all the RegExps that will detect the vulnerability.   |

## **Step 3. Set the RegExps types**

Horusec's engine works with three types of RegExps: 

| **Type** | **Description** |
| :--- | :--- |
| OrMatch | These are more comprehensive rules, which may have more than one pattern to manifest, hence the name, since our engine will perform the logical OR operation for each of the registered RegExps. |
| Regular | It is very similar to OrMatch, but the idea is that it contains multiple ways to detect the same pattern. |
| AndMatch | These are rules that need the file to manifest multiple patterns to be considered something to be reported, therefore, the engine performs the logical operation in each of the registered RegExps to ensure that all conditions have been met. |  
NotMatch | These are rules that require the file to manifest no default and with that it can be considered something to report. However, the engine performs the logical operation in each registered RegExps, to make sure the all conditions were not found. |

## **Step 4.  Apply customized rules flag**

To start using the rules you've created, apply the **-c flag** so you can pass the path to your **.json** file. See the example: 

```bash
horusec start -c="{path to your horusec custom rules json file}"
```


```bash
horusec start -p="./" -c="./custom-rules.json"
```