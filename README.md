    {
  "name": "Ultimate Lnkdn email finder",
  "nodes": [
      {
        "parameters": {
        "method": "POST",
        "url": "https://api.apify.com/v2/acts/2SyF0bVxmgGr8IVCZ/run-sync-get-dataset-items",
        "sendHeaders": true,
        "headerParameters": {
          "parameters": {
              "name": "Accept",
              "value": "application/json"
            },
            {
              "name": "Authorization",
              "value": "Bearer XXXXXXXXXXXXXXXXXXXXXXXXX"
            }
          ]
        },
        "sendBody": true,
        "specifyBody": "json",
        "jsonBody": "={\n    \"profileUrls\": [\n        \"{{ $('Scraped Leads Data').item.json['Linkedin URL'] }}\"\n    ]\n}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        240,
        120
      ],
      "id": "5e686c3f-ee54-4c07-9b24-498832ad824a",
      "name": "HTTP Request2"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.splitInBatches",
      "typeVersion": 3,
      "position": [
        20,
        100
      ],
      "id": "065a8e24-1dbb-4e03-82fa-4c121d126b79",
      "name": "Loop Over Items"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "8b0c89ca-b86f-4129-9a30-cf77e7097402",
              "name": "Full Name",
              "value": "={{ $json.fullName }}",
              "type": "string"
            },
            {
              "id": "efa1897b-da30-4bc1-bd00-3481b7992b30",
              "name": "Email",
              "value": "={{ $json.email }}",
              "type": "string"
            },
            {
              "id": "9080e0a4-db15-4457-8d42-92eb8b98d2e5",
              "name": "Company Name",
              "value": "={{ $json.companyName }}",
              "type": "string"
            },
            {
              "id": "0a3d7d55-c3c6-465a-b932-e6b1b23d53df",
              "name": "Company Website",
              "value": "={{ $json.companyWebsite }}",
              "type": "string"
            },
            {
              "id": "b949ff8c-d54c-4b63-9ca6-eb72ac6f9a6e",
              "name": "Role ",
              "value": "={{ $json.experiences[0].title }}",
              "type": "string"
            },
            {
              "id": "ee0d838d-e2d7-47c5-afd9-014cf00b1297",
              "name": "Company Industry",
              "value": "={{ $json.companyIndustry }}",
              "type": "string"
            },
            {
              "id": "f62e4489-3af5-414e-a7eb-b3bf51e0cfdc",
              "name": "Loaction",
              "value": "={{ $json.addressWithCountry }}",
              "type": "string"
            },
            {
              "id": "3fd38f3f-db6b-4ccc-9aa0-06ad9393258f",
              "name": "linkedinUrl",
              "value": "={{ $json.linkedinUrl }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        440,
        120
      ],
      "id": "993d1746-bcc3-4960-864e-85c29b35d238",
      "name": "Edit Fields"
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict",
            "version": 2
          },
          "conditions": [
            {
              "id": "04d0bbba-615a-48d0-9391-93707d995f6f",
              "leftValue": "={{ $json.Email }}",
              "rightValue": "",
              "operator": {
                "type": "string",
                "operation": "exists",
                "singleValue": true
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.2,
      "position": [
        80,
        360
      ],
      "id": "5b64c909-c0f4-4d74-92dd-e0317860b325",
      "name": "If"
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict",
            "version": 2
          },
          "conditions": [
            {
              "id": "123e70cc-ba68-4d07-8d44-760d410a670e",
              "leftValue": "={{ $json['Company Website'] }}",
              "rightValue": "",
              "operator": {
                "type": "string",
                "operation": "exists",
                "singleValue": true
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.2,
      "position": [
        320,
        600
      ],
      "id": "3872d4b9-7090-47ab-b3df-20e73ecac188",
      "name": "If1"
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "loose",
            "version": 2
          },
          "conditions": [
            {
              "id": "06110187-014e-484a-a264-513f18a5098f",
              "leftValue": "={{ $json.emails }}",
              "rightValue": 0,
              "operator": {
                "type": "string",
                "operation": "notExists",
                "singleValue": true
              }
            },
            {
              "id": "aff917a0-9717-460b-89d6-492d435b3b82",
              "leftValue": "={{ $json.emails }}",
              "rightValue": "NIL",
              "operator": {
                "type": "string",
                "operation": "equals",
                "name": "filter.operator.equals"
              }
            }
          ],
          "combinator": "or"
        },
        "looseTypeValidation": true,
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.2,
      "position": [
        980,
        360
      ],
      "id": "023d9722-4e1d-49f2-bdab-e54c35defe95",
      "name": "If2"
    },
    {
      "parameters": {},
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [
        520,
        340
      ],
      "id": "1306657f-f056-42ae-a3e0-7a7a5c85bf2d",
      "name": "Wait",
      "webhookId": "445a3682-b83c-4573-bfbf-465933f8ba2b"
    },
    {
      "parameters": {},
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [
        1440,
        340
      ],
      "id": "51d0115d-05ce-4182-be74-2de9b6a9df7a",
      "name": "Wait3",
      "webhookId": "445a3682-b83c-4573-bfbf-465933f8ba2b"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkdin Outreach (solar)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 1453550326,
          "mode": "list",
          "cachedResultName": "Scraped Leads - Google",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit#gid=1453550326"
        },
        "filtersUI": {
          "values": [
            {
              "lookupColumn": "Customer",
              "lookupValue": "Ideal"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [
        -180,
        100
      ],
      "id": "2620ea27-0c8a-4799-b97b-7c6cba784609",
      "name": "Scraped Leads Data",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkdin Outreach (solar)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 1763230603,
          "mode": "list",
          "cachedResultName": "Emails Enriched",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit#gid=1763230603"
        },
        "columns": {
          "mappingMode": "autoMapInputData",
          "value": {},
          "matchingColumns": [
            "row_number"
          ],
          "schema": [
            {
              "id": "Full Name",
              "displayName": "Full Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Email",
              "displayName": "Email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Company Name",
              "displayName": "Company Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Company Website",
              "displayName": "Company Website",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Role ",
              "displayName": "Role ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Company Industry",
              "displayName": "Company Industry",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Loaction",
              "displayName": "Loaction",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "linkedinUrl",
              "displayName": "linkedinUrl",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [
        320,
        340
      ],
      "id": "4d895789-0539-4f4a-aca7-9044f77d90cc",
      "name": "Enriched Emails",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkdin Outreach (solar)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 1453550326,
          "mode": "list",
          "cachedResultName": "Scraped Leads - Google",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit#gid=1453550326"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "row_number": "={{ $('Loop Over Items').first().json.row_number }}",
            "Status": "Enriched",
            "Customer": "Lead sent"
          },
          "matchingColumns": [
            "row_number"
          ],
          "schema": [
            {
              "id": "Name",
              "displayName": "Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Role",
              "displayName": "Role",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Linkedin URL",
              "displayName": "Linkedin URL",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "More info",
              "displayName": "More info",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Profile photo",
              "displayName": "Profile photo",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Enriched",
              "displayName": "Enriched",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Company Name",
              "displayName": "Company Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Location",
              "displayName": "Location",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Customer",
              "displayName": "Customer",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Status",
              "displayName": "Status",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "row_number",
              "displayName": "row_number",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "readOnly": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [
        720,
        340
      ],
      "id": "23238740-df33-4caa-8014-a0edcaa8a7e2",
      "name": "Update status",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkdin Outreach (solar)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 763831104,
          "mode": "list",
          "cachedResultName": "Left Lindin profiles",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit#gid=763831104"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Full Name": "={{ $('Edit Fields').first().json['Full Name'] }}",
            "Email": "={{ $('Edit Fields').first().json['Company Name'] }}",
            "Company Name": "={{ $('Edit Fields').first().json['Company Name'] }}",
            "Company Website": "={{ $('Edit Fields').first().json['Company Website'] }}",
            "Role": "={{ $('Edit Fields').first().json['Role '] }}",
            "Company Industry": "={{ $('Edit Fields').first().json['Company Industry'] }}",
            "Location": "={{ $('Edit Fields').first().json.Loaction }}",
            "Lindin URL": "={{ $('Edit Fields').first().json.linkedinUrl }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "Lindin URL",
              "displayName": "Lindin URL",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Full Name",
              "displayName": "Full Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Role",
              "displayName": "Role",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Company Name",
              "displayName": "Company Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Company Industry",
              "displayName": "Company Industry",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Location",
              "displayName": "Location",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Company Website",
              "displayName": "Company Website",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Email",
              "displayName": "Email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [
        700,
        820
      ],
      "id": "a1c4a41e-15d6-4669-bd01-99ba972f4a5b",
      "name": "No data found1",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkdin Outreach (solar)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 1453550326,
          "mode": "list",
          "cachedResultName": "Scraped Leads - Google",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit#gid=1453550326"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "row_number": "={{ $('Loop Over Items').first().json.row_number }}",
            "Status": "Not Found",
            "Customer": "Lead sent"
          },
          "matchingColumns": [
            "row_number"
          ],
          "schema": [
            {
              "id": "Name",
              "displayName": "Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Role",
              "displayName": "Role",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Linkedin URL",
              "displayName": "Linkedin URL",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "More info",
              "displayName": "More info",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Profile photo",
              "displayName": "Profile photo",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Enriched",
              "displayName": "Enriched",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Company Name",
              "displayName": "Company Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Location",
              "displayName": "Location",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Customer",
              "displayName": "Customer",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Status",
              "displayName": "Status",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "row_number",
              "displayName": "row_number",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "readOnly": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [
        1660,
        340
      ],
      "id": "49403bfa-29eb-4c8c-8976-6a2dfef99208",
      "name": "Update status2",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
    },
    {
      "parameters": {},
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [
        900,
        820
      ],
      "id": "3734e213-7053-4f14-bedd-2fee6e639a44",
      "name": "Wait4",
      "webhookId": "445a3682-b83c-4573-bfbf-465933f8ba2b"
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkdin Outreach (solar)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 1453550326,
          "mode": "list",
          "cachedResultName": "Scraped Leads - Google",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit#gid=1453550326"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "row_number": "={{ $('Loop Over Items').first().json.row_number }}",
            "Status": "Not Found",
            "Customer": "Lead sent"
          },
          "matchingColumns": [
            "row_number"
          ],
          "schema": [
            {
              "id": "Name",
              "displayName": "Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Role",
              "displayName": "Role",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Linkedin URL",
              "displayName": "Linkedin URL",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "More info",
              "displayName": "More info",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Profile photo",
              "displayName": "Profile photo",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Enriched",
              "displayName": "Enriched",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Company Name",
              "displayName": "Company Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Location",
              "displayName": "Location",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Customer",
              "displayName": "Customer",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Status",
              "displayName": "Status",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "row_number",
              "displayName": "row_number",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "readOnly": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [
        1120,
        820
      ],
      "id": "7f226eb1-322c-4de5-9df2-f7d2138dd61e",
      "name": "Update status3",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkdin Outreach (solar)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 763831104,
          "mode": "list",
          "cachedResultName": "Left Lindin profiles",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit#gid=763831104"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Full Name": "={{ $('Edit Fields').first().json['Full Name'] }}",
            "Email": "={{ $json.Email }}",
            "Company Name": "={{ $('Edit Fields').first().json['Company Name'] }}",
            "Company Website": "={{ $('Edit Fields').first().json['Company Website'] }}",
            "Role": "={{ $('Edit Fields').first().json['Role '] }}",
            "Company Industry": "={{ $('Edit Fields').first().json['Company Industry'] }}",
            "Location": "={{ $('Edit Fields').first().json.Loaction }}",
            "Lindin URL": "={{ $('Edit Fields').first().json.linkedinUrl }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "Lindin URL",
              "displayName": "Lindin URL",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Full Name",
              "displayName": "Full Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Role",
              "displayName": "Role",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Company Name",
              "displayName": "Company Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Company Industry",
              "displayName": "Company Industry",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Location",
              "displayName": "Location",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Company Website",
              "displayName": "Company Website",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Email",
              "displayName": "Email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [
        1220,
        340
      ],
      "id": "764fff59-2c3d-4a47-a3b2-1eef6675203f",
      "name": "No data found",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "const excludeRegex = /(google|gstatic|ggpht|schema\\.org|example\\.com|sentry\\.wixpress\\.com|sentry-next\\.wixpress\\.com|ingest\\.sentry\\.io|sentry\\.io|imli\\.com|test@|example@|\\.webp|\\.svg)/i;\n\nreturn items.map(item => {\n  const input = item.json;\n  \n  // Clean emails\n  const emails = input.emails || [];\n  const cleanedEmails = emails.filter(email => !excludeRegex.test(email));\n  const finalEmails = cleanedEmails.length > 0 ? cleanedEmails.join(', ') : \"NIL\";\n  \n  return {\n    json: {\n      emails: finalEmails\n    }\n  };\n});"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1020,
        580
      ],
      "id": "8e333cdd-62c7-498b-8cf0-d6b61e011704",
      "name": "Code3"
    },
    {
      "parameters": {
        "url": "=https://{{ $json['Company Website'] }}",
        "options": {}
      },
      "id": "bb6d67e5-2b0b-4d7d-89c8-9f770d31a27b",
      "name": "HTTP Request1",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        580,
        580
      ],
      "onError": "continueRegularOutput"
    },
    {
      "parameters": {
        "jsCode": "\n// Main processing code\nconst pageHTML = $json.data;\n\n// Extract emails\nconst emailRegex = /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.(?!png|jpg|gif|jpeg)[a-zA-Z]{2,}/g;\nconst emails = pageHTML.match(emailRegex) || [];\nconst uniqueEmails = [...new Set(emails)];\n\n// Return the result in n8n format\nreturn {\n  json: {\n    emails: uniqueEmails\n  }\n};"
      },
      "id": "593600bf-27bc-4e3e-8444-df0627f2c505",
      "name": "Code1",
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        800,
        580
      ],
      "onError": "continueRegularOutput"
    },
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        -200,
        -120
      ],
      "id": "66fa661d-9fd6-4287-8e10-bf8da36912fc",
      "name": "When clicking ‘Test workflow’"
    },
    {
      "parameters": {},
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [
        1440,
        580
      ],
      "id": "967d0f62-9db9-493c-80df-e79a7778a1e2",
      "name": "Wait6",
      "webhookId": "445a3682-b83c-4573-bfbf-465933f8ba2b"
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkdin Outreach (solar)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 1453550326,
          "mode": "list",
          "cachedResultName": "Scraped Leads - Google",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit#gid=1453550326"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "row_number": "={{ $('Loop Over Items').first().json.row_number }}",
            "Status": "Enriched",
            "Customer": "Lead sent"
          },
          "matchingColumns": [
            "row_number"
          ],
          "schema": [
            {
              "id": "Name",
              "displayName": "Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Role",
              "displayName": "Role",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Linkedin URL",
              "displayName": "Linkedin URL",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "More info",
              "displayName": "More info",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Profile photo",
              "displayName": "Profile photo",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Enriched",
              "displayName": "Enriched",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Company Name",
              "displayName": "Company Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Location",
              "displayName": "Location",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Customer",
              "displayName": "Customer",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Status",
              "displayName": "Status",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "row_number",
              "displayName": "row_number",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "readOnly": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [
        1660,
        580
      ],
      "id": "925a730e-13e8-4e30-b277-04aad846411e",
      "name": "Update status5",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkdin Outreach (solar)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 990024898,
          "mode": "list",
          "cachedResultName": "Emails Enriched - Domain",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit#gid=990024898"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Full Name": "={{ $('Edit Fields').first().json['Full Name'] }}",
            "Company Name": "={{ $('Edit Fields').first().json['Company Name'] }}",
            "Company Website": "={{ $('Edit Fields').first().json['Company Website'] }}",
            "Company Industry": "={{ $('Edit Fields').first().json['Company Industry'] }}",
            "Location": "={{ $('Edit Fields').first().json.Loaction }}",
            "linkedinUrl": "={{ $('Edit Fields').first().json.Loaction }}",
            "Role ": "={{ $('Edit Fields').first().json['Role'] }}",
            "Email 1": "={{ $json.emails.split(',')[0].trim() }}",
            "Rest Emails": "={{ $json.emails.split(',').slice(1).join(',') }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "Full Name",
              "displayName": "Full Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Company Name",
              "displayName": "Company Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Company Website",
              "displayName": "Company Website",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Role ",
              "displayName": "Role ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Company Industry",
              "displayName": "Company Industry",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Location",
              "displayName": "Location",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "linkedinUrl",
              "displayName": "linkedinUrl",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Email 1",
              "displayName": "Email 1",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Rest Emails",
              "displayName": "Rest Emails",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [
        1220,
        580
      ],
      "id": "add4436f-52f3-41f4-b91e-48d3d8dbedad",
      "name": "Email found",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
    },
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "triggerAtHour": 9
            }
          ]
        }
      },
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1.2,
      "position": [
        -200,
        280
      ],
      "id": "83ccd05c-532b-4511-87aa-8c563ca11382",
      "name": "Schedule Trigger"
    }
  ],
  "pinData": {
    "When clicking ‘Test workflow’": [
      {
        "json": {}
      }
    ]
  },
  "connections": {
    "HTTP Request2": {
      "main": [
        [
          {
            "node": "Edit Fields",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Loop Over Items": {
      "main": [
        [],
        [
          {
            "node": "HTTP Request2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Edit Fields": {
      "main": [
        [
          {
            "node": "If",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "If": {
      "main": [
        [
          {
            "node": "Enriched Emails",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "If1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "If1": {
      "main": [
        [
          {
            "node": "HTTP Request1",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "No data found1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "If2": {
      "main": [
        [
          {
            "node": "No data found",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Email found",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Wait": {
      "main": [
        [
          {
            "node": "Update status",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Wait3": {
      "main": [
        [
          {
            "node": "Update status2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Scraped Leads Data": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Enriched Emails": {
      "main": [
        [
          {
            "node": "Wait",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Update status": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "No data found1": {
      "main": [
        [
          {
            "node": "Wait4",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Update status2": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Wait4": {
      "main": [
        [
          {
            "node": "Update status3",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Update status3": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "No data found": {
      "main": [
        [
          {
            "node": "Wait3",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTTP Request1": {
      "main": [
        [
          {
            "node": "Code1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Code1": {
      "main": [
        [
          {
            "node": "Code3",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Code3": {
      "main": [
        [
          {
            "node": "If2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "When clicking ‘Test workflow’": {
      "main": [
        [
          {
            "node": "Scraped Leads Data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Wait6": {
      "main": [
        [
          {
            "node": "Update status5",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Update status5": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Email found": {
      "main": [
        [
          {
            "node": "Wait6",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "Scraped Leads Data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "bef96faf-cab1-4e26-ad13-8ecf06dad0ba",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "77f1d8375380ee2bc4995763b4e39528bf040d446fc3e9e5f6d802ec19784049"
  },
  "id": "SwqFYHi6Grx7xvwV",
  "tags": []
}      
