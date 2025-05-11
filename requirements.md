# Requirements Specification – Backend Features

## 1. User Authentication

### Functional Requirements
- Users must be able to register and log in securely.
- JWT tokens must be issued upon successful login for session management.
- Passwords must be hashed using bcrypt.

### API Endpoints
- POST /api/register
  - Input: username, email, password
  - Output: Success message or error
- POST /api/login
  - Input: email, password
  - Output: JWT token or error

### Validation Rules
- Email must be in a valid format and unique.
- Password must be at least 8 characters and include both letters and numbers.

### Performance Criteria
- Authentication responses should be under 1 second.
- Limit login attempts to 5 per minute per IP address.

## 2. Property Management

### Functional Requirements
- Users can create, update, and delete their own property listings.
- Each listing includes title, description, location, price, and optional images.

### API Endpoints
- POST /api/properties
  - Input: title, description, location, price, images
- GET /api/properties
  - Output: List of properties with optional filters
- PUT /api/properties/:id
- DELETE /api/properties/:id

### Validation Rules
- Price must be a positive number.
- Only property owners can modify or delete their listings.

### Performance Criteria
- GET requests should return results in under 2 seconds.
- Support pagination (e.g., 20 items per page).

## 3. Booking System

### Functional Requirements
- Users can book properties for specific date ranges.
- System must prevent double-booking.
- Confirmations should be sent after successful booking.

### API Endpoints
- POST /api/bookings
  - Input: property_id, start_date, end_date
  - Output: Booking confirmation or error
- GET /api/bookings/user
  - Output: List of user bookings

### Validation Rules
- Booking dates must be in the future.
- start_date must be earlier than end_date.

### Performance Criteria
- Booking creation should take less than 3 seconds.
- Conflict checking must be fast and reliable.

## Notes
- All endpoints require token-based authentication.
- Use standard HTTP status codes (200, 400, 401, 404, etc.)
