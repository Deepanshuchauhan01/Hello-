# Hello-
Act as a Senior Solution Architect and Principal .NET Developer.

Generate a COMPLETE enterprise-grade ASP.NET Core Microservices solution named:

EShoppingZone

The implementation must be production-ready and follow the Low Level Design specification below.

===========================================================
PROJECT OVERVIEW
===========================================================

EShoppingZone is an E-Commerce Shopping Cart System.

Architecture:
- Microservices Architecture
- ASP.NET Core 10 Web API
- Entity Framework Core
- SQL Server
- JWT Authentication
- Role-Based Authorization
- API Gateway
- SMTP Email Notifications
- Global Exception Middleware
- NUnit Unit Testing
- Swagger/OpenAPI
- Repository Pattern
- Service Layer Pattern
- Clean Architecture
- Docker Support
- Serilog Logging

Roles:
1. Customer
2. Merchant

Customers:
- Register/Login
- Manage Profile
- Browse Products
- Search Products
- Add Products to Cart
- Update Cart
- Remove Cart Items
- Checkout
- Pay Online using Wallet
- View Orders
- View Wallet Transactions

Merchants:
- Login
- Add Products
- Update Own Products
- Delete Own Products
- View Orders containing their Products

===========================================================
MANDATORY FEATURES
===========================================================

1. JWT Authentication
2. Role Based Authorization
3. SMTP Email Service
4. Global Exception Middleware
5. NUnit Unit Tests
6. Wallet Payment Gateway
7. Swagger
8. Repository Pattern
9. Dependency Injection
10. EF Core Code First
11. DTO Pattern
12. AutoMapper
13. Serilog
14. API Gateway
15. SQL Server
16. Migration Scripts
17. Validation using FluentValidation
18. Password Hashing
19. Refresh Token Support
20. Audit Fields

===========================================================
MICROSERVICES
===========================================================

Create separate projects:

1. ApiGateway
2. ProfileService
3. ProductService
4. CartService
5. OrderService
6. WalletService

===========================================================
DATABASES
===========================================================

Each service must have its own SQL Server database.

ProfileDB
ProductDB
CartDB
OrderDB
WalletDB

Use EF Core Code First.

Generate:
- DbContext
- Models
- Entity Configurations
- Migrations
- Seed Data

===========================================================
PROFILE SERVICE
===========================================================

Responsibilities:
- Customer Registration
- Customer Login
- Merchant Login
- JWT Generation
- Refresh Tokens
- Customer Profile Management
- Address Management

Entities:

ApplicationUser
- Id
- FirstName
- LastName
- Email
- PasswordHash
- PhoneNumber
- Role
- CreatedDate
- ModifiedDate

Address
- Id
- UserId
- AddressLine1
- AddressLine2
- City
- State
- Country
- ZipCode

Roles:
- CUSTOMER
- MERCHANT

APIs:

POST /api/auth/register
POST /api/auth/login
POST /api/auth/refresh-token
GET /api/profile
PUT /api/profile
POST /api/address
GET /api/address
PUT /api/address/{id}
DELETE /api/address/{id}

SMTP EMAIL:

Send Email On:
- Registration Success
- Password Reset
- Order Confirmation

===========================================================
PRODUCT SERVICE
===========================================================

Responsibilities:
- Product Catalogue
- Search
- Merchant Product Management

Entity:

Product
- Id
- MerchantId
- Name
- Description
- Category
- Price
- Stock
- ImageUrl
- IsActive
- CreatedDate

APIs:

GET /api/products
GET /api/products/{id}
GET /api/products/search
POST /api/products
PUT /api/products/{id}
DELETE /api/products/{id}

Authorization:

Customer:
- Read Only

Merchant:
- Add
- Update Own Products
- Delete Own Products

===========================================================
CART SERVICE
===========================================================

Entities:

Cart
- Id
- CustomerId
- TotalPrice

CartItem
- Id
- CartId
- ProductId
- ProductName
- Price
- Quantity

APIs:

GET /api/cart
POST /api/cart/items
PUT /api/cart/items/{id}
DELETE /api/cart/items/{id}
DELETE /api/cart/clear

Business Rules:

- Product must exist
- Quantity > 0
- Recalculate total automatically

===========================================================
ORDER SERVICE
===========================================================

Entities:

Order
- Id
- CustomerId
- AddressId
- TotalAmount
- Status
- PaymentStatus
- CreatedDate

OrderItem
- Id
- OrderId
- ProductId
- MerchantId
- Quantity
- Price

