# API Documents

  - **Base URL:** `http://bk-api.balancikaapps.com`
  - **Header:** [Generate Token](#authentication)
    ```json
    { 
      "Authentication": "Bearer ..."
    }
    ```

# How to create an invoice
  - **Endpoint Path:** `/api/invoice`
  - **Method:** `POST`
  - **Body:** [Invoice Object](#invoice-object)

  - ## Response
    - **Status Code :** `200`
    - **Result :** `true`
  
  - ## Error
    - **Status Code :** `400`
    - **Result :** e.g.:
      ```json
      {
        "message": "Invalid Invoice",
        "validation": {
          "custId": "Invalid Customer Id",
          "empId": "Invalid Employee Id",
          "items": [
            {
              "itemId": "Invalid Item Id",
              "uomId": "Invalid Uom Id"
            }
          ]
        }
      }
      ```

## Invoice Object

### Overview

The Invoice object represents an invoice with various details including customer information, itemized details, and tax information.

### Fields

  - **id**: **`required`**
    - The unique identifier for the invoice. (e.g., `"INV000001"`)
    - Type: **`string`**
    - Default: **`"***NEW***"`** for system generate the unique identifier for the invoice

  - **custId**: **`required`**
    - Customer ID associated with the invoice. (e.g., `"BC000001"`)
    - Type: **`string`**

  - **empId**: **`required`**
    - Employee ID who created the invoice. (e.g., `"E00001"`)
    - Type: **`string`**

  - **classId**: *`optional`*
    - Class ID for categorizing the invoice. (e.g., `"ECOM"`)
    - Type: **`string`**

  - **pcId**: **`required`**
    - Price Code ID related to the invoice. (e.g., `"EA"`)
    - Type: **`string`**

  - **term**: *`optional`*
    - Payment term. (e.g., `"NET_15"`)
    - Type: **`string`**

  - **ref**: *`optional`*
    - Reference number
    - Type: **`string`**

  - **remark**: *`optional`*
    - Additional remarks.
    - Type: **`string`**

  - **prefix**: *`optional`*
    - Prefix used for the invoice number. (e.g., `"INVOICE"`)
    - Type: **`string`**
    - Default: `DEFAULT`

  - **createdBy**: **`required`**
    - Username of the person who created the invoice. (e.g., `"narongsay"`)
    - Type: **`string`**

  - **createdAt**: **`required`**
    - Timestamp when the invoice was created. (e.g., `"2024-07-20 15:15:34"`)
    - Type: **`datetime`**
    - Date format `"yyyy-MM-dd HH:mm:ss"`

  - **invAt**: *`optional`*
    - Timestamp when the invoice was issued. (e.g., `"2021-12-21 15:15:34"`)
    - Type: **`datetime`**
    - Date format `"yyyy-MM-dd HH:mm:ss"`

  - **stockAt**: *`optional`*
    - Timestamp when the stock was recorded. (e.g., `"2021-12-21 15:15:34"`)
    - Type: **`datetime`**
    - Date format `"yyyy-MM-dd HH:mm:ss"`

  - **dueAt**: *`optional`*
    - Due date for the invoice payment. (e.g., `"2021-12-30 15:15:34"`)
    - Type: **`datetime`**
    - Date format `"yyyy-MM-dd HH:mm:ss"`

  - **currency**: **`required`**
    - Currency information.
    - Type: [Currency Object](#invoice-currency-object)

  - **poId**: *`optional`*
    - Purchase Order ID, if applicable. (e.g., `""`)
    - Type: **`string`**

  - **soId**: *`optional`*
    - Sales Order ID, if applicable. (e.g., `""`)
    - Type: **`string`**

  - **taxBeforeDiscount**: *`optional`*
    - Indicates if tax is applied before discount. (e.g., `true`)
    - Type: **`boolean`**
    - Default: `false`

  - **cardId**: *`optional`*
    - Card ID, if applicable.
    - Type: **`string`**

  - **bankId**: *`optional`*
    - Bank ID associated with the invoice.
    - Type: **`string`**

  - **items**: **`required`**
    - An array of items included in the invoice.
    - Type: [Invoice Item Object](#invoice-item-object)

## Invoice Item Object

### Overview

An item included in the invoice.

#### Field

  - **line**: `required`
    - Line number of the item in the invoice. (e.g., `1`)
    - Type: **`int`**

  - **itemId**: `required`
    - Unique identifier for the item. (e.g., `"101010411"`)
    - Type: **`string`**

  - **description**: *`optional`*
    - Description of the item. (e.g., `""`)
    - Type: **`string`**

  - **locId**: `required`
    - Location ID where the item is stored. (e.g., `"KD"`)
    - Type: **`string`**

  - **classId**: *`optional`*
    - Class ID for categorizing the item. (e.g., `"ECOM"`)
    - Type: **`string`**

  - **uomId**: `required`
    - Unit of Measure ID. (e.g., `"EA"`)
    - Type: **`string`**

  - **qty**: `required`
    - Quantity of the item. (e.g., `2`)
    - Type: **`int`**

  - **price**: `required`
    - Price per unit of the item. (e.g., `10.0`)
    - Type: **`double`**

  - **discount**: *`optional`*
    - Discount information.
    - Type: [Discount Object](#discount-object)

  - **tax1**: *`optional`*
    - Tax amount for tax category 1. (e.g., `0`)
    - Type: **`int`**

  - **tax2**: *`optional`*
    - Tax amount for tax category 2. (e.g., `0`)
    - Type: **`int`**

  - **tax3**: *`optional`*
    - Tax amount for tax category 3. (e.g., `0`)
    - Type: **`int`**

  - **tax4**: *`optional`*
    - Tax amount for tax category 4. (e.g., `26`)
    - Type: **`int`**

  - **tax5**: *`optional`*
    - Tax amount for tax category 5. (e.g., `0`)
    - Type: **`int`**



## Invoice Currency Object

### Overview
Currency information.

#### Field

  - **id**: `required`
    - Currency code. (e.g., `"USD"`)
    - Type: **`string`**
  - **rate**: *`optional`*
    - Currency exchange rate. (e.g., `4100`)
    - Type: **`double`**

## Discount Object
### Overview
Invoice item discount information.
#### Field
  - **percentage**: `required`
    - Discount percentage. (e.g., `10`)
    - Type: **`number`**


### Example

```json
{
    "id": "***NEW***",
    "custId": "BC000001",
    "empId": "E00001",
    "classId": "ECOM",
    "pcId": "chomrurn",
    "term": "Type1",
    "ref": "",
    "remark": "",
    "prefix": "INVOICE",
    "createdBy": "narongsay",
    "createdAt": "2024-07-20 15:15:34",
    "invAt": "2021-12-21 15:15:34",
    "stockAt": "2021-12-21 15:15:34",
    "dueAt": "2021-12-30 15:15:34",
    "currency": {
        "id": "EUR"
    },
    "poId": "",
    "soId": "",
    "taxBeforeDiscount": true,
    "cardId": "",
    "bankId": 0,
    "items": [
        {
            "line": 1,
            "itemId": "101010411",
            "description": "",
            "locId": "KD",
            "classId": "ECOM",
            "uomId": "EA",
            "qty": 2,
            "price": 10,
            "discount": {
                "percentage": 0
            },
            "tax1": 0,
            "tax2": 0,
            "tax3": 0,
            "tax4": 26,
            "tax5": 0
        },
        {
            "line": 2,
            "itemId": "AAAAAA",
            "description": "",
            "locId": "KD",
            "classId": "ECOM",
            "uomId": "EA",
            "qty": 3,
            "price": 5,
            "discount": {
                "percentage": 10
            },
            "tax1": 0,
            "tax2": 0,
            "tax3": 0,
            "tax4": 0,
            "tax5": 0
        }
    ]
}
```

# Authentication
  API keys are required for all requests.

  ## Overview
  - **Base URL:** `https://oauth.balancikaapps.com`
  - **Headers:**
    ```json
    { 
      "Authentication": "Basic YmFsYW5jaWthX2FwaTpiYWxhbmNpa2FAMTY4"
    }
    ```
  
  ## Generate Token
  - **Endpoint Path:** `/oauth/token`
  - **Method:** `POST`
  - **Body:** [Balancika Cambodia](https://balancikacambodia.com/) will provide username and password for access to APIs
    ```json
    {
      "username": "[USERNAME]",
      "password": "[PASSWORD]",
      "type": "password"
    }
    ```

  - ### Response
    - **Status Code :** `200`
    - **Result :**
      ```json
      {
        "access_token": "...",
        "token_type": "...",
        "refresh_token": "...",
        "expires_in": 271824224,
        ...
      }
      ```
  
  - ### Error
    - **Status Code :** `400`
    - **Result :** `Invalid username and password`      
      ```json
      {
        "error": "invalid_grant",
        "error_description": "Bad credentials"
      }
      ```