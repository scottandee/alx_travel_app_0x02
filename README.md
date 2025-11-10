# ALX Travel App – ProDev Backend (Milestone 4)
### Project Overview
This repository contains the initial setup for the **ALX Travel App**, a real-world Django application that serves as the foundation for a travel listing platform. Milestone 4 focuses on integrating the Chapa Payment Gateway to the travel booking application. It covers payment initiation, verification, and status handling for bookings.

## File Structure
```bash
.
├── README.md
└── alx_travel_app
    ├── README.md
    ├── alx_travel_app
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── requirement.txt
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    ├── listings
    │   ├── __init__.py
    │   ├── admin.py
    │   ├── apps.py
    │   ├── fixtures
    │   │   └── example.json
    │   ├── management
    │   │   └── commands
    │   │       └── seed.py
    │   ├── migrations
    │   │   ├── 0001_initial.py
    │   │   ├── 0002_rename_creatd_at_booking_created_at.py
    │   │   ├── 0003_alter_booking_user_id.py
    │   │   ├── 0004_rename_creatd_at_review_created_at.py
    │   │   ├── 0005_alter_review_user_id.py
    │   │   ├── 0006_rename_property_id_listing_listing_id_and_more.py
    │   │   ├── 0007_rename_listing_id_booking_listing_and_more.py
    │   │   ├── 0008_remove_user_password_hash_alter_user_email_and_more.py
    │   │   └── __init__.py
    │   ├── models.py
    │   ├── permissions.py
    │   ├── serializers.py
    │   ├── tests.py
    │   ├── urls.py
    │   └── views.py
    ├── manage.py
    └── requirements.txt

7 directories, 30 files
```

## Quickstart
1. Create a virtual environment
    ```bash
    python -m venv venv
    source venv/bin/activate
    ```
2. Clone the repository
    ```bash
    git clone https://github.com/scottandee/alx_travel_app.git
    cd alx_travel_app/alx_travel_app/
    ```
3. Install dependencies
    ```bash
    pip install -r requirements.txt
    ```
4. Configure environment variables
    ```bash
    cp .env.example .env
    ```
5. Apply migrations
    ```bash
    python manage.py makemigrations
    python manage.py migrate
    ```
6. Create a user
    ```bash
    python manage.py createsuperuser
    ```
7. Run the development server
    ```bash
    python manage.py runserver
    ```
8. Access Swagger documentation
- Navigate to: http://127.0.0.1:8000/api/swagger/

## Authentication
- **Endpoint**: **POST** `http://127.0.0.1:8000/api/token/`
- **Body**:
  ```json
  {
      "username": "clarencehunt",
      "password": "password"
  }
  ```
- **Success Response**:
  ```json
  {
      "refresh": "sjsjsjsjsjsjsjsjsjsjsjjsjsjsjsjsjs",
      "access": "nsjsjsjsjsjsjsjsjsjsjsjsjsjsj"
  }
  ```

## Payment Endpoints
### Initiate Payment
- **Endpoint**: **POST** `http://127.0.0.1:8000/api/payments/initiate/`
- **Authorization**: Bearer
- **Body**:
  ```json
  {
    "booking": "c0d78ce1-8df7-4e3d-9ff4-ce34f418fc0f"
  }
  ```
- **Success Response**:
  ```json
  {
      "payment_id": "b86cc6d0-b873-4cee-88ee-c27c78cb4464",
      "booking": "216c02a5-ec69-41a4-96e1-97df9f29b45b",
      "tx_ref": "cfba3f32-b8a4-4d7f-97dc-ffc68e4e6388",
      "amount": "1266.00",
      "status": "pending",
      "created_at": "2025-11-09T20:13:32.053487Z",
      "checkout_url": "https://checkout.chapa.co/checkout/payment/yJC9jLGXW4kfhr45DY2tHMemBzEVeKQD0M5EP8cr1fHfS"
  }
  ```
### Verify Payment
- **Endpoint**: **POST** `http://127.0.0.1:8000/api/payments/verify/{tx_ref}/`
- **Authorization** : Bearer
- **Parameter**: `tx_ref`
- **Success Response**:
  ```json
  {
      "payment_id": "b86cc6d0-b873-4cee-88ee-c27c78cb4464",
      "booking": "216c02a5-ec69-41a4-96e1-97df9f29b45b",
      "tx_ref": "cfba3f32-b8a4-4d7f-97dc-ffc68e4e6388",
      "amount": "1266.00",
      "status": "success",
      "created_at": "2025-11-09T20:13:32.053487Z"
  }
  ```
  
