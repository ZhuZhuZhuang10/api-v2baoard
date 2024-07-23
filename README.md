# FULL API

## API Documentation

### 1. Fetch Orders (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/orders`  
**Query Parameters:**

- `status` (optional) — status of the order for filtering.

**Example Request:**

```http
GET /api/v1/user/orders?status=pending
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": [
        {
            "trade_no": "1234567890",
            "plan_id": 1,
            "period": "monthly",
            "total_amount": 10.00,
            "status": 0,
            "plan": {
                "id": 1,
                "name": "Basic Plan"
            }
        }
    ]
}
```

### 2. Get Order Details (`detail`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/order/detail`  
**Query Parameters:**

- `trade_no` — unique order number.

**Example Request:**

```http
GET /api/v1/user/order/detail?trade_no=1234567890
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": {
        "trade_no": "1234567890",
        "plan_id": 1,
        "period": "monthly",
        "total_amount": 10.00,
        "status": 0,
        "plan": {
            "id": 1,
            "name": "Basic Plan"
        }
    }
}
```

### 3. Save Order (`save`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/order/save`  
**Request Body:**

- `plan_id` — Plan ID.
- `period` — Payment period (e.g., "monthly").
- `coupon_code` (optional) — Coupon code to apply.

**Example Request:**

```http
POST /api/v1/user/order/save
Authorization: Bearer {token}
Content-Type: application/json

{
    "plan_id": 1,
    "period": "monthly",
    "coupon_code": "DISCOUNT10"
}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": "1234567890"
}
```

### 4. Check Order Status (`check`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/order/check`  
**Query Parameters:**

- `trade_no` — unique order number.

**Example Request:**

```http
GET /api/v1/user/order/check?trade_no=1234567890
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": 1
}
```

### 5. Get Available Payment Methods (`getPaymentMethod`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/payment/methods`

**Example Request:**

```http
GET /api/v1/user/payment/methods
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": [
        {
            "id": 1,
            "name": "Credit Card",
            "payment": "stripe",
            "icon": "/icons/credit-card.png",
            "handling_fee_fixed": 1.00,
            "handling_fee_percent": 2.5
        }
    ]
}
```

### 6. Checkout Order (`checkout`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/order/checkout`  
**Request Body:**

- `trade_no` — unique order number.
- `method` — payment method.
- `token` (optional) — Stripe token for payment.

**Example Request:**

```http
POST /api/v1/user/order/checkout
Authorization: Bearer {token}
Content-Type: application/json

{
    "trade_no": "1234567890",
    "method": 1,
    "token": "tok_visa"
}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "type": 1,
    "data": {
        "payment_url": "https://paymentgateway.com/pay/1234567890"
    }
}
```

### 7. Cancel Order (`cancel`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/order/cancel`  
**Request Body:**

- `trade_no` — unique order number.

**Example Request:**

```http
POST /api/v1/user/order/cancel
Authorization: Bearer {token}
Content-Type: application/json

{
    "trade_no": "1234567890"
}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": true
}
```


Certainly! Here’s the API documentation for the `UserController` in English.

## API Documentation

### 1. Get Active Sessions (`getActiveSession`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/sessions`  

**Example Request:**

```http
GET /api/v1/user/sessions
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": [
        {
            "session_id": "abc123",
            "ip": "192.168.1.1",
            "last_activity": "2024-07-24T12:34:56Z"
        }
    ]
}
```

### 2. Remove Active Session (`removeActiveSession`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/sessions/remove`  
**Request Body:**

- `session_id` — The ID of the session to be removed.

**Example Request:**

```http
POST /api/v1/user/sessions/remove
Authorization: Bearer {token}
Content-Type: application/json

{
    "session_id": "abc123"
}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": true
}
```

### 3. Check Login Status (`checkLogin`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/login/status`

**Example Request:**

```http
GET /api/v1/user/login/status
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": {
        "is_login": true,
        "is_admin": false
    }
}
```

### 4. Change Password (`changePassword`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/password/change`  
**Request Body:**

- `old_password` — Current password.
- `new_password` — New password.

**Example Request:**

```http
POST /api/v1/user/password/change
Authorization: Bearer {token}
Content-Type: application/json

{
    "old_password": "oldPass123",
    "new_password": "newPass456"
}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": true
}
```

### 5. Get User Info (`info`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/info`

**Example Request:**

```http
GET /api/v1/user/info
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": {
        "email": "user@example.com",
        "transfer_enable": 10000,
        "device_limit": 3,
        "last_login_at": "2024-07-24T12:34:56Z",
        "created_at": "2023-01-01T12:00:00Z",
        "banned": false,
        "remind_expire": true,
        "remind_traffic": false,
        "expired_at": "2024-12-31T23:59:59Z",
        "balance": 50.00,
        "commission_balance": 10.00,
        "plan_id": 1,
        "discount": 5,
        "commission_rate": 2.5,
        "telegram_id": "123456789",
        "uuid": "abcd-1234-efgh-5678",
        "avatar_url": "https://www.gravatar.com/avatar/{md5_email}?s=64&d=identicon"
    }
}
```

### 6. Get User Statistics (`getStat`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/statistics`

**Example Request:**

```http
GET /api/v1/user/statistics
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": [
        5,  // Pending Orders
        2,  // Open Tickets
        10  // Invited Users
    ]
}
```

### 7. Get Subscription Info (`getSubscribe`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/subscription`

**Example Request:**

```http
GET /api/v1/user/subscription
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": {
        "plan_id": 1,
        "token": "abcdef123456",
        "expired_at": "2024-12-31T23:59:59Z",
        "u": 1000,
        "d": 500,
        "transfer_enable": 10000,
        "device_limit": 3,
        "email": "user@example.com",
        "uuid": "abcd-1234-efgh-5678",
        "plan": {
            "id": 1,
            "name": "Premium Plan"
        },
        "alive_ip": 3,
        "subscribe_url": "https://example.com/subscribe?token=abcdef123456",
        "reset_day": 30
    }
}
```

### 8. Reset Security Information (`resetSecurity`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/security/reset`

**Example Request:**

```http
POST /api/v1/user/security/reset
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": "https://example.com/subscribe?token=newtoken123456"
}
```

### 9. Update User Settings (`update`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/settings/update`  
**Request Body:**

- `remind_expire` — Boolean indicating whether to remind about expiration.
- `remind_traffic` — Boolean indicating whether to remind about traffic.

**Example Request:**

```http
POST /api/v1/user/settings/update
Authorization: Bearer {token}
Content-Type: application/json

{
    "remind_expire": true,
    "remind_traffic": false
}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": true
}
```

### 10. Transfer Commission (`transfer`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/commission/transfer`  
**Request Body:**

- `transfer_amount` — Amount of commission to transfer.

**Example Request:**

```http
POST /api/v1/user/commission/transfer
Authorization: Bearer {token}
Content-Type: application/json

{
    "transfer_amount": 10.00
}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": true
}
```

### 11. Get Quick Login URL (`getQuickLoginUrl`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/login/quick`  
**Query Parameters:**

- `redirect` (optional) — URL to redirect to after login.

**Example Request:**

```http
GET /api/v1/user/login/quick?redirect=dashboard
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": "https://example.com/#/login?verify=unique_code&redirect=dashboard"
}
```

## Summary

This API controller provides endpoints for user management, including session management, password changes, user information retrieval, subscription details, and quick login URLs. Each endpoint is protected and requires an authorization token in the `Authorization` header. Follow the provided examples for requests and responses to interact with these endpoints effectively.

Here's the API documentation for the `TicketController` in English.

## API Documentation

### 1. Fetch Tickets (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/tickets`  
**Query Parameters:**

- `id` (optional) — The ID of a specific ticket to fetch.

**Example Request:**

```http
GET /api/v1/user/tickets?id=123
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

- When `id` is provided:

```json
{
    "data": {
        "id": 123,
        "user_id": 1,
        "subject": "Issue with account",
        "level": 1,
        "status": 0,
        "created_at": "2024-07-24T12:34:56Z",
        "updated_at": "2024-07-24T12:34:56Z",
        "message": [
            {
                "user_id": 1,
                "message": "This is a message",
                "created_at": "2024-07-24T12:34:56Z",
                "is_me": false
            }
        ]
    }
}
```

- When `id` is not provided:

```json
{
    "data": [
        {
            "id": 123,
            "user_id": 1,
            "subject": "Issue with account",
            "level": 1,
            "status": 0,
            "created_at": "2024-07-24T12:34:56Z",
            "updated_at": "2024-07-24T12:34:56Z"
        }
    ]
}
```

### 2. Save Ticket (`save`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/tickets/save`  
**Request Body:**

- `subject` — The subject of the ticket.
- `level` — The urgency level of the ticket.
- `message` — The initial message for the ticket.

**Example Request:**

```http
POST /api/v1/user/tickets/save
Authorization: Bearer {token}
Content-Type: application/json

{
    "subject": "Issue with billing",
    "level": 2,
    "message": "The invoice is incorrect."
}
```

#### Response

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "Tickets are temporarily closed"
}
```

### 3. Reply to Ticket (`reply`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/tickets/reply`  
**Request Body:**

- `id` — The ID of the ticket to reply to.
- `message` — The message to send in the reply.

**Example Request:**

```http
POST /api/v1/user/tickets/reply
Authorization: Bearer {token}
Content-Type: application/json

{
    "id": 123,
    "message": "Thank you for your response."
}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": true
}
```

### 4. Close Ticket (`close`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/tickets/close`  
**Request Body:**

- `id` — The ID of the ticket to close.

**Example Request:**

```http
POST /api/v1/user/tickets/close
Authorization: Bearer {token}
Content-Type: application/json

{
    "id": 123
}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": true
}
```

### 5. Withdraw Commission (`withdraw`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/tickets/withdraw`  
**Request Body:**

- `withdraw_method` — The method of withdrawal.
- `withdraw_account` — The account for withdrawal.

**Example Request:**

```http
POST /api/v1/user/tickets/withdraw
Authorization: Bearer {token}
Content-Type: application/json

{
    "withdraw_method": "PayPal",
    "withdraw_account": "user@example.com"
}
```

#### Response

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "Tickets are temporarily closed"
}
```

### Private Methods

- **`sendNotify(Ticket $ticket, string $message, $userid = null)`**: Sends notifications about the ticket via Telegram. This method is called internally to notify admins or users.
- **`getFlowData($b)`**: Converts flow data from bytes to a human-readable format (GB/MB).

## Summary

This API controller provides endpoints for managing support tickets, including fetching tickets, saving new tickets, replying to tickets, closing tickets, and requesting commission withdrawals. Some endpoints are temporarily closed for maintenance. Each request requires an authorization token in the `Authorization` header. The provided examples should be used as a guide to correctly format requests and handle responses.

Here's the API documentation for the `InviteController` in English.

## API Documentation

### 1. Save Invite Code (`save`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/invite/save`  
**Request Body:**

No parameters are required in the request body.

**Example Request:**

```http
POST /api/v1/user/invite/save
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": true
}
```

**Error Response:**

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "The maximum number of creations has been reached"
}
```

### 2. Invite Details (`details`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/invite/details`  
**Query Parameters:**

