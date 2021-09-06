# \testintegration

Neste remote iremos disparar uma notificação sempre.

<!--
focus: false
-->
![image.png](https://stoplight.io/api/v1/projects/cHJqOjgzMDA1/images/1hmZJccVDNo)



```json title="\testintegration" lineNumbers
{
	"id": 10,
	"active": true,
	"templateId": 10,
	"accountName": "accountName",
	"discountType": "PERCENT",
	"useSandbox": true,
	"accountDefault": true,
	"priceFactor": 10.0,
	"discountValue": 5.0,
	"initialDateForOrderImport": "dd-MM-yyyy",
	"updatePriceStockStatus": true,
	"additionOfFreight": 0
	"login": "XXXXXXXX",
	"senha": "XXXXXXXX"
}
```

---

```json json_schema
{
  "title": "testIntegration",
  "type": "object",
  "properties": {
    "id": {
      "type": "string",
      "description": "Id da Conta"
    },
    "active": {
      "type": "string",
      "description": ""
    },
    "templateId": {
      "type": "number",
      "minimum": 0,
      "maximum": 150
    },
    "accountName": {
      "type": "string",
      "description": ""
    },
    "discountType": {
      "type": "string",
      "description": ""
    },
    "useSandbox": {
      "type": "string",
      "description": ""
    },
    "accountDefault": {
      "type": "string",
      "description": ""
    },
     "priceFactor": {
      "type": "string",
      "description": ""
    },
    "discountValue": {
      "type": "string",
      "description": ""
    },
    "initialDateForOrderImport": {
      "type": "string",
      "description": ""
    },
    "updatePriceStockStatus": {
      "type": "string",
      "description": ""
    },
    "additionOfFreight": {
      "type": "string",
      "description": ""
    },
    "login": {
      "type": "string",
      "description": ""
    },
    "senha": {
      "type": "string",
      "description": ""
    }
  }
}
```

---

```json title="200 - OK" 
true
```

---

```json title="401 - Unauthorized"  
false
```