Enums:

OrderStatus
- Pending
- Confirmed
- Cancelled

PaymentStatus
- Pending
- Paid
- Failed

APIs:

POST /api/orders
GET /api/orders/customer
GET /api/orders/{id}
GET /api/orders/merchant

Business Flow:

1. Validate Customer
2. Load Cart
3. Validate Cart Not Empty
4. Calculate Amount
5. Call Wallet Service
6. Create Order
7. Empty Cart
8. Send Email
9. Return Response

Merchant Authorization:

Merchant can only see orders containing their products.

===========================================================
WALLET SERVICE
===========================================================

Entities:

Wallet
- Id
- CustomerId
- Balance

WalletTransaction
- Id
- WalletId
- Amount
- TransactionType
- OrderId
- Remarks
- CreatedDate

TransactionType:
- CREDIT
- DEBIT

APIs:

POST /api/wallet/add-money
POST /api/wallet/pay
GET /api/wallet
GET /api/wallet/transactions

Business Rules:

- Wallet must exist
- Amount > 0
- Sufficient Balance Required
- Create Transaction Records

===========================================================
GLOBAL EXCEPTION MIDDLEWARE
===========================================================

Implement:

GlobalExceptionMiddleware

Handle:

ValidationException -> 400
UnauthorizedAccessException -> 401
NotFoundException -> 404
BusinessException -> 400
Exception -> 500

Return standard error response.

===========================================================
JWT AUTHENTICATION
===========================================================

Implement:

JwtTokenGenerator
RefreshTokenGenerator

Claims:

UserId
Email
Role

Policies:

CustomerPolicy
MerchantPolicy

===========================================================
SMTP EMAIL SERVICE
===========================================================

Implement:

EmailService

Using:

MailKit
SMTP

Templates:

Welcome Email
Order Confirmation
Payment Success
Payment Failed

Configuration:

SMTP Host
SMTP Port
SMTP Username
SMTP Password

===========================================================
PAYMENT GATEWAY
===========================================================

Implement Wallet Payment Gateway.

Order Service -> Wallet Service

Communication:

HttpClient

Endpoints:

POST /wallet/pay

Responses:

Success
Failed
Insufficient Balance

===========================================================
UNIT TESTING
===========================================================

Use:

NUnit
Moq
FluentAssertions

Test Projects:

ProfileService.Tests
ProductService.Tests
CartService.Tests
OrderService.Tests
WalletService.Tests

Cover:

100% major business logic

Required Scenarios:

Cart:
- Add Valid Product
- Invalid Product
- Quantity Zero
- Update Quantity
- Remove Item
- Checkout Empty Cart

Order:
- Successful Order
- Empty Cart
- Unauthorized User
- Invalid Address
- Payment Success
- Payment Failure

Merchant:
- Add Product
- Update Own Product
- Update Other Merchant Product
- View Product Orders

Wallet:
- Add Money
- Pay Success
- Pay Failure
- Insufficient Balance

===========================================================
API GATEWAY
===========================================================

Implement YARP Reverse Proxy.

Routes:

/profile/*
/product/*
/cart/*
/order/*
/wallet/*

Gateway Responsibilities:

- JWT Validation
- Request Routing
- Authorization

===========================================================
VALIDATIONS
===========================================================

Customer:
- Name Required
- Email Required
- Password Required
- Email Unique

Merchant:
- Merchant Role Required

Product:
- Name Required
- Category Required
- Price > 0

Cart:
- Quantity > 0
- Product Exists

Wallet:
- Amount > 0
- Sufficient Balance

===========================================================
DELIVERABLES
===========================================================

Generate EVERYTHING.

Do not skip any file.

Output:

1. Complete Solution Structure
2. Folder Tree
3. All NuGet Packages
4. Entity Models
5. DTOs
6. Repositories
7. Services
8. Interfaces
9. Controllers
10. Middleware
11. Validators
12. AutoMapper Profiles
13. DbContexts
14. Program.cs
15. appsettings.json
16. JWT Configuration
17. SMTP Configuration
18. EF Configurations
19. SQL Scripts
20. API Gateway Config
21. NUnit Test Cases
22. Docker Files
23. Docker Compose
24. Swagger Configuration
25. Seed Data
26. Sample Requests
27. Sample Responses

Generate all code files completely with full implementations.

Never return placeholders like:
"implement here"
"todo"

Every class must contain complete compilable code.

Provide code service-by-service starting from ProfileService and ending with API Gateway.