- `current` (optional) — The page number to fetch (default is 1).
- `page_size` (optional) — The number of records per page (default is 10, minimum is 10).

**Example Request:**

```http
GET /api/v1/user/invite/details?current=1&page_size=20
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": [
        {
            "id": 123,
            "trade_no": "TRADE123456",
            "order_amount": 100,
            "get_amount": 10,
            "created_at": "2024-07-24T12:34:56Z"
        }
    ],
    "total": 1
}
```

### 3. Fetch Invite Codes and Statistics (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/invite/fetch`  
**Query Parameters:**

No parameters are required in the query string.

**Example Request:**

```http
GET /api/v1/user/invite/fetch
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": {
        "codes": [
            {
                "id": 1,
                "user_id": 1,
                "code": 12345,
                "status": 0
            }
        ],
        "stat": [
            10,  // Number of registered users
            100, // Valid commissions
            50,  // Commission in confirmation
            10,  // Commission rate
            200  // Available commission
        ]
    }
}
```

### Summary

This API controller manages the invitation codes and related statistics for users. It includes functionality to:

- **Generate a new invite code** (`save`).
- **Retrieve a list of commission logs** related to invite codes (`details`).
- **Fetch invite codes and overall statistics** related to commissions and invites (`fetch`).

Each request requires an authorization token in the `Authorization` header. The provided examples should be used as a guide to format requests and handle responses effectively.

Here's the API documentation for the `CommController` in English.

## API Documentation

### 1. Get Configuration (`config`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/comm/config`  
**Query Parameters:** 

None required.

**Example Request:**

```http
GET /api/v1/user/comm/config
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": {
        "is_telegram": 1,
        "telegram_discuss_link": "https://t.me/example_channel",
        "stripe_pk": "pk_test_XXXXXXXXXXXXXX",
        "withdraw_methods": [
            "paypal",
            "bank_transfer"
        ],
        "withdraw_close": 0,
        "currency": "CNY",
        "currency_symbol": "¥",
        "commission_distribution_enable": 1,
        "commission_distribution_l1": 10,
        "commission_distribution_l2": 5,
        "commission_distribution_l3": 2
    }
}
```

### 2. Get Stripe Public Key (`getStripePublicKey`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/comm/get-stripe-public-key`  
**Query Parameters:**

- `id` (required) — The ID of the payment record.

**Example Request:**

```http
GET /api/v1/user/comm/get-stripe-public-key?id=1
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": "pk_test_XXXXXXXXXXXXXX"
}
```

**Error Response:**

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "payment is not found"
}
```

### Summary

This API controller provides endpoints related to configuration settings and payment details. It includes functionality to:

- **Retrieve system configuration settings** including Telegram integration, Stripe public key, withdrawal methods, and commission distribution (`config`).
- **Get the Stripe public key** associated with a specific payment record (`getStripePublicKey`).

Each request should include an authorization token in the `Authorization` header. The examples provided demonstrate how to format requests and handle responses.

Here’s the API documentation for the `CouponController`.

## API Documentation

### 1. Check Coupon (`check`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/coupon/check`  
**Query Parameters:** 

None required.

**Request Body:**

```json
{
    "code": "COUPON_CODE",
    "plan_id": 1
}
```

**Headers:**

- `Authorization: Bearer {token}` (required)

**Example Request:**

```http
POST /api/v1/user/coupon/check
Authorization: Bearer {token}
Content-Type: application/json

{
    "code": "SAVE20",
    "plan_id": 3
}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": {
        "coupon_code": "SAVE20",
        "discount_amount": 20,
        "description": "20% off on plan 3",
        "is_valid": true
    }
}
```

**Error Responses:**

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "Coupon cannot be empty!"
}
```

**HTTP Status Code:** `400 Bad Request`  
**Response Body:**

```json
{
    "message": "Invalid coupon code or plan ID"
}
```

### Summary

The `CouponController` API provides functionality to check the validity and details of a coupon code.

- **Check Coupon**: Validates a given coupon code and applies it to a specific plan. If successful, it returns details about the coupon, including any applicable discounts and descriptions.

**Error Handling:**

- The API will return a `500 Internal Server Error` if the coupon code is empty or invalid.
- A `400 Bad Request` might be returned if the coupon code or plan ID is not valid or if there are issues with the coupon application.

This documentation provides information on how to properly format requests, handle responses, and address potential errors when interacting with the coupon checking API.

Here's the API documentation for the `KnowledgeController`.

## API Documentation

### 1. Fetch Knowledge Article (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/knowledge/fetch`  
**Query Parameters:**

- `id` (optional): The ID of the knowledge article to fetch. If not provided, a list of articles is returned.
- `language` (optional): The language to filter the articles by.
- `keyword` (optional): A keyword to search within the article titles and bodies.

**Headers:**

- `Authorization: Bearer {token}` (required)

**Example Request:**

```http
GET /api/v1/user/knowledge/fetch?id=1
Authorization: Bearer {token}
```

**Example Request for List:**

```http
GET /api/v1/user/knowledge/fetch?language=en&keyword=server
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body (Single Article):**

```json
{
    "data": {
        "id": 1,
        "category": "General",
        "title": "How to Set Up a Server",
        "body": "Here is how to set up a server: {{siteName}}. For more info, visit {{subscribeUrl}}.",
        "updated_at": "2024-07-20T10:00:00Z"
    }
}
```

**Response Body (List of Articles):**

```json
{
    "data": {
        "General": [
            {
                "id": 1,
                "category": "General",
                "title": "How to Set Up a Server",
                "updated_at": "2024-07-20T10:00:00Z"
            }
        ],
        "Tips": [
            {
                "id": 2,
                "category": "Tips",
                "title": "Server Maintenance Tips",
                "updated_at": "2024-07-18T10:00:00Z"
            }
        ]
    }
}
```

**Error Responses:**

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "Article does not exist"
}
```

**HTTP Status Code:** `400 Bad Request`  
**Response Body:**

```json
{
    "message": "Invalid request parameters"
}
```

### Private Methods

- **`getBetween($input, $start, $end)`**: Extracts a substring between two markers (`$start` and `$end`) from the given `$input`.

- **`formatAccessData(&$body)`**: Replaces placeholders for subscription-required content within the article body with a message indicating that a valid subscription is required.

### Summary

The `KnowledgeController` API provides functionality to:

1. **Fetch Knowledge Articles**: Retrieve a specific knowledge article by its ID or a list of articles filtered by language and keyword. The article body may contain placeholders that are replaced with dynamic data such as site name and subscription URLs.

2. **Access Control**: If the user is not authorized to access certain content, the placeholders are replaced with a message indicating that a valid subscription is required.

**Error Handling:**

- The API will return a `500 Internal Server Error` if the specified article does not exist.
- A `400 Bad Request` might be returned if the request parameters are invalid or missing.

This documentation provides details on making requests to the `KnowledgeController` API, handling responses, and understanding the private methods used for content formatting and access control.

Here's the API documentation for the `NoticeController`.

## API Documentation

### 1. Fetch Notices (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/notice/fetch`  
**Query Parameters:**

- `current` (optional): The page number to fetch. If not provided, defaults to 1.
  
**Headers:**

- `Authorization: Bearer {token}` (required)

**Example Request:**

```http
GET /api/v1/user/notice/fetch?current=2
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": [
        {
            "id": 1,
            "title": "Important Notice",
            "body": "This is an important notice for all users.",
            "created_at": "2024-07-20T10:00:00Z"
        },
        {
            "id": 2,
            "title": "Maintenance Notice",
            "body": "Scheduled maintenance will occur on July 25th.",
            "created_at": "2024-07-19T10:00:00Z"
        }
    ],
    "total": 10
}
```

**Error Responses:**

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "An error occurred while fetching notices."
}
```

#### Description

The `fetch` method retrieves a paginated list of notices from the database.

- **Pagination**: The results are paginated with a page size of 5 notices per page.
- **Sorting**: Notices are sorted by their creation date in descending order.
- **Filtering**: Only notices with the `show` field set to `1` are included in the results.

**Fields in the Response:**

- `data`: An array of notice objects.
  - `id`: The unique identifier for the notice.
  - `title`: The title of the notice.
  - `body`: The content of the notice.
  - `created_at`: The date and time when the notice was created.
- `total`: The total number of notices available that match the criteria.

This API allows users to fetch notices in a paginated manner, providing an easy way to view the latest updates or important messages.

Here's the API documentation for the `PlanController`.

## API Documentation

### 1. Fetch Plans (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/plan/fetch`  
**Query Parameters:**

- `id` (optional): The ID of a specific plan to fetch. If not provided, fetches all plans.
  
**Headers:**

- `Authorization: Bearer {token}` (required)

**Example Request:**

```http
GET /api/v1/user/plan/fetch?id=1
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body (Single Plan):**

```json
{
    "data": {
        "id": 1,
        "name": "Premium Plan",
        "description": "Access to all premium features.",
        "price": 1999,
        "capacity_limit": 100,
        "show": 1,
        "renew": 1,
        "sort": 1
    }
}
```

**Response Body (All Plans):**

```json
{
    "data": [
        {
            "id": 1,
            "name": "Basic Plan",
            "description": "Basic features with limited capacity.",
            "price": 999,
            "capacity_limit": 50,
            "show": 1,
            "renew": 1,
            "sort": 2
        },
        {
            "id": 2,
            "name": "Premium Plan",
            "description": "Access to all premium features.",
            "price": 1999,
            "capacity_limit": 100,
            "show": 1,
            "renew": 1,
            "sort": 1
        }
    ]
}
```

**Error Responses:**

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "Subscription plan does not exist"
}
```

#### Description

The `fetch` method retrieves subscription plans from the database. It can return either a specific plan or a list of all available plans, based on the `id` query parameter.

- **Single Plan**: If the `id` parameter is provided, the API returns details of the specific plan with that ID. The plan must be either visible (`show` is `1`) or available for renewal (`renew` is `1`). If the plan does not meet these criteria, a `500` error is returned with the message "Subscription plan does not exist."
  
- **All Plans**: If the `id` parameter is not provided, the API returns a list of all plans that are currently visible (`show` is `1`). Each plan's capacity limit is adjusted based on the number of active users, if applicable.

**Fields in the Response:**

- `data`: 
  - For a single plan:
    - `id`: The unique identifier of the plan.
    - `name`: The name of the plan.
    - `description`: A description of the plan.
    - `price`: The price of the plan in cents.
    - `capacity_limit`: The capacity limit of the plan, or `null` if not applicable.
    - `show`: Indicates if the plan is visible (`1` for visible, `0` for hidden).
    - `renew`: Indicates if the plan can be renewed (`1` for yes, `0` for no).
    - `sort`: The sorting order of the plan.
  - For all plans:
    - An array of plan objects as described above.

This API provides the necessary details for users to view available subscription plans and their respective capacities, ensuring that users can make informed decisions based on their needs.

Here’s the API documentation for the `ServerController`.

## API Documentation

### 1. Fetch Available Servers (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/server/fetch`  
**Query Parameters:**

- None.

**Headers:**

- `Authorization: Bearer {token}` (required)
- `If-None-Match: "{eTag}"` (optional, for cache validation)

