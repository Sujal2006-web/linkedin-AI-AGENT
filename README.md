// {
  "name": "Ultimate Lnkdn email finder",
  "nodes": [
    // ... (Other nodes remain unchanged for brevity; only modified ones are shown below)

    {
      "parameters": {
        "assignments": {
          "assignments": [
            // ... (Other assignments unchanged)
            {
              "id": "f62e4489-3af5-414e-a7eb-b3bf51e0cfdc",
              "name": "Location",  // Fixed typo from "Loaction"
              "value": "={{ $json.addressWithCountry }}",
              "type": "string"
            },
            // ... (Rest unchanged)
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [440, 120],
      "id": "993d1746-bcc3-4960-864e-85c29b35d238",
      "name": "Edit Fields"
    },

    // ... (Skipping unchanged nodes)

    {
      "parameters": {
        "operation": "append",
        "documentId": { ... },  // Unchanged
        "sheetName": { ... },  // Unchanged
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Full Name": "={{ $('Edit Fields').first().json['Full Name'] }}",
            "Email": "={{ $('Edit Fields').first().json['Email'] }}",  // Fixed to correct field
            "Company Name": "={{ $('Edit Fields').first().json['Company Name'] }}",
            "Company Website": "={{ $('Edit Fields').first().json['Company Website'] }}",
            "Role": "={{ $('Edit Fields').first().json['Role'] }}",  // Removed trailing space for consistency
            "Company Industry": "={{ $('Edit Fields').first().json['Company Industry'] }}",
            "Location": "={{ $('Edit Fields').first().json.Location }}",  // Fixed typo
            "Lindin URL": "={{ $('Edit Fields').first().json.linkedinUrl }}"
          },
          // ... (Rest unchanged)
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [700, 820],
      "id": "a1c4a41e-15d6-4669-bd01-99ba972f4a5b",
      "name": "No data found1"
    },

    // ... (Similarly, apply fixes to other nodes like "No data found", "Email found", etc., if they have the same issues)

    {
      "parameters": {
        "operation": "append",
        "documentId": { ... },
        "sheetName": { ... },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Full Name": "={{ $('Edit Fields').first().json['Full Name'] }}",
            "Company Name": "={{ $('Edit Fields').first().json['Company Name'] }}",
            "Company Website": "={{ $('Edit Fields').first().json['Company Website'] }}",
            "Company Industry": "={{ $('Edit Fields').first().json['Company Industry'] }}",
            "Location": "={{ $('Edit Fields').first().json.Location }}",  // Fixed typo
            "linkedinUrl": "={{ $('Edit Fields').first().json.linkedinUrl }}",
            "Role ": "={{ $('Edit Fields').first().json['Role'] }}",  // Fixed for consistency
            "Email 1": "={{ $json.emails.split(',')[0].trim() }}",
            "Rest Emails": "={{ $json.emails.split(',').slice(1).join(',') }}"
          },
          // ... (Rest unchanged)
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.5,
      "position": [1220, 580],
      "id": "add4436f-52f3-41f4-b91e-48d3d8dbedad",
      "name": "Email found"
    },

    // ... (Rest of the nodes unchanged)
  ],
  // ... (The rest of the JSON, like connections and settings, remains the same)
}
