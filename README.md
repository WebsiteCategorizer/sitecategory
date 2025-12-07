# SiteCategory.com API

**Free, Fast, and Accurate Website Categorization API & Database**

[![SiteCategory.com](https://img.shields.io/badge/Status-Online-success)](https://sitecategory.com)

[![API Latency](https://img.shields.io/badge/Latency-~50ms-blue)](https://sitecategory.com)

[![License](https://img.shields.io/badge/License-Free-green)](https://sitecategory.com)

[![Categorized Domains](https://img.shields.io/badge/Domains-99.4M+-orange)](https://sitecategory.com)

Stop paying for website categorization. **[SiteCategory.com](https://sitecategory.com)** provides a developer-first API for [website categorization](https://sitecategory.com), [domain classification](https://sitecategory.com), and [content categorization](https://sitecategory.com). No API key required for standard usage, 100 requests/day rate limit, and continuously updated data.

---

## 🚀 Features

*   **Completely Free:** No credit card or API key required for standard usage (100 requests/day).

*   **Ultra Low Latency:** ~50ms average response time with optimized infrastructure.

*   **Massive Database:**
    *   **99.4M+ Categorized Domains:** All domains have verified categories.
    *   **636M+ Domains Crawled:** Comprehensive coverage of the web.
    *   **174M+ Active Websites:** Real-time categorization data.
    *   **100+ Categories:** Complete classification system.

*   **Easy Integration:** Simple REST API with session-based authentication.

*   **Offline Database:** Download complete database in CSV or SQL format for self-hosting.

*   **Enterprise Ready:** [Enterprise API](https://sitecategory.com/domain-categories-database) available with no rate limits.

---

## ⚡ Quick Start

Get the category for any domain instantly using `curl`:

### Step 1: Get Authorization Token

```bash
curl -X POST https://api.sitecategory.com/api/session \
  -H "Content-Type: application/json"
```

### Step 2: Categorize Domain

```bash
curl -X POST https://api.sitecategory.com/api/categorize \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_SESSION_TOKEN" \
  -d '{"domain": "google.com"}'
```

### Example Response

```json
{
  "success": true,
  "domain": "google.com",
  "category": "Search Engines and Portals"
}
```

---

## 💻 Integration Examples

Integrate SiteCategory.com into your project in under a minute.

### JavaScript / Node.js

```javascript
// Step 1: Get session token
const sessionResponse = await fetch('https://api.sitecategory.com/api/session', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' }
});
const sessionData = await sessionResponse.json();
const token = sessionData.token;

// Step 2: Categorize domain
const response = await fetch('https://api.sitecategory.com/api/categorize', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${token}`
  },
  body: JSON.stringify({ domain: 'google.com' })
});
const data = await response.json();
console.log(data);
```

### Python

```python
import requests

# Step 1: Get session token
session_response = requests.post(
    'https://api.sitecategory.com/api/session',
    headers={'Content-Type': 'application/json'}
)
token = session_response.json()['token']

# Step 2: Categorize domain
response = requests.post(
    'https://api.sitecategory.com/api/categorize',
    headers={
        'Content-Type': 'application/json',
        'Authorization': f'Bearer {token}'
    },
    json={'domain': 'google.com'}
)
print(response.json())
```

### PHP

```php
// Step 1: Get session token
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.sitecategory.com/api/session');
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, ['Content-Type: application/json']);
$response = curl_exec($ch);
curl_close($ch);
$data = json_decode($response, true);
$token = $data['token'];

// Step 2: Categorize domain
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api.sitecategory.com/api/categorize');
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode(['domain' => 'google.com']));
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Content-Type: application/json',
    'Authorization: Bearer ' . $token
]);
$response = curl_exec($ch);
curl_close($ch);
print_r(json_decode($response, true));
```

### Go

```go
package main

import (
	"bytes"
	"encoding/json"
	"fmt"
	"io/ioutil"
	"net/http"
)

func main() {
	// Step 1: Get session token
	sessionReq, _ := http.NewRequest("POST", "https://api.sitecategory.com/api/session", nil)
	sessionReq.Header.Set("Content-Type", "application/json")
	client := &http.Client{}
	sessionResp, _ := client.Do(sessionReq)
	sessionBody, _ := ioutil.ReadAll(sessionResp.Body)
	var sessionData map[string]interface{}
	json.Unmarshal(sessionBody, &sessionData)
	token := sessionData["token"].(string)

	// Step 2: Categorize domain
	payload := map[string]string{"domain": "google.com"}
	jsonPayload, _ := json.Marshal(payload)
	req, _ := http.NewRequest("POST", "https://api.sitecategory.com/api/categorize", bytes.NewBuffer(jsonPayload))
	req.Header.Set("Content-Type", "application/json")
	req.Header.Set("Authorization", "Bearer "+token)
	resp, _ := client.Do(req)
	body, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(body))
}
```

### Java

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.http.HttpRequest.BodyPublishers;
import java.net.http.HttpResponse.BodyHandlers;
import com.google.gson.Gson;
import com.google.gson.JsonObject;

public class Main {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newHttpClient();
        Gson gson = new Gson();

        // Step 1: Get session token
        HttpRequest sessionRequest = HttpRequest.newBuilder()
                .uri(URI.create("https://api.sitecategory.com/api/session"))
                .header("Content-Type", "application/json")
                .POST(BodyPublishers.noBody())
                .build();
        HttpResponse<String> sessionResponse = client.send(sessionRequest, BodyHandlers.ofString());
        JsonObject sessionData = gson.fromJson(sessionResponse.body(), JsonObject.class);
        String token = sessionData.get("token").getAsString();

        // Step 2: Categorize domain
        JsonObject payload = new JsonObject();
        payload.addProperty("domain", "google.com");
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://api.sitecategory.com/api/categorize"))
                .header("Content-Type", "application/json")
                .header("Authorization", "Bearer " + token)
                .POST(BodyPublishers.ofString(gson.toJson(payload)))
                .build();
        HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
        System.out.println(response.body());
    }
}
```

---

## 🗄️ Database Download

For high-volume applications, download the complete [website categorization database](https://sitecategory.com/domain-categories-database) for self-hosting:

*   **99.4M+ Categorized Domains:** All domains with verified categories.
*   **CSV & SQL Formats:** Ready for import into your database.
*   **One-Time Purchase:** $9,999 for unlimited lookups.
*   **Country Data Included:** Geographic information for each domain.
*   **Commercial License:** Use in production applications.

Visit our [database page](https://sitecategory.com/domain-categories-database) for more information and pricing.

---

## 📊 Use Cases

*   **Content Filtering:** Block or allow access to specific website categories for parental controls, corporate networks, or educational institutions.

*   **Ad Targeting:** [Programmatic advertising](https://sitecategory.com) platforms use categorization to place ads on relevant websites.

*   **Security Policies:** Enforce access policies based on website categories to protect networks from malicious content.

*   **Compliance Monitoring:** Financial institutions track which categories of websites their customers visit for regulatory compliance.

*   **Traffic Analysis:** Understand website visitor behavior and competitive intelligence.

*   **Automated Content Moderation:** Social platforms use categorization for automated content filtering.

---

## 🔒 Rate Limits

*   **Free Tier:** 100 requests per day per session token and per IP address.
*   **Enterprise API:** No rate limits available. [Contact us](mailto:support@sitecategory.com) for custom pricing.

---

## 🔗 Links

*   **Website:** [https://sitecategory.com](https://sitecategory.com)
*   **API Documentation:** [https://sitecategory.com](https://sitecategory.com)
*   **Database Download:** [https://sitecategory.com/domain-categories-database](https://sitecategory.com/domain-categories-database)
*   **Global Statistics:** [https://sitecategory.com/stats](https://sitecategory.com/stats)
*   **Support:** [support@sitecategory.com](mailto:support@sitecategory.com)

---

## 📈 Statistics

*   **636M+ Domains Crawled**
*   **174M+ Active Websites**
*   **99.4M+ Categorized Domains**
*   **100+ Distinct Categories**

View live [API request statistics](https://sitecategory.com/stats) from around the world.

---

## 🏷️ Keywords

[Website Categorization](https://sitecategory.com) • [Domain Classification](https://sitecategory.com) • [Website Category API](https://sitecategory.com) • [Domain Category Lookup](https://sitecategory.com) • [Website Classification Database](https://sitecategory.com) • [Content Categorization](https://sitecategory.com) • [URL Categorization](https://sitecategory.com) • [Website Intelligence](https://sitecategory.com) • [Domain Classification API](https://sitecategory.com) • [Website Category Database](https://sitecategory.com)

---

&copy; 2025 SiteCategory. All rights reserved.