**Example Request:**

```http
GET /api/v1/user/server/fetch
Authorization: Bearer {token}
If-None-Match: "some-etag-value"
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": [
        {
            "id": 1,
            "name": "Server A",
            "location": "New York",
            "status": "active",
            "cache_key": "server_a_cache_key"
        },
        {
            "id": 2,
            "name": "Server B",
            "location": "Los Angeles",
            "status": "active",
            "cache_key": "server_b_cache_key"
        }
    ]
}
```

**HTTP Status Code:** `304 Not Modified`  
**Response Body:** Empty.

**Error Responses:**

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "Server information could not be fetched"
}
```

#### Description

The `fetch` method retrieves a list of available servers for the authenticated user. 

- **Cache Validation**: The API uses ETag headers for cache validation. If the client provides an `If-None-Match` header with a value that matches the current ETag, the server responds with `304 Not Modified` to indicate that the cached version is still valid and no data has changed.

- **Available Servers**: The API checks if the user is eligible to view servers using the `UserService`. If the user is available, it retrieves the list of servers using the `ServerService`.

**Fields in the Response:**

- `data`: 
  - An array of server objects. Each object includes:
    - `id`: The unique identifier of the server.
    - `name`: The name of the server.
    - `location`: The geographical location of the server.
    - `status`: The current status of the server (e.g., "active", "inactive").
    - `cache_key`: A unique key used for cache validation.

**Cache Handling:**

- **ETag Header**: The response includes an `ETag` header, which is a hash of the server data's cache key. This helps clients determine if the data has changed since the last fetch.

This API ensures efficient data retrieval and caching, reducing unnecessary data transfers and improving performance for users accessing server information.
Here’s a detailed explanation for the `StatController` and its `getTrafficLog` method.

## API Documentation

### 1. Get Traffic Log (`getTrafficLog`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/stat/getTrafficLog`  
**Query Parameters:**

- None.

**Headers:**

- `Authorization: Bearer {token}` (required)

**Example Request:**

```http
GET /api/v1/user/stat/getTrafficLog
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": [
        {
            "u": 1024,
            "d": 2048,
            "record_at": "2024-07-01T00:00:00Z",
            "user_id": 1,
            "server_rate": 0.5
        },
        {
            "u": 512,
            "d": 1024,
            "record_at": "2024-07-02T00:00:00Z",
            "user_id": 1,
            "server_rate": 0.5
        }
    ]
}
```

**Error Responses:**

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "Unable to retrieve traffic logs"
}
```

#### Description

The `getTrafficLog` method retrieves traffic statistics for the authenticated user. It focuses on data from the current month, based on the `record_at` timestamp.

- **Data Retrieval**: The method queries the `StatUser` model to fetch records where the `user_id` matches the authenticated user's ID and where `record_at` is from the beginning of the current month. The results are ordered by `record_at` in descending order.

**Fields in the Response:**

- `data`: 
  - An array of traffic log objects, each containing:
    - `u`: The amount of data uploaded by the user (in bytes).
    - `d`: The amount of data downloaded by the user (in bytes).
    - `record_at`: The timestamp when the record was created, formatted in ISO 8601.
    - `user_id`: The ID of the user the traffic log belongs to.
    - `server_rate`: A rate associated with the server during that record (e.g., bandwidth rate).

#### Key Concepts

1. **Traffic Logs**: These logs track the amount of data uploaded and downloaded by users. This information is crucial for understanding data usage patterns and managing server resources.

2. **Date Filtering**: The query filters records to include only those from the beginning of the current month. This approach helps in generating monthly reports or summaries.

3. **Timestamp Format**: The `record_at` field is typically in ISO 8601 format, which makes it easy to sort and filter dates programmatically.

By understanding these elements, you'll be better equipped to handle similar data retrieval tasks in your own applications. If you have any specific questions about the code or concepts, feel free to ask!

Here’s a detailed explanation for the `TelegramController` and its methods:

## API Documentation

### 1. Get Bot Information (`getBotInfo`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/user/telegram/getBotInfo`  
**Query Parameters:**

- None.

**Headers:**

- `Authorization: Bearer {token}` (required)

**Example Request:**

```http
GET /api/v1/user/telegram/getBotInfo
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": {
        "username": "your_bot_username"
    }
}
```

**Error Responses:**

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "Failed to retrieve bot information"
}
```

#### Description

The `getBotInfo` method retrieves the basic information about the Telegram bot. It uses the `TelegramService` to call the Telegram API’s `getMe` method, which provides details about the bot.

- **Data Retrieval**: The method calls `TelegramService`'s `getMe` function to fetch the bot's username.

**Fields in the Response:**

- `data`: 
  - `username`: The username of the Telegram bot as provided by the `getMe` API call.

#### Key Concepts

1. **Telegram API Integration**: This method interacts with the Telegram API to fetch information about the bot. It requires proper setup and credentials for the Telegram bot.

2. **Service Class Usage**: The `TelegramService` is used to encapsulate the logic of interacting with the Telegram API. This separation helps maintain cleaner code and better manage external integrations.

### 2. Unbind User (`unbind`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/user/telegram/unbind`  
**Query Parameters:**

- None.

**Headers:**

- `Authorization: Bearer {token}` (required)

**Request Body:**

- `None` (assuming this endpoint might use a different method to get necessary user data)

**Example Request:**

```http
POST /api/v1/user/telegram/unbind
Authorization: Bearer {token}
```

#### Response

**HTTP Status Code:** `200 OK`  
**Response Body:**

```json
{
    "data": "Successfully unbound"
}
```

**Error Responses:**

**HTTP Status Code:** `500 Internal Server Error`  
**Response Body:**

```json
{
    "message": "Failed to unbind user"
}
```

#### Description

The `unbind` method is intended to unbind a user's Telegram account from the system. However, the method implementation is incomplete as it only retrieves the user object from the database and does not perform any actions. The expected functionality should include removing or updating the user's Telegram binding status.

- **Data Retrieval**: The method fetches the user from the database based on the `user_id` provided in the request.

**Fields in the Response:**

- `data`: 
  - A confirmation message indicating the result of the unbinding process (although the current implementation does not perform the actual unbinding).

#### Key Concepts

1. **User Management**: Unbinding a user’s Telegram account typically involves updating user records to remove or alter Telegram-related data.

2. **Incomplete Implementation**: The current method fetches the user but lacks further logic to unbind or update the user’s status. This method should be extended to include logic for unbinding.

### Summary

- **`getBotInfo`**: Retrieves the bot's username using the Telegram API.
- **`unbind`**: Currently retrieves a user but does not perform any action. The implementation is incomplete and needs additional logic to unbind a user's Telegram account.

Feel free to ask if you need further details or have specific questions about the code!
Here's a detailed explanation for the `TelegramController` class and its methods:

## API Documentation

### Overview

The `TelegramController` handles interactions with the Telegram API, specifically dealing with webhooks related to messages and chat join requests. It uses the `TelegramService` to communicate with Telegram and process commands or manage chat join requests.

### 1. Constructor (`__construct`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/guest/telegram/webhook`  
**Query Parameters:**

- None.

**Headers:**

- `Content-Type: application/json` (typically for webhooks)

**Request Body:**

- JSON payload from Telegram's webhook.

**Example Request:**

```http
POST /api/v1/guest/telegram/webhook?access_token={token}
Content-Type: application/json

{
    "message": {
        "text": "/start",
        "chat": {
            "id": 123456789,
            "type": "private"
        },
        "message_id": 1
    }
}
```

#### Description

The constructor checks if the provided `access_token` matches the hashed bot token configured in the `v2board.telegram_bot_token` setting. If it doesn't match, it aborts with a 401 Unauthorized error.

### 2. Webhook Handler (`webhook`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/guest/telegram/webhook`  
**Query Parameters:**

- None.

**Headers:**

- `Content-Type: application/json`

**Request Body:**

- JSON payload from Telegram's webhook.

**Example Request:**

```http
POST /api/v1/guest/telegram/webhook?access_token={token}
Content-Type: application/json

{
    "message": {
        "text": "/start",
        "chat": {
            "id": 123456789,
            "type": "private"
        },
        "message_id": 1
    }
}
```

#### Description

This method processes the incoming webhook data:

1. **Formats the Message**: Calls `formatMessage` to transform the incoming message data into a standardized format.
2. **Formats Chat Join Requests**: Calls `formatChatJoinRequest` to handle any chat join requests.
3. **Handles Commands**: Calls `handle` to process the formatted message and execute relevant commands.

### 3. Handle Commands (`handle`)

#### Request

- No direct request. This method is invoked by `webhook`.

#### Description

Processes the formatted message and executes the appropriate command:

1. **Command Parsing**: If the command contains a bot name (e.g., `/start@botname`), it verifies and strips out the bot name.
2. **Command Execution**: Iterates over all command classes in the `Commands` directory and executes the command handler if the command matches.
3. **Error Handling**: Catches any exceptions and sends an error message to the Telegram chat.

### 4. Get Bot Name (`getBotName`)

#### Request

- No direct request. This method is called within `handle`.

#### Description

Retrieves the bot's username from Telegram using the `TelegramService`.

**Response:**

- Returns the bot's username.

### 5. Format Message (`formatMessage`)

#### Request

- No direct request. This method is invoked by `webhook`.

#### Description

Transforms the incoming message data into a standardized format:

1. **Extract Command and Arguments**: Splits the message text to identify the command and arguments.
2. **Identify Message Type**: Determines whether the message is a regular message or a reply to another message.
3. **Sets Message Object**: Stores the processed message data in an object.

### 6. Format Chat Join Request (`formatChatJoinRequest`)

#### Request

- No direct request. This method is invoked by `webhook`.

#### Description

Handles chat join requests:

1. **Check User**: Verifies if the user making the request exists in the system.
2. **Approve or Decline**: Approves or declines the chat join request based on the user's status.

### Key Concepts

- **Webhook Integration**: The controller integrates with Telegram's webhook system to receive and process updates.
- **Command Handling**: Commands are handled dynamically by iterating over command classes, allowing for modular command implementations.
- **Chat Join Requests**: Manages the approval or rejection of users trying to join Telegram chats based on their subscription status.

### Summary

- **`__construct`**: Validates the access token.
- **`webhook`**: Handles incoming webhook data and processes messages or chat join requests.
- **`handle`**: Executes the relevant command based on the message.
- **`getBotName`**: Retrieves the bot's username.
- **`formatMessage`**: Formats incoming messages into a standardized format.
- **`formatChatJoinRequest`**: Handles chat join requests based on user status.

Feel free to ask if you have more questions or need further details!

Here's an overview of the `PaymentController` class and its methods, which handle payment notifications and order processing:

## API Documentation

### Overview

The `PaymentController` is responsible for handling payment notifications from various payment methods, processing the payment, and sending notifications to administrators about successful transactions.

### 1. Notify Payment (`notify`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/guest/payment/notify/{method}/{uuid}`  
**Path Parameters:**

- `method`: The payment method used (e.g., `stripe`, `paypal`).
- `uuid`: A unique identifier for the payment method or transaction.

**Headers:**

- `Content-Type: application/json` (typically for notifications)

**Request Body:**

