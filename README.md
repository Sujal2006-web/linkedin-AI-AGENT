{
  "name": "Email verifier (Reoon)",
  "nodes": [
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        -1600,
        -120
      ],
      "id": "6bdb0ed8-55cf-4bb7-bfb4-ec18a32cb1b0",
      "name": "When clicking ‘Execute workflow’"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.splitInBatches",
      "typeVersion": 3,
      "position": [
        -1640,
        140
      ],
      "id": "5e356a47-3122-476c-b1f4-5d22a685ad40",
      "name": "Loop Over Items1"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "c71ab82b-fef3-48f7-999f-7b0ca0cfbe06",
              "name": "row_number",
              "value": "={{ $json.row_number }}",
              "type": "string"
            },
            {
              "id": "cd25916d-1c57-49c5-8bcb-3e1a558cdb1e",
              "name": "Email 1",
              "value": "={{ $json.Email }}",
              "type": "string"
            },
            {
              "id": "1f7c6661-6a5c-4556-ab36-125e7dd39bab",
              "name": "Company info",
              "value": "={{ $json['Company Name'] }}",
              "type": "string"
            },
            {
              "id": "107a03df-450e-4d4d-ae8a-52fb674beb38",
              "name": "Kay",
              "value": "aVHPtWGyw44wrQVgKP8dzBThlvXxqZI3",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -840,
        -120
      ],
      "id": "fef17475-931b-4f73-963b-d24e3941d948",
      "name": "Edit Fields"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkedin Scraping - Solar (N8N) (start)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 1763230603,
          "mode": "list",
          "cachedResultName": "Emails Enriched",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs/edit#gid=1763230603"
        },
        "filtersUI": {
          "values": [
            {
              "lookupColumn": "Verified",
              "lookupValue": "NA"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.6,
      "position": [
        -1200,
        -120
      ],
      "id": "9bf60e2c-2a3d-4700-a862-62634b79c947",
      "name": "Google Sheets5",
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
          "cachedResultName": "Linkedin Scraping - Solar (N8N) (start)",
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
          "mappingMode": "defineBelow",
          "value": {
            "row_number": "={{ $('Loop Over Items1').item.json.row_number }}",
            "Verified": "Risky"
          },
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
              "removed": true
            },
            {
              "id": "Email",
              "displayName": "Email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Verified",
              "displayName": "Verified",
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
              "removed": true
            },
            {
              "id": "linkedinUrl",
              "displayName": "linkedinUrl",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Company Website",
              "displayName": "Company Website",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Loaction",
              "displayName": "Loaction",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Role ",
              "displayName": "Role ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
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
      "typeVersion": 4.6,
      "position": [
        -540,
        360
      ],
      "id": "07601378-229d-41ca-916c-d4147d3cdf27",
      "name": "Google Sheets7",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "784b4f97-a497-464c-8e5c-9fef33d16b79",
              "name": "Email 1",
              "value": "={{ $json['Email 1'] }}",
              "type": "string"
            },
            {
              "id": "57927afb-eb1e-442e-bda4-faf43cda8631",
              "name": "row_number",
              "value": "={{ $json.row_number }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -1380,
        160
      ],
      "id": "3ea717a0-3bc7-4038-a0cd-b75f1d0c3390",
      "name": "Edit Fields1"
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "value": "1hPaRoR-JZcldS_gfTm3_o146iNc9nKQF4l_V-svQ6qs",
          "mode": "list",
          "cachedResultName": "Linkedin Scraping - Solar (N8N) (start)",
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
          "mappingMode": "defineBelow",
          "value": {
            "row_number": "={{ $('Loop Over Items1').item.json.row_number }}",
            "Verified": "Verified"
          },
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
              "removed": true
            },
            {
              "id": "Email",
              "displayName": "Email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Verified",
              "displayName": "Verified",
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
              "removed": true
            },
            {
              "id": "linkedinUrl",
              "displayName": "linkedinUrl",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Company Website",
              "displayName": "Company Website",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Loaction",
              "displayName": "Loaction",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Role ",
              "displayName": "Role ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
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
      "typeVersion": 4.6,
      "position": [
        -560,
        120
      ],
      "id": "ac3b1943-79c2-4e48-b153-6c14e959d2f9",
      "name": "Google Sheets",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "tY0FJBuJ7JTKB0im",
          "name": "N8n X Google"
        }
      }
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
              "id": "ca910321-414b-4eb2-8dc1-743ebc94aaab",
              "leftValue": "={{ $json.status }}",
              "rightValue": "=safe",
              "operator": {
                "type": "string",
                "operation": "equals",
                "name": "filter.operator.equals"
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
        -940,
        160
      ],
      "id": "2bba4478-8b14-41de-ab40-7181ff76d5f7",
      "name": "If1"
    },
    {
      "parameters": {
        "rule": {
          "interval": [
            {}
          ]
        }
      },
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1.2,
      "position": [
        -1580,
        -300
      ],
      "id": "9bca5253-c914-4a8e-9d5b-3c5132c247ce",
      "name": "Schedule Trigger"
    },
    {
      "parameters": {
        "url": "=https://emailverifier.reoon.com/api/v1/verify?email={{ $json['Email 1'] }}&key=XXXXXXXXXXXXXX&mode=power",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        -1160,
        160
      ],
      "id": "cbdc9fe6-d52e-400f-bc99-504ffe0e836a",
      "name": "quick Reoon verifier "
    }
  ],
  "pinData": {
    "When clicking ‘Execute workflow’": [
      {
        "json": {}
      }
    ]
  },
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Google Sheets5",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Loop Over Items1": {
      "main": [
        [],
        [
          {
            "node": "Edit Fields1",
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
            "node": "Loop Over Items1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Google Sheets5": {
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
    "Google Sheets7": {
      "main": [
        [
          {
            "node": "Loop Over Items1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Edit Fields1": {
      "main": [
        [
          {
            "node": "quick Reoon verifier ",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Google Sheets": {
      "main": [
        [
          {
            "node": "Loop Over Items1",
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
            "node": "Google Sheets",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Google Sheets7",
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
            "node": "Google Sheets5",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "quick Reoon verifier ": {
      "main": [
        [
          {
            "node": "If1",
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
  "versionId": "915b18ca-ffdd-40ef-899f-dc6b52732207",
  "meta": {
    "instanceId": "77f1d8375380ee2bc4995763b4e39528bf040d446fc3e9e5f6d802ec19784049"
  },
  "id": "9v5iEtBOIgZPY5Ii",
  "tags": []
}
