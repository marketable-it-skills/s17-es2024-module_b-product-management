# Test Project Outline – Module B – Products Management

## Introduction

You are required to create a management system for an office administrator (referred to as "admin") to manage a set of made-in-France products. Products belong to companies, and the administrator must also manage the associated company data. Only the admin can access the listing and editing views for companies and products.

Each product record includes a unique identifier called the Global Trade Item Number (GTIN), developed by the international organization GS1.

There are also public-facing pages:

- A public GTIN bulk verification page
- A public product detail page

## General Description of Project and Tasks

This project involves building a management system for companies and products. It includes:

- Admin web pages for listing and editing records
- JSON APIs for reading and querying the data

## Requirements

### Admin Access

The admin login page is available at the path `/login`. It requires a passphrase for authentication. Use "admin" as the valid passphrase.

As this is a 3-hour prototype, a simple passphrase-based system is acceptable.

Unauthenticated attempts to access admin pages should return a 401 error.

### Managing Companies

Admins can:

- View a list of companies
- View individual company details
- View associated products within each company page
- Create and update company records

Company data fields include:

- Company name
- Company address
- Company telephone number
- Company email address
- Owner:
  - Name
  - Mobile number
  - Email address
- Contact:
  - Name
  - Mobile number
  - Email address

#### Deactivating Companies

- Admins can mark a company as deactivated.
- Deactivation hides all associated products.
- Deactivated companies should appear in a separate list.
- Deletion of company records via the web interface is not allowed.

### Managing Products

Each product has a GTIN (13 or 14 digit number, validated server-side).

Admins can:

- View a list of products at `/products`
- Access a product detail page at `/products/[GTIN]`
- Mark products as hidden
- Delete hidden products
- Create new products via `/products/new`

Product data fields include:

- Name (English and French)
- GTIN
- Description (English and French)
- Brand name
- Country of origin
- Gross weight (with packaging)
- Net content weight
- Weight unit

#### Product Image

- Each product may have one associated image
- Admins can upload, update, or delete the image
- A placeholder image is shown if no image is uploaded

### JSON API Outputs

- GET `/products.json` lists products with pagination
- GET `/products/[GTIN].json` returns single product data
- 404 is returned for non-existent or hidden products
- Keyword filtering: `/products.json?query=KEYWORD`

#### Example Company JSON Output

```json
{
  "companyName": "Euro Expo",
  "companyAddress": "Boulevard de l'Europe, 69680 Chassieu, France",
  "companyTelephone": "+33 1 41 56 78 00",
  "companyEmail": "mail.customerservice.hdq@example.com",
  "owner": {
    "name": "Benjamin Smith",
    "mobileNumber": "+33 6 12 34 56 78",
    "email": "b.smith@example.com"
  },
  "contact": {
    "name": "Marie Dubois",
    "mobileNumber": "+33 6 98 76 54 32",
    "email": "m.dubois@example.com"
  }
}
```

#### Example Product JSON Output

```json
{
  "name": {
    "en": "Organic Apple Juice",
    "fr": "Jus de pomme biologique"
  },
  "description": {
    "en": "Our organic apple juice is pressed from 100% fresh organic apples...",
    "fr": "Notre jus de pomme biologique est pressé à partir de 100% de pommes biologiques..."
  },
  "gtin": "03000123456789",
  "brand": "Green Orchard",
  "countryOfOrigin": "France",
  "weight": {
    "gross": 1.1,
    "net": 1.0,
    "unit": "L"
  },
  "company": {
    (same structure as company JSON above)
  }
}
```

#### Example Products List JSON Output

```json
{
  "data": [
    { (Product JSON) },
    { (Product JSON) }
  ],
  "pagination": {
    "current_page": 1,
    "total_pages": 5,
    "per_page": 10,
    "next_page_url": "http://wsXX.worldskills.org/XX_module_b/products.json?page=2",
    "prev_page_url": null
  }
}
```

### Public-Facing Pages

#### GTIN Bulk Verification Page

- Users can submit multiple GTINs to check their validity
- Valid = GTIN exists and is not hidden
- Results shown per GTIN
- If all GTINs are valid, show a "All valid" message with a green tick

#### Public Product Page

- URL format: `/01/[GTIN]` ("01" is static)

- Mobile-friendly layout

- Must display:

  - Company name
  - Product name
  - GTIN
  - Product description
  - Product image
  - Gross weight and unit
  - Net content weight and unit

- Language toggle between English and French

### Instructions to the Competitor

#### Database and Model Design

- Use a database to store companies and products
- Support multilingual product fields
- Provide:
  - Database dump (with FK constraints and valid schema)
  - ER diagram
  - Indexed GTIN field
  - Preloaded sample data

#### Hosting and Path Notes

- Project can be hosted in a subfolder or on a different port

## Assessment

This project will be assessed using Firefox Developer Edition.

## Mark distribution

| WSOS SECTION | Description                 | Points |
| ------------ | --------------------------- | ------ |
| 1            | Admin                       | 1.25   |
| 2            | Database                    | 2.50   |
| 3            | Companies (Admin)           | 4.25   |
| 4            | Products CRUD (Admin)       | 7.75   |
| 5            | Products API                | 4.50   |
| 6            | GTIN Query and Verification | 1.75   |
| 7            | Public facing product page  | 1.50   |
| **Total**    |                             | 23.50  |