- JSON payload from the payment gateway containing payment details.

**Example Request:**

```http
POST /api/v1/guest/payment/notify/stripe/123e4567-e89b-12d3-a456-426614174000
Content-Type: application/json

{
    "trade_no": "txn_123456",
    "callback_no": "callback_123456",
    "amount": 10000,
    "status": "success"
}
```

#### Description

Handles payment notifications from the payment gateway:

1. **Initialize PaymentService**: Creates an instance of `PaymentService` with the provided method and UUID.
2. **Verify Notification**: Calls `notify` method of `PaymentService` to verify the payment notification.
3. **Handle Payment**: If verification is successful, it processes the payment and updates the order status.
4. **Send Response**: Responds with a custom result or "success" if everything is correct.
5. **Exception Handling**: Catches and handles any exceptions, returning a failure message.

#### Response

- **Success:** A success message or custom result from the payment service.
- **Failure:** HTTP 500 Internal Server Error if verification or handling fails.

### 2. Handle Payment (`handle`)

#### Description

Processes the payment and updates the order status:

1. **Find Order**: Retrieves the order based on `tradeNo`.
2. **Check Order Status**: If the order is already processed (`status` is not `0`), the method returns `true`.
3. **Process Payment**: If the order is not yet paid, it calls the `paid` method of `OrderService` to update the order status.
4. **Send Telegram Notification**: Sends a message to the admin via Telegram about the successful payment.

**Dependencies:**

- **OrderService**: Handles updating the order status.
- **TelegramService**: Sends a notification message to administrators.

#### Response

- **Success:** Returns `true` if the order was successfully updated and the notification was sent.
- **Failure:** Returns `false` if processing or notification fails.

### Key Concepts

- **Payment Notification**: The controller processes payment notifications received from different payment methods.
- **Order Processing**: Updates the order status based on the payment information.
- **Administrator Notification**: Uses Telegram to notify administrators about successful payments.

### Summary

- **`notify`**: Handles incoming payment notifications, verifies them, processes the order, and sends a notification to administrators.
- **`handle`**: Updates the order status based on payment information and sends a Telegram message about the successful payment.

Feel free to ask if you need more details or have other questions!

Here's an overview of the `CommController` class, which is responsible for providing configuration settings to guests:

## API Documentation

### Overview

The `CommController` class serves endpoints to retrieve configuration settings related to the application. It provides various configuration details such as URLs, verification settings, and application information.

### 1. Configuration (`config`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/guest/comm/config`

**Headers:**

- `Accept: application/json` (default for API responses)

#### Description

This method returns the configuration settings of the application, including:

- **Terms of Service URL (`tos_url`)**: The URL to the terms of service.
- **Email Verification (`is_email_verify`)**: Indicates if email verification is required. Returns `1` if enabled, otherwise `0`.
- **Invite Force (`is_invite_force`)**: Indicates if an invitation is required to access the service. Returns `1` if enabled, otherwise `0`.
- **Email Whitelist Suffix (`email_whitelist_suffix`)**: Returns a list of allowed email suffixes if email whitelist is enabled, otherwise `0`.
- **reCAPTCHA (`is_recaptcha`)**: Indicates if reCAPTCHA is enabled. Returns `1` if enabled, otherwise `0`.
- **reCAPTCHA Site Key (`recaptcha_site_key`)**: The site key for reCAPTCHA.
- **App Description (`app_description`)**: A description of the application.
- **App URL (`app_url`)**: The URL of the application.
- **Logo (`logo`)**: URL or path to the application logo.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "tos_url": "https://example.com/tos",
        "is_email_verify": 1,
        "is_invite_force": 0,
        "email_whitelist_suffix": ["example.com", "test.com"],
        "is_recaptcha": 1,
        "recaptcha_site_key": "your-recaptcha-site-key",
        "app_description": "Your app description here",
        "app_url": "https://example.com",
        "logo": "https://example.com/logo.png"
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` (in case of unexpected issues)

### 2. Email Whitelist Suffix Helper (`getEmailSuffix`)

#### Description

This private method retrieves the email whitelist suffixes. It handles the configuration value, which could be a comma-separated string or an array. It converts the configuration value into an array of suffixes.

**Logic:**

1. **Check Type**: If the configuration value is not an array, it splits the string by commas to form an array.
2. **Return Array**: Returns the array of email suffixes.

**Dependencies:**

- **Dict**: Used to provide a default value for the email whitelist suffix.

### Summary

- **`config`**: Provides application configuration settings for guests.
- **`getEmailSuffix`**: Helper method to process email whitelist suffixes.

This controller is mainly used to expose configuration settings relevant to guest users, which helps in setting up or customizing the application based on the provided configuration. If you have any specific questions or need further details, feel free to ask!

Here's an overview of the `UserController` class, which manages user-related operations for staff:

## API Documentation

### Overview

The `UserController` class provides endpoints for managing user information, updating user details, sending emails to users, and banning users. It is designed for use by staff members and performs operations such as retrieving user information, updating user records, and handling bulk actions like sending emails or banning users.

### 1. Get User Info by ID (`getUserInfoById`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/staff/user/info`

**Parameters:**

- **id** (required): The ID of the user whose information is to be retrieved.

**Headers:**

- `Accept: application/json` (default for API responses)

#### Description

This method retrieves information for a specific user by ID. It ensures that the user is not an admin or staff member, as these types are excluded from this endpoint.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "id": 1,
        "email": "user@example.com",
        "name": "John Doe",
        "is_admin": 0,
        "is_staff": 0,
        // Additional user fields
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error`
- **Error Messages:**
  - "参数错误" (Parameter error) if the ID is missing.
  - "用户不存在" (User does not exist) if the user is not found.

### 2. Update User (`update`)

#### Request

**HTTP Method:** `PUT`  
**URL:** `/api/v1/staff/user/update`

**Parameters:**

- **id** (required): The ID of the user to update.
- **email**: The new email address of the user.
- **password**: The new password for the user.
- **plan_id**: The ID of the subscription plan to assign to the user.

**Headers:**

- `Accept: application/json` (default for API responses)
- `Content-Type: application/json`

#### Description

This method updates user details based on the provided parameters. It handles email uniqueness, password hashing, and plan assignment.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error`
- **Error Messages:**
  - "用户不存在" (User does not exist) if the user is not found.
  - "邮箱已被使用" (Email already in use) if the email is already taken.
  - "订阅计划不存在" (Subscription plan does not exist) if the plan is not found.
  - "保存失败" (Save failed) if the update operation fails.

### 3. Send Mail (`sendMail`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/staff/user/send-mail`

**Parameters:**

- **subject** (required): The subject of the email.
- **content** (required): The content of the email.
- **sort**: Field to sort the users by (default is `created_at`).
- **sort_type**: Sorting order (`ASC` or `DESC`, default is `DESC`).

**Headers:**

- `Accept: application/json` (default for API responses)
- `Content-Type: application/json`

#### Description

This method sends an email to all users based on the provided criteria. It uses the `SendEmailJob` to dispatch email sending tasks.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

### 4. Ban Users (`ban`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/staff/user/ban`

**Parameters:**

- **sort**: Field to sort the users by (default is `created_at`).
- **sort_type**: Sorting order (`ASC` or `DESC`, default is `DESC`).

**Headers:**

- `Accept: application/json` (default for API responses)
- `Content-Type: application/json`

#### Description

This method bans users based on the provided sorting and filtering criteria. It updates the `banned` field to `1` for all users matching the criteria.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error`
- **Error Messages:**
  - "处理失败" (Processing failed) if the update operation fails.

### Summary

- **`getUserInfoById`**: Retrieve detailed information about a user by ID.
- **`update`**: Update user details, including email, password, and plan.
- **`sendMail`**: Send bulk emails to users based on specified criteria.
- **`ban`**: Ban users based on sorting and filtering criteria.

This controller provides essential functionality for managing user accounts and performing bulk operations related to users. If you have further questions or need additional information, feel free to ask!

Here's a detailed overview of the `AuthController` class, which handles authentication-related operations for users:

## API Documentation

### Overview

The `AuthController` class provides various endpoints related to user authentication, including login, registration, password reset, and quick login. It also handles rate limiting, CAPTCHA verification, and email-based login links.

### 1. Login with Mail Link (`loginWithMailLink`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/passport/login-with-mail-link`

**Parameters:**

- **email** (required): The email address of the user.
- **redirect** (optional): URL to redirect to after login.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Sends a login link to the user's email if email-based login is enabled. The link includes a temporary token for logging in.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": "https://your-app-url/#/login?verify=token&redirect=dashboard"
}
```

**Failure:**

- **HTTP Status Code:** `404 Not Found` if email-based login is not enabled.
- **HTTP Status Code:** `500 Internal Server Error` for various errors, such as frequent requests or other failures.

### 2. Register (`register`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/passport/register`

**Parameters:**

- **email** (required): The email address of the user.
- **password** (required): The password for the user.
- **invite_code** (optional): Invitation code for registration.
- **email_code** (optional): Email verification code.
- **recaptcha_data** (optional): CAPTCHA data if reCAPTCHA is enabled.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Registers a new user with the provided email and password, checking various conditions like email verification, invitation code validity, and CAPTCHA.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "token": "generated-auth-token",
        "expires_in": 3600
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` for various errors, such as invalid email verification code or registration limits.

### 3. Login (`login`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/passport/login`

**Parameters:**

- **email** (required): The email address of the user.
- **password** (required): The password for the user.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Logs in a user with the provided email and password, implementing password error limits and checking if the account is banned.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "token": "generated-auth-token",
        "expires_in": 3600
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` for invalid email/password or account suspension.

### 4. Token2Login (`token2Login`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/passport/token2-login`

**Parameters:**

- **token** (optional): The temporary token for login.
- **verify** (optional): The token used for verification.

**Headers:**

- `Accept: application/json`

#### Description

Handles login via a token, either redirecting to a login page with a token or verifying a provided token for authentication.

#### Response

**Success:**

- **HTTP Status Code:** `302 Found` for redirects.
- **HTTP Status Code:** `200 OK` for successful token verification.

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` for invalid tokens or user issues.

### 5. Get Quick Login URL (`getQuickLoginUrl`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/passport/get-quick-login-url`

**Parameters:**

- **auth_data** (optional): Authorization data for generating a quick login URL.
- **redirect** (optional): URL to redirect to after login.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Generates a quick login URL for an authenticated user, allowing for fast login without entering credentials.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": "https://your-app-url/#/login?verify=token&redirect=dashboard"
}
```

**Failure:**

- **HTTP Status Code:** `403 Forbidden` if the user is not authenticated.

### 6. Forget Password (`forget`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/passport/forget`

**Parameters:**

