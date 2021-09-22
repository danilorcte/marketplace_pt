# \testIntegration

Neste remote iremos disparar uma notificação sempre.

<!--
focus: false
-->
![image.png](https://stoplight.io/api/v1/projects/cHJqOjgzMDA1/images/1hmZJccVDNo)
### Comportamento esperado

### Requisição

```json title="POST: \testIntegration" lineNumbers
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
      "type": "integer",
      "description": "Id da Conta"
    },
    "active": {
      "type": "boolean",
      "description": ""
    },
    "templateId": {
      "type": "number",
      "description": ""
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
      "type": "boolean",
      "description": ""
    },
    "accountDefault": {
      "type": "boolean",
      "description": ""
    },
     "priceFactor": {
      "type": "number",
      "description": ""
    },
    "discountValue": {
      "type": "number",
      "description": ""
    },
    "initialDateForOrderImport": {
      "type": "string",
      "format": "dd-MM-yyyy",
      "description": ""
    },
    "updatePriceStockStatus": {
      "type": "boolean",
      "description": ""
    },
    "additionOfFreight": {
      "type": "integer",
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

### Respostas que esperamos

```json title="200 - OK" 
true
```

---

```json title="401 - Unauthorized"  
false
```
