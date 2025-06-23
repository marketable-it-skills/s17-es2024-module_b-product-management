# Test Project Outline – Module B – Products Management

## Introduction

We are going to create a management system for an office administrator (as known as "admin") to manage some made-in-France products. Products belongs to companies. The administrator will also manage the associated company data as well. Only admin can view and manage these companies and products listing and editing views.

Each product record comes with a unique identifier number, we call it Global Trade Item Number (GTIN). As a background information, the GTIN is developed by the international organization GS1.

On the other hand, there are public-facing pages. They are:

- Public GTIN bulk verification page
- Public Product page

## General Description of Project and Tasks

In this project, we create a companies and products management system for an admin to manage these madein-France products.

It contains management web pages for listing and editing the records. And JSON API for querying and reading the data as well.

## Requirements

### Admin access

Admin login page is at path \`/XX_module_b/login\`. The login page asks for a passphrase to proceed the authentication. A passphrase "admin" can be used to access the admin management system.

As a prototype product for a 3 hours' work. We do not require robust authentication. The management system uses simple passphrase-based checking.

The task is to create a companies and products management system.

Given that the time constant, we focus on the prototype of the companies and products recording management and the proof-of-concept of displaying the product in a public page.

Accessing product editing and management functions without login results in 401 error.

### Managing Companies

Only admin can list and manage the companies.

Admin can click and view a particular company from the companies list.

In each company page, admin can view the associated products.

Admin can also create new companies or update existing companies’ information.

Here are the data we would like to store and manage for each company:

- company name
- company address
- company telephone number • company email address
- owner information:
- owner's name
- owner's mobile number
- owner's email address
- contact information
- contact's name
- contact's mobile number
- contact's email address

#### Deactivating companies

Admin can mark a company as deactivated.

When a company is deactivated, all the associated products are marked as hidden.

There should be a separated list for listing deactivated companies.

No one should be able to delete any company records from the web interface.

### Managing Products

There are different fields in each product, one worth remark is the GTIN.

In this project, we simplify the GTIN to be any number with 13 or 14 digits. It could be any sequence of number, as long as they are unique for each product. Please validate this GTIN format after form submissions, via serverside validation.

#### Listing products

Admin should be able to list and manage products.

When admin access the /XX_module_b/products, admin can see the list of all products.

Admin can access and manage a particular product by clicking on the product record from the list, or by accessing the following path: /XX_module_b/products/\[GTIN\]. \[GTIN\] is the placeholder of the GTIN field.

For example, given a product with GTIN 3000123456789, accessing the

/XX_module_b/products/3000123456789 will be the product management page for this given product.

#### Hiding and deleting products

Admin can mark products as hidden.

Or a product becomes hidden when the associated company is marked as deactivated.

Admin can permanently delete hidden products.

#### Creating new products

Admin can view the create product form by accessing the /products/new, and can save newly created products to database.

Products has two languages of information, English and French.

For products, we have the following data to store:

- name
- name in French
- GTIN (Global Trade Item Number)
- description, can be multiple lines of text.
- description in French
- product brand name
- product country of origin
- product gross weight (with packaging)
- product net content weight
- product weight unit

#### Product Images Uploading

There could be one image associated to each product. Admin can upload and change this image, or admin can remove the uploaded images.

When no image is uploaded, there is a default placeholder image.

### JSON API Outputs

The data can be output as JSON format when accessing GET /XX_module_b/products.json. When listing the products, the API will show a pagination structure.

A single product can be queried via JSON by GET /XX_module_b/products/\[GTIN\].json, where the GTIN is dynamic.

The product API returns 404 network status when accessing a non-exist product, or a hidden product.

The products list JSON allows querying by using keyword, by GET

/XX_module_b/products.json?query=KEYWORD. The list should show products with name, or name in French, or description, or description in French, that contains the KEYWORD.

### JSON API Example Outputs

Example company output

{

"companyName": "Euro Expo",

"companyAddress": " Boulevard de l'Europe, 69680 Chassieu, France",

"companyTelephone": "+33 1 41 56 78 00",

"companyEmail": "<mail.customerservice.hdq@example.com>",

"owner": {

"name": "Benjamin Smith",

"mobileNumber": "+33 6 12 34 56 78",

"email": "<b.smith@example.com> "

},

"contact": {

"name": "Marie Dubois",

"mobileNumber": "+33 6 98 76 54 32",

"email": "<m.dubois@example.com> "

}

}

Example product output

{

"name": {

"en": "Organic Apple Juice",

"fr": "Jus de pomme biologique"

},

"description": {

"en": "Our organic apple juice is pressed from 100% fresh organic apples, with no added sugars or preservatives. Rich in vitamin C and antioxidants, it's an ideal choice for your daily healthy diet.",

"fr": "Notre jus de pomme biologique est pressé à partir de 100% de pommes biologiques fraîches, sans sucre ajouté ni conservateurs. Riche en vitamine C et en antioxydants, c'est le choix idéal pour votre alimentation quotidienne saine."

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

"companyName": "Euro Expo",

"companyAddress": " Boulevard de l'Europe, 69680 Chassieu, France",

"companyTelephone": "+33 1 41 56 78 00",

"companyEmail": "<mail.customerservice.hdq@example.com>",

"owner": {

"name": "Benjamin Smith",

"mobileNumber": "+33 6 12 34 56 78",

"email": "<b.smith@example.com> "

},

"contact": {

"name": "Marie Dubois",

"mobileNumber": "+33 6 98 76 54 32",

"email": "<m.dubois@example.com> "

}

}

}

#### Example Products JSON

{

"data": \[

{

(Same as single product JSON structure)

},

{

(Same as single product JSON structure)

},

\],

"pagination": {

"current_page": 1,

"total_pages": 5,

"per_page": 10,

"next_page_url": "<http://wsXX.worldskills.org/XX_module_b/products.json?page=2>", "prev_page_url": null

}

}

### Public-facing Pages

There are two public facing pages, they are GTIN bulk verification page, and public product page.

#### Public GTIN bulk verification page

There is a page for bulk validating if given GTIN numbers are registered and valid. Any user can input multiple GTIN codes and submit to see the validation result.

A GTIN is valid when it exists in the database and is not hidden.

The page uses a text area to allow user to bulk inputting GTIN numbers. These numbers are separated by line breaks. Then the page should check each GTIN number and display a list of results, showing if each GTIN number is valid.

If all the given GTIN numbers are valid, a separated "All valid" text and green tick is displayed on the top of the result page.

#### Public Product Page

A product's public page can be reached by accessing the /XX_module_b/01/\[GTIN\]. Where the "01" is static.

The public product page shows the following required field. And is in mobile-friendly layout.

The required field to display: company name, product name, GTIN number, product description, product image, weight with unit, net content weight with unit.

User can choose between English and French for the public product page The lang attribute for the page, French part and English part is correctly configured.

### Instructions to the Competitor

### Database and model creation consideration

We would like to store the companies and products data in database.

Please consider the flexibility of multi-lingual information for products.

Please provide the database dump. The database dump should contain FK-constraints and correct columns. The columns type definition shall be reasonable.

Please provide the ER diagram schema.

Please consider the normal form of database.

The GTIN field should be indexed.

Some sample data has been provided. Please use them and have some data in database for easier assessment.

### Other

You may put your project in a sub-folder or different port. Please redirect to your destination from the path wsXX.worldskills.org/XX_module_b/

The path mentioned in this document may be relative to your sub-folder. For example, when mentioning the login page as /XX_module_b/login — dependent to your actual setup — it may be actually /XX_module_b/public/login, or /XX_module_b/index.php/login or at different port such as <http://wsXX.worldskills.org:3000/XX_module_b/login>.

Please also provide a file named \`expert_readme.txt\` to include executing guide. You must provide this file even if you use the default executing path.

Note if you are using NodeJS, please be aware of the node_modules files for Windows (on workstation) and Linux (on server) is different. Using a wrong node_modules folder may result in unexpected error.

## Assessment

This project will be assessed by using Firefox Developer Edition web browser.

## Mark distribution

The table below outlines how marks are broken down and how they align with the WorldSkills
Occupation Standards (WSOS). Please read the Technical Description for a full explanation of the
WorldSkills Occupation Standards.

| WSOS SECTION | Description                            | Points |
| ------------ | -------------------------------------- | ------ |
| 1            | Work organization and self-management  | 1      |
| 2            | Communication and interpersonal skills | 1      |
| 3            | Design Implementation                  | 15     |
| 4            | Front-End Development                  | 0      |
| 5            | Back-End Development                   | 0      |
|              |                                        |        |
| **Total**    |                                        | 17     |