- **email** (required): The email address of the user.
- **email_code** (required): Email verification code.
- **password** (required): New password for the user.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Handles password reset requests, verifying the email and code before allowing the user to set a new password.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` for verification issues or reset failures.

### Summary

- **`loginWithMailLink`**: Sends a login link via email.
- **`register`**: Handles user registration, including various validation checks.
- **`login`**: Authenticates a user with email and password.
- **`token2Login`**: Logs in users via a temporary token.
- **`getQuickLoginUrl`**: Generates a quick login URL for authenticated users.
- **`forget`**: Resets the user's password after verifying email and code.

This controller manages authentication workflows, including registration, login, and password management, with additional security measures like CAPTCHA and rate limiting. If you have any questions or need further details, feel free to ask!

Here’s an overview of the `CommController` class, which manages common functionalities related to email verification and invite code statistics:

## API Documentation

### Overview

The `CommController` class provides methods for:
1. Email verification code management.
2. Tracking the number of times an invite code is viewed.
3. Fetching email suffixes for whitelist validation.

### 1. Email Verification (`sendEmailVerify`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/passport/send-email-verify`

**Parameters:**

- **email** (required): The email address to which the verification code will be sent.
- **recaptcha_data** (optional): CAPTCHA data for reCAPTCHA verification (if enabled).

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Sends an email verification code to the provided email address, with reCAPTCHA verification if enabled. Implements a cooldown period to prevent spammy requests.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `429 Too Many Requests` if requests are too frequent.
- **HTTP Status Code:** `500 Internal Server Error` for CAPTCHA failures or other issues.

#### Error Messages

- **429 Too Many Requests:** "Слишком много попыток! Попробуйте через X секунд"
- **500 Internal Server Error:** "Invalid code is incorrect"

### 2. Track Invite Code Views (`pv`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/passport/pv`

**Parameters:**

- **invite_code** (required): The invite code to be tracked.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Increments the view count for the specified invite code.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if invite code does not exist or other issues occur.

### 3. Get Email Suffixes (`getEmailSuffix`)

#### Request

**HTTP Method:** N/A (Private method, not exposed via an endpoint)

**Parameters:**

- **None**

**Headers:**

- N/A

#### Description

Fetches the list of allowed email suffixes for whitelist validation. Used internally for validating email addresses against a whitelist.

**Returns:**

- **Type:** `array` of email suffixes.

**Example:**

```php
[
    'example.com',
    'anotherdomain.com'
]
```

### Summary

- **`sendEmailVerify`**: Sends a verification code to the provided email and implements rate limiting and CAPTCHA if configured.
- **`pv`**: Tracks the number of times an invite code has been viewed.
- **`getEmailSuffix`**: Provides a list of allowed email suffixes for validation.

The `CommController` class focuses on common email and invite code operations, ensuring security with CAPTCHA and cooldown periods, and allowing for tracking of invite code usage. If you need more details or have specific questions, feel free to ask!
Here’s an overview of the `UserController` class from your Laravel application. This controller manages user-related functionalities in the admin panel.

## API Documentation

### Overview

The `UserController` class provides methods for:
1. Resetting user secrets.
2. Filtering and fetching user data.
3. Retrieving user information by ID.
4. Updating user details.
5. Exporting user data to CSV.
6. Generating new user accounts.
7. Sending emails to users.
8. Banning users.
9. Deleting users and their related data.

### 1. Reset User Secret (`resetSecret`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/user/reset-secret`

**Parameters:**

- **id** (required): The ID of the user whose secrets will be reset.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Resets the user's token and UUID.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the user does not exist.

### 2. Fetch Users (`fetch`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/user/fetch`

**Parameters:**

- **current** (optional): Page number for pagination (default is 1).
- **pageSize** (optional): Number of users per page (minimum is 10).
- **sort_type** (optional): Sorting order, either `ASC` or `DESC` (default is `DESC`).
- **sort** (optional): Field to sort by (default is `created_at`).
- **filter** (optional): Array of filters to apply to the query.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Fetches a paginated and filtered list of users.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "email": "user@example.com",
            "balance": 100,
            "commission_balance": 10,
            "transfer_enable": 5,
            "device_limit": 3,
            "not_use_flow": 1,
            "expire_date": "2024-12-31 23:59:59",
            "plan_name": "Premium",
            "subscribe_url": "http://example.com/subscribe"
        }
    ],
    "total": 1
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` for internal errors.

### 3. Get User Info by ID (`getUserInfoById`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/user/get-user-info-by-id`

**Parameters:**

- **id** (required): The ID of the user whose information is being requested.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Fetches user information by ID.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "id": 1,
        "email": "user@example.com",
        "invite_user": {
            "id": 2,
            "email": "inviter@example.com"
        }
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if parameters are incorrect or user does not exist.

### 4. Update User (`update`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/user/update`

**Parameters:**

- **id** (required): The ID of the user to update.
- **email** (optional): New email for the user.
- **password** (optional): New password for the user.
- **plan_id** (optional): ID of the new subscription plan.
- **invite_user_email** (optional): Email of the user who invited this user.
- **banned** (optional): Ban status (`1` to ban, `0` to unban).

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Updates user information including email, password, subscription plan, and ban status.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the user does not exist or update fails.

### 5. Export Users to CSV (`dumpCSV`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/user/dump-csv`

**Parameters:**

- **filter** (optional): Filters to apply to the exported data.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Exports user data to a CSV file.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `text/csv`

**Example Response:**

```csv
邮箱,余额,推广佣金,总流量,设备数限制,剩余流量,套餐到期时间,订阅计划,订阅地址
user@example.com,100,10,5,3,1,2024-12-31 23:59:59,Premium,http://example.com/subscribe
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` for internal errors.

### 6. Generate User (`generate`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/user/generate`

**Parameters:**

- **email_prefix** (required): Prefix for the user's email.
- **email_suffix** (required): Suffix for the user's email.
- **plan_id** (optional): ID of the subscription plan.
- **expired_at** (optional): Expiration date for the user's account.
- **password** (optional): Password for the user.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Generates a new user account. Can also generate multiple accounts.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the email already exists or generation fails.

### 7. Send Mail (`sendMail`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/user/send-mail`

**Parameters:**

- **subject** (required): Subject of the email.
- **content** (required): Content of the email.
- **sort_type** (optional): Sorting order, either `ASC` or `DESC` (default is `DESC`).
- **sort** (optional): Field to sort by (default is `created_at`).
- **filter** (optional): Filters to apply to the email recipients.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Sends an email to users matching the provided filters.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` for internal errors.

### 8. Ban Users (`ban`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/user/ban`

**Parameters:**

- **sort_type** (optional): Sorting order, either `ASC` or `DESC` (default is `DESC`).
- **sort** (optional): Field to sort by (default is `created_at`).
- **filter** (optional): Filters to apply to the users to be banned.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Bans users matching the provided filters.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` for internal errors.

### 9. Delete Users (`allDel` and `delUser`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/user/all-del` (for bulk delete)  
**URL:** `/api/v1/admin/user/del-user` (for single delete)

**Parameters:**

- **id** (required for single delete): The ID of the user to delete.
- **filter** (optional for bulk delete): Filters to apply to the users to be deleted.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Deletes a single user or multiple users, along with their related data like orders and invite relationships.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
-

 **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if deletion fails.

This comprehensive documentation should help with understanding and using the `UserController` methods effectively in your API. If you have further questions or need additional details, feel free to ask!

The `TicketController` class in your Laravel application handles ticket-related functionalities. Here’s a detailed overview of its methods and their usage:

## API Documentation

### Overview

The `TicketController` class manages:
1. Fetching ticket details and listing tickets.
2. Replying to tickets.
3. Closing tickets.

### 1. Fetch Tickets (`fetch`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/ticket/fetch`

**Parameters:**

- **id** (optional): The ID of a specific ticket to retrieve.
- **current** (optional): Page number for pagination (default is 1).
- **pageSize** (optional): Number of tickets per page (minimum is 10).
- **status** (optional): Filter tickets by status.
- **reply_status** (optional): Filter tickets by reply status.
- **email** (optional): Filter tickets by user email.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

- **If `id` is provided:** Retrieves a specific ticket along with its messages. Marks messages as sent by the user or admin based on the user ID.
- **If `id` is not provided:** Fetches a list of tickets with optional filters and pagination.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "id": 1,
            "status": 0,
            "updated_at": "2024-07-24T12:34:56",
            "message": [
                {
                    "id": 1,
                    "user_id": 2,
                    "content": "Message content",
                    "is_me": true
                }
            ]
        }
    ],
    "total": 1
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error retrieving the ticket or if required parameters are missing.

### 2. Reply to Ticket (`reply`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/ticket/reply`

**Parameters:**

- **id** (required): The ID of the ticket to reply to.
- **message** (required): The reply message content.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Replies to a ticket as an admin. The ticket's reply is processed through the `TicketService`.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if parameters are missing or if an error occurs during the reply process.

### 3. Close Ticket (`close`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/ticket/close`

**Parameters:**

- **id** (required): The ID of the ticket to close.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Closes a specific ticket by setting its status to `1` (closed).

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the ticket does not exist or if closing the ticket fails.

### Error Handling

In all methods, `abort(500, 'message')` is used to indicate errors. Customize these messages to fit your application's needs and localization.

### Summary

- **`fetch`**: Retrieves tickets with optional filters and pagination or specific ticket details.
- **`reply`**: Sends a reply to a ticket.
- **`close`**: Closes a ticket by updating its status.

This documentation should help you understand and integrate the `TicketController` functionalities into your admin panel. If you need more information or have additional questions, feel free to ask!

The `ThemeController` class in your Laravel application handles theme-related functionalities, including retrieving, saving, and managing theme configurations. Here's a detailed overview of its methods:

## API Documentation

### Overview

The `ThemeController` class manages:
1. Retrieving available themes and their configurations.
2. Fetching configuration for a specific theme.
3. Saving updated configuration for a theme.

### 1. Get Available Themes (`getThemes`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/theme/getThemes`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Retrieves a list of available themes and their configurations. It also initializes any theme that has not been configured yet.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "themes": {
            "theme1": {
                "name": "Theme 1",
                "configs": [
                    {
                        "field_name": "color_scheme",
                        "default": "dark"
                    }
                ]
            }
        },
        "active": "v2board"
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error retrieving the theme configurations.

### 2. Get Theme Configuration (`getThemeConfig`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/theme/getThemeConfig`

**Parameters:**

- **name** (required): The name of the theme to retrieve the configuration for.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Fetches the current configuration for a specific theme.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "color_scheme": "dark",
        "font_size": "medium"
    }
}
```

**Failure:**

- **HTTP Status Code:** `400 Bad Request` if the `name` parameter is invalid.
- **HTTP Status Code:** `500 Internal Server Error` if there is an error retrieving the configuration.

### 3. Save Theme Configuration (`saveThemeConfig`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/theme/saveThemeConfig`

**Parameters:**

