1) Retrieve All Bookings (GET)
Request:
Sends a GET request to retrieve the list of all booking IDs available in the system.
Response:
Returns 200 OK with a JSON array containing all booking IDs.
2) Retrieve Particular Booking (GET)
Request:
Sends a GET request with a booking ID in the URL to fetch the details of that booking.
Response:
Returns 200 OK with the booking information such as customer name, booking dates, total price, and additional needs.
3) Generate Token (POST)
Request:
Sends the username and password in the request body to generate an authentication token.
Response:
Returns 200 OK with a token that is used for authorized requests like PUT, PATCH and DELETE.
4) Create Booking (POST)
Request:
Sends customer booking details in JSON format to create a new booking.
Response:
Returns 200 OK with the newly created booking ID and booking details.
5) Update Booking (PUT)
Request:
Sends the complete updated booking details along with a valid Cookie token to replace the existing booking information.
Response:
Returns 200 OK with the updated booking details.
6) Patch Booking (PATCH)
Request:
Sends only the fields that need to be modified along with a valid Cookie token.
Response:
Returns 200 OK with the updated booking information.
7) Delete Booking (DELETE)
Request:
Sends a DELETE request with the booking ID and valid Cookie token to remove the booking.
Response:
Returns 201 Created, indicating the booking was successfully deleted.
2. Improve Negative Scenarios
Current
While generating Bearer Token for Authorization, then body requires username and password.
Replace with
Negative Scenario 1
Scenario: Generate token using an incorrect username or password.
Expected Result: API should reject the request and return 401 Unauthorized.
Actual Result: API returned 401 Unauthorized.
Current
While deleting booking we need to enter token value and cookie key.
Replace with
Negative Scenario 2
Scenario: Delete a booking without providing a valid Cookie token.
Expected Result: API should deny access and return 403 Forbidden.
Actual Result: API returned 403 Forbidden.