- **name** (required): The name of the theme to update.
- **config** (required): Base64-encoded JSON string containing the new configuration.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Saves the updated configuration for a specific theme. It validates and processes the provided configuration, then saves it to the configuration file.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "color_scheme": "light",
        "font_size": "large"
    }
}
```

**Failure:**

- **HTTP Status Code:** `400 Bad Request` if the `name` or `config` parameters are invalid.
- **HTTP Status Code:** `500 Internal Server Error` if there are errors in saving the configuration or updating the cache.

### Error Handling

- **500 Internal Server Error** is used to handle unexpected errors or failures in file operations, theme configuration validations, or cache updates.

### Summary

- **`getThemes`**: Retrieves a list of all available themes and their configurations, initializing themes if needed.
- **`getThemeConfig`**: Fetches the configuration of a specific theme.
- **`saveThemeConfig`**: Updates and saves the configuration of a specific theme, with validation and caching.

This documentation should help you understand and integrate theme management functionalities into your admin panel. If you have further questions or need more details, feel free to ask!

The `SystemController` class in your Laravel application is responsible for managing and providing information about system status, queue workload, and logs. Here’s a breakdown of its functionalities:

## API Documentation

### Overview

The `SystemController` class provides endpoints to:
1. Retrieve system status and scheduling details.
2. Get details about the queue workload.
3. Fetch statistics related to the queue and Horizon (Laravel's queue manager).
4. Retrieve system logs.

### 1. Get System Status (`getSystemStatus`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/system/status`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Returns the overall system status including the status of the scheduled tasks, Horizon, and the last time the schedule was checked.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "schedule": true,
        "horizon": true,
        "schedule_last_runtime": "2024-07-24T12:34:56Z"
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error fetching system status.

### 2. Get Queue Workload (`getQueueWorkload`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/system/queue-workload`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

**Parameters:**

- **workloadRepository** (optional): Instance of the `WorkloadRepository` class.

#### Description

Retrieves the workload distribution of the queue, sorted by name.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "name": "high_priority",
            "jobs": 10
        },
        {
            "name": "low_priority",
            "jobs": 5
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error fetching queue workload.

### 3. Get Queue Stats (`getQueueStats`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/system/queue-stats`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Provides statistics related to the queue system, including failed jobs, jobs per minute, paused masters, and wait times.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "failedJobs": 2,
        "jobsPerMinute": 15,
        "pausedMasters": 1,
        "periods": {
            "failedJobs": 100,
            "recentJobs": 50
        },
        "processes": 12,
        "queueWithMaxRuntime": "high_priority",
        "queueWithMaxThroughput": "default",
        "recentJobs": 20,
        "status": true,
        "wait": [
            {
                "queue": "default",
                "time": 30
            }
        ]
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error retrieving queue statistics.

### 4. Get System Log (`getSystemLog`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/system/logs`

**Parameters:**

- **current** (optional): Page number for pagination.
- **page_size** (optional): Number of logs per page.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Fetches system logs with pagination. Allows filtering based on log level.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "id": 1,
            "level": "error",
            "message": "Failed to connect to database.",
            "created_at": "2024-07-24T12:34:56Z"
        },
        {
            "id": 2,
            "level": "info",
            "message": "Scheduled task executed successfully.",
            "created_at": "2024-07-24T12:00:00Z"
        }
    ],
    "total": 2
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error fetching system logs.

### Error Handling

- **500 Internal Server Error** is used for unexpected errors or failures in fetching system information or processing requests.

### Summary

- **`getSystemStatus`**: Provides a summary of the system’s status, including scheduling and Horizon.
- **`getQueueWorkload`**: Retrieves the distribution of workload across queues.
- **`getQueueStats`**: Provides detailed statistics about queue processing, Horizon status, and job wait times.
- **`getSystemLog`**: Fetches paginated system logs with optional filtering.

Feel free to ask if you need more details or have any other questions!
The `StatController` class in your Laravel application manages various statistical data related to server usage, user activity, and system performance. Here’s a detailed explanation of each method in the controller:

## API Documentation

### Overview

The `StatController` class provides endpoints for:
1. Retrieving overall statistics and metrics.
2. Getting ranking information for servers and users.
3. Fetching statistics related to specific users.

### 1. Get Override Statistics (`getOverride`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/statistics/override`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Returns various statistics such as monthly income, registration totals, pending tickets, and commission payouts.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "month_income": 1000.00,
        "month_register_total": 150,
        "ticket_pending_total": 10,
        "commission_pending_total": 5,
        "day_income": 50.00,
        "last_month_income": 800.00,
        "commission_month_payout": 200.00,
        "commission_last_month_payout": 150.00
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error processing the statistics.

### 2. Get Order Statistics (`getOrder`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/statistics/orders`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Provides daily statistics on payments and commissions over the past 31 days.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "type": "收款金额",
            "date": "07-23",
            "value": 120.00
        },
        {
            "type": "收款笔数",
            "date": "07-23",
            "value": 3
        },
        {
            "type": "佣金金额(已发放)",
            "date": "07-23",
            "value": 30.00
        },
        {
            "type": "佣金笔数(已发放)",
            "date": "07-23",
            "value": 1
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error fetching the statistics.

### 3. Get Server Ranking for Last Day (`getServerLastRank`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/statistics/server-last-rank`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Retrieves server usage statistics for the last day and ranks servers based on total data usage.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "server_id": 1,
            "server_type": "shadowsocks",
            "u": 5000000000,
            "d": 3000000000,
            "total": 7.45,
            "server_name": "Server A"
        },
        {
            "server_id": 2,
            "server_type": "v2ray",
            "u": 2000000000,
            "d": 1000000000,
            "total": 2.79,
            "server_name": "Server B"
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error retrieving server statistics.

### 4. Get Server Ranking for Today (`getServerTodayRank`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/statistics/server-today-rank`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Retrieves server usage statistics for today and ranks servers based on total data usage.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "server_id": 1,
            "server_type": "shadowsocks",
            "u": 2000000000,
            "d": 1000000000,
            "total": 2.79,
            "server_name": "Server A"
        },
        {
            "server_id": 2,
            "server_type": "v2ray",
            "u": 1000000000,
            "d": 500000000,
            "total": 1.32,
            "server_name": "Server B"
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error retrieving server statistics.

### 5. Get User Ranking for Today (`getUserTodayRank`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/statistics/user-today-rank`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Retrieves and ranks users based on their data usage for today.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "user_id": 1,
            "email": "user@example.com",
            "total": 5.25
        },
        {
            "user_id": 2,
            "email": "anotheruser@example.com",
            "total": 3.00
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error retrieving user statistics.

### 6. Get User Ranking for Last Day (`getUserLastRank`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/statistics/user-last-rank`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Retrieves and ranks users based on their data usage for the last day.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "user_id": 1,
            "email": "user@example.com",
            "total": 4.50
        },
        {
            "user_id": 2,
            "email": "anotheruser@example.com",
            "total": 2.75
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an error retrieving user statistics.

### 7. Get User Statistics (`getStatUser`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/statistics/user`

**Parameters:**

- **user_id** (required): The ID of the user for whom the statistics are being retrieved.
- **current** (optional): Page number for pagination.
- **pageSize** (optional): Number of records per page.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Fetches statistical records for a specific user with pagination support.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "record_at": "2024-07-24",
            "u": 1000000000,
            "d": 500000000,
            "total": 1.40
        }
    ],
    "total": 10
}
```

**Failure:**

- **HTTP Status Code:** `400 Bad Request` if the `user_id` parameter is invalid.
- **HTTP Status Code:** `500 Internal Server Error` if there is an error retrieving user statistics.

### Error Handling

- **500 Internal Server Error** is used for unexpected errors or failures in fetching or processing statistics.
- **400 Bad Request** is used for validation errors (e.g., missing or invalid `user_id`).

### Summary

- **`getOverride`**: Provides general system statistics like income, registration totals, and commission payouts.
- **`getOrder`**: Provides daily statistics on payments and commissions.
- **`getServerLastRank`**: Retrieves server rankings for the last day based on data usage.
- **`getServerTodayRank`**: Retrieves server rankings for today based on data usage.
- **`getUserTodayRank`**: Retrieves user rankings for today based on data usage.
- **`getUserLastRank`**: Retrieves user rankings for the last day based on data usage.
- **`getStatUser`**: Retrieves statistical records for a specific user with pagination.

Feel free to ask if you need further details or have additional questions!
The `PlanController` class in your Laravel application is responsible for managing subscription plans. It includes methods to fetch, save, delete, update, and sort plans. Below is a detailed explanation of each method, including request and response formats:

## API Documentation

### Overview

The `PlanController` class handles operations related to subscription plans, including CRUD operations and sorting.

### 1. Fetch Plans (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/plans`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Fetches all subscription plans, ordered by their sorting index, and includes the count of active users for each plan.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "id": 1,
            "name": "Basic Plan",
            "price": 9.99,
            "group_id": 1,
            "transfer_enable": 2147483648,
            "device_limit": 3,
            "speed_limit": 100,
            "sort": 1,
            "count": 15
        },
        {
            "id": 2,
            "name": "Pro Plan",
            "price": 19.99,
            "group_id": 2,
            "transfer_enable": 4294967296,
            "device_limit": 5,
            "speed_limit": 200,
            "sort": 2,
            "count": 8
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an issue fetching the data.

### 2. Save Plan (`save`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/plans/save`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

**Parameters:**

- `id` (optional): The ID of the plan to update. If not provided, a new plan is created.
- `name`: The name of the plan.
- `price`: The price of the plan.
- `group_id`: The group ID associated with the plan.
- `transfer_enable`: The data transfer limit for the plan (in GB).
- `device_limit`: The device limit for the plan.
- `speed_limit`: The speed limit for the plan.
- `force_update` (optional): Whether to force update user details.

#### Description

Creates a new subscription plan or updates an existing one. If `force_update` is set to true, updates user details associated with the plan.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the operation fails (e.g., due to validation errors or database issues).

### 3. Drop Plan (`drop`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/plans/drop`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

**Parameters:**

- `id`: The ID of the plan to delete.

#### Description

Deletes a subscription plan if no orders or users are associated with it.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there are orders or users associated with the plan, or if the plan cannot be found.

### 4. Update Plan (`update`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/plans/update`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

**Parameters:**

- `id`: The ID of the plan to update.
- `show`: Whether the plan should be visible.
- `renew`: Whether the plan should be renewable.

#### Description

Updates specific attributes of a subscription plan.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the plan does not exist or the update fails.

### 5. Sort Plans (`sort`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/plans/sort`

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

**Parameters:**

- `plan_ids`: An array of plan IDs ordered as per the desired sorting.

#### Description

Updates the sorting index for the subscription plans.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the sorting update fails.

### Error Handling

- **500 Internal Server Error** is used for unexpected errors, such as issues with database transactions or operations that fail validation.

### Summary

- **`fetch`**: Retrieves and returns all subscription plans with active user counts.
- **`save`**: Creates a new plan or updates an existing one, optionally forcing updates to associated users.
- **`drop`**: Deletes a plan if it has no associated orders or users.
- **`update`**: Updates specific attributes of a plan.
- **`sort`**: Updates the sorting index of the plans.

Feel free to reach out if you have more questions or need further clarification!
The `PaymentController` class in your Laravel application manages payment methods. It includes methods for fetching payment methods, handling forms, and managing payment configurations. Here’s a detailed breakdown of each method:

## API Documentation

### Overview

The `PaymentController` class deals with operations related to payment methods. It provides functionalities to fetch, save, update, delete, and sort payment methods.

### 1. Get Payment Methods (`getPaymentMethods`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/payment/methods`

**Headers:**

- `Accept: application/json`

#### Description

Retrieves a list of available payment method classes by scanning the `app/Payments` directory.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        "Stripe",
        "PayPal",
        "BankTransfer"
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an issue fetching the payment methods.

### 2. Fetch Payment Methods (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/payment`

**Headers:**

- `Accept: application/json`

#### Description

Fetches all payment methods from the database and returns their details. The method also generates and includes the notify URL for each payment method.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "id": 1,
            "name": "Stripe",
            "icon": "/images/stripe.png",
            "payment": "stripe",
            "config": "{...}",
            "notify_domain": null,
            "notify_url": "http://example.com/api/v1/guest/payment/notify/stripe/uuid1",
            "sort": 1,
            "enable": true
        },
        {
            "id": 2,
            "name": "PayPal",
            "icon": "/images/paypal.png",
            "payment": "paypal",
            "config": "{...}",
            "notify_domain": "https://customdomain.com",
            "notify_url": "https://customdomain.com/api/v1/guest/payment/notify/paypal/uuid2",
            "sort": 2,
            "enable": false
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an issue fetching the payment methods.

### 3. Get Payment Form (`getPaymentForm`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/payment/form`

**Parameters:**

- `payment`: The payment method identifier.
- `id`: The ID of the payment configuration (if updating an existing method).

**Headers:**

- `Accept: application/json`

#### Description

Generates and returns the payment form for a specified payment method. This form is used to configure or update payment methods.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "fields": [
            {
                "name": "api_key",
                "type": "text",
                "label": "API Key",
                "required": true
            },
            {
                "name": "secret",
                "type": "password",
                "label": "Secret",
                "required": true
            }
        ]
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an issue generating the form.

### 4. Show Payment Method (`show`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/payment/show`

**Parameters:**

- `id`: The ID of the payment method to enable/disable.

**Headers:**

- `Accept: application/json`

#### Description

Toggles the enable/disable status of a specified payment method.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the payment method does not exist or if the update fails.

### 5. Save Payment Method (`save`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/payment/save`

**Parameters:**

- `id` (optional): The ID of the payment method to update.
- `name`: The display name of the payment method.
- `icon`: The icon associated with the payment method (optional).
- `payment`: The payment gateway identifier.
- `config`: Configuration parameters for the payment method.
- `notify_domain`: Custom notification domain (optional).
- `handling_fee_fixed`: Fixed handling fee (optional).
- `handling_fee_percent`: Percentage handling fee (optional).

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Creates a new payment method or updates an existing one. Validates input data and saves the payment method configuration to the database.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the payment method cannot be created or updated.

### 6. Drop Payment Method (`drop`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/payment/drop`

**Parameters:**

- `id`: The ID of the payment method to delete.

**Headers:**

- `Accept: application/json`

#### Description

Deletes a specified payment method from the database.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the payment method does not exist or if the deletion fails.

### 7. Sort Payment Methods (`sort`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/payment/sort`

**Parameters:**

- `ids`: An array of payment method IDs in the desired order.

**Headers:**

- `Accept: application/json`
- `Content-Type: application/json`

#### Description

Updates the sorting index of payment methods.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the sorting update fails.

### Error Handling

- **500 Internal Server Error** is used for unexpected errors, such as issues with database transactions, validation failures, or if required configurations are missing.

### Summary

- **`getPaymentMethods`**: Retrieves available payment method classes.
- **`fetch`**: Fetches and returns all payment methods with their details.
- **`getPaymentForm`**: Provides the configuration form for a specified payment method.
- **`show`**: Toggles the enable/disable status of a payment method.
- **`save`**: Creates or updates a payment method.
- **`drop`**: Deletes a payment method.
- **`sort`**: Updates the sorting index of payment methods.

Let me know if you need more details or further assistance!

The `OrderController` class manages operations related to orders in your Laravel application. It handles creating, fetching, updating, and managing orders and their related entities. Here’s a detailed breakdown of each method:

## API Documentation

### Overview

The `OrderController` class provides functionalities for managing orders, including fetching, updating, and assigning orders, as well as handling order statuses.

### 1. Detail (`detail`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/order/detail`

**Parameters:**

- `id`: The ID of the order to retrieve.

**Headers:**

- `Accept: application/json`

#### Description

Fetches detailed information about a specific order, including associated commission logs and surplus orders.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "id": 1,
        "user_id": 123,
        "plan_id": 456,
        "trade_no": "TRADE123",
        "total_amount": 100,
        "status": 1,
        "commission_log": [
            {
                "id": 1,
                "amount": 10,
                "created_at": "2024-07-24T12:00:00Z"
            }
        ],
        "surplus_orders": [
            {
                "id": 2,
                "user_id": 123,
                "plan_id": 456,
                "trade_no": "TRADE456",
                "total_amount": 50,
                "status": 0
            }
        ]
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the order does not exist or if there is an issue retrieving the details.

### 2. Fetch (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/order/fetch`

**Parameters:**

- `current` (optional): The current page number.
- `pageSize` (optional): The number of items per page.
- `is_commission` (optional): Filter by commission-related orders.
- `filter` (optional): Array of filter conditions.

**Headers:**

- `Accept: application/json`

#### Description

Fetches a list of orders with optional filters and pagination. Also includes plan names for each order.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "id": 1,
            "user_id": 123,
            "plan_id": 456,
            "trade_no": "TRADE123",
            "total_amount": 100,
            "status": 1,
            "plan_name": "Premium Plan"
        }
    ],
    "total": 1
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an issue fetching the orders.

### 3. Paid (`paid`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/order/paid`

**Parameters:**

- `trade_no`: The trade number of the order to mark as paid.

**Headers:**

- `Accept: application/json`

#### Description

Marks an order as paid based on its trade number. Only applicable to orders with a status of `0` (pending payment).

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the order does not exist, is not in a pending state, or if the update fails.

### 4. Cancel (`cancel`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/order/cancel`

**Parameters:**

- `trade_no`: The trade number of the order to cancel.

**Headers:**

- `Accept: application/json`

#### Description

Cancels an order based on its trade number. Only applicable to orders with a status of `0` (pending payment).

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the order does not exist, is not in a pending state, or if the update fails.

### 5. Update (`update`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/order/update`

**Parameters:**

- `trade_no`: The trade number of the order to update.
- `commission_status`: New commission status for the order.

**Headers:**

- `Accept: application/json`

#### Description

Updates the commission status of an order based on its trade number.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the order does not exist or if the update fails.

### 6. Assign (`assign`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/order/assign`

**Parameters:**

- `plan_id`: The ID of the plan to assign to the user.
- `email`: The email address of the user to whom the plan is assigned.
- `period`: The period of the order.
- `total_amount`: The total amount of the order.

**Headers:**

- `Accept: application/json`

#### Description

Creates a new order and assigns it to a user based on the provided email and plan ID. Ensures that the user does not have any pending orders.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": "TRADE123"
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the user or plan does not exist, if the user has pending orders, or if the order creation fails.

### Error Handling

- **500 Internal Server Error** is used for unexpected errors such as missing orders, failed updates, or issues with database transactions.

### Summary

- **`detail`**: Retrieves detailed information about a specific order.
- **`fetch`**: Fetches a list of orders with optional filters and pagination.
- **`paid`**: Marks an order as paid.
- **`cancel`**: Cancels an order.
- **`update`**: Updates the commission status of an order.
- **`assign`**: Creates and assigns an order to a user.

Let me know if you need more details or further assistance!
The `NoticeController` class is responsible for managing notices within your Laravel application. It provides functionality to fetch, save, show, and delete notices. Here's a detailed breakdown of each method:

## API Documentation

### Overview

The `NoticeController` class allows you to manage notices in your system, including retrieving, updating, displaying, and deleting them.

### 1. Fetch (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/notice/fetch`

**Parameters:**

- None

**Headers:**

- `Accept: application/json`

#### Description

Retrieves a list of all notices, ordered by ID in descending order.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "id": 1,
            "title": "Notice Title",
            "content": "Notice Content",
            "img_url": "http://example.com/image.jpg",
            "tags": ["tag1", "tag2"],
            "show": 1,
            "created_at": "2024-07-24T12:00:00Z",
            "updated_at": "2024-07-24T12:00:00Z"
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there is an issue retrieving the notices.

### 2. Save (`save`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/notice/save`

**Parameters:**

- `id` (optional): The ID of the notice to update. If not provided, a new notice will be created.
- `title`: The title of the notice.
- `content`: The content of the notice.
- `img_url` (optional): The URL of the notice image.
- `tags` (optional): An array of tags associated with the notice.

**Headers:**

- `Accept: application/json`

#### Description

Creates a new notice or updates an existing notice based on the provided `id`. 

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the save operation fails.

### 3. Show (`show`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/notice/show`

**Parameters:**

- `id`: The ID of the notice to toggle visibility.

**Headers:**

- `Accept: application/json`

#### Description

Toggles the visibility of a notice. If the notice is currently visible, it will be hidden, and vice versa.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the notice does not exist or if the update fails.

### 4. Drop (`drop`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/notice/drop`

**Parameters:**

- `id`: The ID of the notice to delete.

**Headers:**

- `Accept: application/json`

#### Description

Deletes a notice based on its ID.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the notice does not exist or if the deletion fails.

### Error Handling

- **500 Internal Server Error** is used for errors such as missing notices, failed saves, or deletion issues.

### Summary

- **`fetch`**: Retrieves all notices, ordered by ID in descending order.
- **`save`**: Creates or updates a notice.
- **`show`**: Toggles the visibility of a notice.
- **`drop`**: Deletes a notice.

This controller handles CRUD operations for notices and manages their visibility. Let me know if you need further assistance or have any additional questions!

The `KnowledgeController` class manages knowledge entries in your Laravel application. It handles operations such as fetching, saving, displaying, sorting, and deleting knowledge records. Here's a detailed explanation of each method:

## API Documentation

### Overview

The `KnowledgeController` class is responsible for CRUD operations related to knowledge entries, including their categorization and ordering.

### 1. Fetch (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/knowledge/fetch`

**Parameters:**

- `id` (optional): The ID of a specific knowledge entry to fetch.

**Headers:**

- `Accept: application/json`

#### Description

Retrieves a specific knowledge entry by ID or all knowledge entries with minimal fields (`title`, `id`, `updated_at`, `category`, `show`) if no ID is provided.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "id": 1,
            "title": "Knowledge Title",
            "category": "Category Name",
            "updated_at": "2024-07-24T12:00:00Z",
            "show": 1
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the knowledge entry does not exist when an ID is provided.

### 2. Get Category (`getCategory`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/knowledge/getCategory`

**Parameters:**

- None

**Headers:**

- `Accept: application/json`

#### Description

Retrieves all unique categories from knowledge entries.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        "Category1",
        "Category2"
    ]
}
```

### 3. Save (`save`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/knowledge/save`

**Parameters:**

- `id` (optional): The ID of the knowledge entry to update. If not provided, a new knowledge entry will be created.
- `title`: The title of the knowledge entry.
- `content`: The content of the knowledge entry.
- `category`: The category of the knowledge entry.
- `show`: Boolean indicating whether the entry is visible.

**Headers:**

- `Accept: application/json`

#### Description

Creates a new knowledge entry or updates an existing one based on the provided `id`.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the save operation fails.

### 4. Show (`show`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/knowledge/show`

**Parameters:**

- `id`: The ID of the knowledge entry to toggle visibility.

**Headers:**

- `Accept: application/json`

#### Description

Toggles the visibility of a knowledge entry. If the entry is currently visible, it will be hidden, and vice versa.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the knowledge entry does not exist or if the update fails.

### 5. Sort (`sort`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/knowledge/sort`

**Parameters:**

- `knowledge_ids`: An array of knowledge entry IDs in the desired order.

**Headers:**

- `Accept: application/json`

#### Description

Sorts knowledge entries based on the provided IDs.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if sorting fails or an exception occurs.

### 6. Drop (`drop`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/knowledge/drop`

**Parameters:**

- `id`: The ID of the knowledge entry to delete.

**Headers:**

- `Accept: application/json`

#### Description

Deletes a knowledge entry based on its ID.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the knowledge entry does not exist or if the deletion fails.

### Error Handling

- **500 Internal Server Error** is used for errors such as missing knowledge entries, failed saves, sorting issues, or deletion problems.

### Summary

- **`fetch`**: Retrieves specific knowledge entry or all entries with minimal details.
- **`getCategory`**: Retrieves all unique categories from knowledge entries.
- **`save`**: Creates or updates a knowledge entry.
- **`show`**: Toggles the visibility of a knowledge entry.
- **`sort`**: Sorts knowledge entries based on provided IDs.
- **`drop`**: Deletes a knowledge entry.

This controller handles all the necessary operations for managing knowledge entries in your system, including visibility, categorization, and sorting. Let me know if you need further details or have any questions!

The `CouponController` class manages coupon-related functionality in your Laravel application. This includes operations such as fetching, showing, generating, and deleting coupons. Here's a detailed explanation of each method:

## API Documentation

### Overview

The `CouponController` class handles various operations for managing coupons, including their visibility, generation, and deletion.

### 1. Fetch (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/coupon/fetch`

**Parameters:**

- `current` (optional): The current page number for pagination. Defaults to `1`.
- `pageSize` (optional): Number of coupons per page. Defaults to `10` if less than `10`.
- `sort` (optional): The column by which to sort. Defaults to `id`.
- `sort_type` (optional): The sort direction, either `ASC` or `DESC`. Defaults to `DESC`.

**Headers:**

- `Accept: application/json`

#### Description

Retrieves a paginated list of coupons, ordered by the specified column and sort direction.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "id": 1,
            "code": "ABCD1234",
            "name": "Discount Coupon",
            "type": 1,
            "value": 10,
            "started_at": 1680624000,
            "ended_at": 1683302400,
            "limit_use": 1,
            "limit_plan_ids": ["1", "2"],
            "created_at": "2024-07-24T12:00:00Z",
            "show": 1
        }
    ],
    "total": 1
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if any error occurs during fetching.

### 2. Show (`show`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/coupon/show`

**Parameters:**

- `id`: The ID of the coupon to toggle visibility.

**Headers:**

- `Accept: application/json`

#### Description

Toggles the visibility of a coupon. If the coupon is currently visible, it will be hidden, and vice versa.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the coupon does not exist or if the update fails.

### 3. Generate (`generate`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/coupon/generate`

**Parameters:**

- `id` (optional): The ID of an existing coupon to update.
- `name`: The name of the coupon.
- `type`: The type of coupon (1 for amount, 2 for percentage).
- `value`: The value of the coupon (amount or percentage).
- `started_at`: The start timestamp for the coupon.
- `ended_at`: The end timestamp for the coupon.
- `limit_use` (optional): The limit on how many times the coupon can be used.
- `limit_plan_ids` (optional): Array of plan IDs where the coupon is applicable.
- `generate_count` (optional): Number of coupons to generate if bulk generation is needed.

**Headers:**

- `Accept: application/json`

#### Description

Creates or updates a coupon. If `generate_count` is provided, it will generate multiple coupons.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the creation or update fails.

**Bulk Generation:**

When `generate_count` is provided, the method generates multiple coupons, formats them, and outputs them as a CSV string.

### 4. Drop (`drop`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/coupon/drop`

**Parameters:**

- `id`: The ID of the coupon to delete.

**Headers:**

- `Accept: application/json`

#### Description

Deletes a coupon based on its ID.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the coupon does not exist or if the deletion fails.

### Error Handling

- **500 Internal Server Error** is used for errors such as missing coupon entries, failed creations, or deletions.

### Summary

- **`fetch`**: Retrieves a paginated list of coupons with sorting.
- **`show`**: Toggles the visibility of a coupon.
- **`generate`**: Creates or updates a coupon, with support for bulk generation.
- **`drop`**: Deletes a coupon.

This controller provides robust functionality for managing coupons, including both individual and bulk operations. Let me know if you need further details or have additional questions!
The `ConfigController` class in your Laravel application manages various configuration settings and operations related to email templates, theme templates, Telegram webhooks, and application configuration. Here’s a detailed overview of its functionality:

## API Documentation

### Overview

The `ConfigController` class provides methods for:

- Retrieving email and theme templates.
- Testing email sending functionality.
- Setting Telegram webhooks.
- Fetching and saving application configurations.

### 1. Get Email Templates (`getEmailTemplate`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/config/email-templates`

**Headers:**

- `Accept: application/json`

#### Description

Lists all available email template files located in the `resources/views/mail/` directory.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        "welcome.blade.php",
        "notification.blade.php"
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there's an error accessing the file system.

### 2. Get Theme Templates (`getThemeTemplate`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/config/theme-templates`

**Headers:**

- `Accept: application/json`

#### Description

Lists all available theme template files located in the `public/theme/` directory.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        "default.css",
        "dark-theme.css"
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there's an error accessing the file system.

### 3. Test Send Mail (`testSendMail`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/config/test-send-mail`

**Parameters:**

- `email`: The recipient's email address.

**Headers:**

- `Accept: application/json`

#### Description

Sends a test email using the `SendEmailJob`. The email is sent to the address provided in the request.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true,
    "log": "Email sent successfully"
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if the email fails to send.

### 4. Set Telegram Webhook (`setTelegramWebhook`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/config/set-telegram-webhook`

**Parameters:**

- `telegram_bot_token`: The Telegram bot token.

**Headers:**

- `Accept: application/json`

#### Description

Sets the webhook URL for a Telegram bot using the provided token. The webhook URL is constructed and set for receiving updates.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if setting the webhook fails.

### 5. Fetch Configurations (`fetch`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v1/admin/config/fetch`

**Parameters:**

- `key` (optional): The specific configuration key to retrieve. If omitted, all configurations are returned.

**Headers:**

- `Accept: application/json`

#### Description

Fetches configuration values based on the provided key. If the key is not specified, it returns all configuration settings.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "invite": {
            "invite_force": 0,
            "invite_commission": 10,
            ...
        },
        "site": {
            "logo": "logo.png",
            "app_name": "V2Board",
            ...
        },
        ...
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there's an issue fetching the configuration.

### 6. Save Configurations (`save`)

#### Request

**HTTP Method:** `POST`  
**URL:** `/api/v1/admin/config/save`

**Parameters:**

- Configurations to save. This should adhere to validation rules defined in `ConfigSave`.

**Headers:**

- `Accept: application/json`

#### Description

Saves updated configuration values to the `v2board.php` configuration file. Clears the configuration cache after saving.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": true
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if saving the configuration or clearing the cache fails.

### Error Handling

- **500 Internal Server Error** is used for errors related to file access, email sending, or configuration saving.

### Summary

- **`getEmailTemplate`**: Lists email templates.
- **`getThemeTemplate`**: Lists theme templates.
- **`testSendMail`**: Sends a test email.
- **`setTelegramWebhook`**: Sets a webhook URL for Telegram.
- **`fetch`**: Retrieves configuration settings.
- **`save`**: Saves configuration settings and clears the cache.

This controller provides essential functionality for managing configurations, testing email functionality, and interacting with Telegram. Let me know if you need further details or assistance with any other parts of your application!
The `StatController` class in your Laravel application handles statistical data operations related to various aspects of the system. It provides endpoints for overriding statistics, recording specific statistics, and ranking based on different metrics. Here’s a detailed overview of its functionality:

## API Documentation

### Overview

The `StatController` class includes methods for:

- Overriding statistics with custom date ranges.
- Recording statistics based on type and date range.
- Ranking data based on specific metrics.

### 1. Override Statistics (`override`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v2/admin/stat/override`

**Parameters:**

- `start_at` (optional): The start date for fetching statistics (format: `YYYY-MM-DD`).
- `end_at` (optional): The end date for fetching statistics (format: `YYYY-MM-DD`).

**Headers:**

- `Accept: application/json`

#### Description

Fetches statistics for a given date range. If no date range is provided, generates and returns default statistical data using the `StatisticalService`.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "total_users": 100,
        "total_orders": 50,
        "total_commission": 500.00
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there’s an issue retrieving or processing the statistics.

### 2. Record Statistics (`record`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v2/admin/stat/record`

**Parameters:**

- `type`: The type of statistic to fetch. Possible values: `paid_total`, `commission_total`, `register_count`.
- `start_at` (optional): The start date for fetching statistics (format: `YYYY-MM-DD`).
- `end_at` (optional): The end date for fetching statistics (format: `YYYY-MM-DD`).

**Headers:**

- `Accept: application/json`

#### Description

Fetches statistics based on the specified type and optional date range. Utilizes the `StatisticalService` to retrieve data.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": {
        "paid_total": 1000.00,
        "commission_total": 200.00,
        "register_count": 10
    }
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there’s an issue retrieving the statistics.

### 3. Ranking Data (`ranking`)

#### Request

**HTTP Method:** `GET`  
**URL:** `/api/v2/admin/stat/ranking`

**Parameters:**

- `type`: The type of ranking to fetch. Possible values: `server_traffic_rank`, `user_consumption_rank`, `invite_rank`.
- `start_at` (optional): The start date for fetching ranking data (format: `YYYY-MM-DD`).
- `end_at` (optional): The end date for fetching ranking data (format: `YYYY-MM-DD`).
- `limit` (optional): The number of records to return. Default is `20`.

**Headers:**

- `Accept: application/json`

#### Description

Fetches ranking data based on the specified type and optional date range. Uses the `StatisticalService` to generate rankings.

#### Response

**Success:**

- **HTTP Status Code:** `200 OK`
- **Content-Type:** `application/json`

**Example Response:**

```json
{
    "data": [
        {
            "user_id": 1,
            "username": "user1",
            "rank": 1,
            "value": 500
        },
        {
            "user_id": 2,
            "username": "user2",
            "rank": 2,
            "value": 300
        }
    ]
}
```

**Failure:**

- **HTTP Status Code:** `500 Internal Server Error` if there’s an issue retrieving the ranking data.

### Error Handling

- **500 Internal Server Error** is used for issues related to data retrieval or processing.

### Summary

- **`override`**: Retrieves or generates statistical data based on optional date ranges.
- **`record`**: Fetches specific types of statistics, optionally filtered by date range.
- **`ranking`**: Retrieves ranking data based on specified metrics, with optional date ranges and limits.

This controller is crucial for managing and accessing statistical information within the application. If you need more details or have further questions, feel free to ask!
