# API Documentation in Siperuka

## Booking Module

### GET /bookings

Retrieve all bookings.

- **Response Example:**

```json
[
  {
    "id": 1,
    "roomId": 2,
    "userId": 3,
    "statusId": 1,
    "date": "2026-02-17",
    "startTime": "09:00:00",
    "endTime": "11:00:00",
    "purpose": "Meeting",
    "room": {
      "id": 2,
      "roomCode": "A101",
      "roomName": "Ruang Rapat",
      "capacity": 10,
      "location": "Gedung A",
      "roomStatus": "Available"
    }
  }
]
```

- **Status Code:** 200 OK

---

### GET /bookings/{id}

Retrieve booking by ID.

- **Response Example:**

```json
{
  "id": 1,
  "roomId": 2,
  "userId": 3,
  "statusId": 1,
  "date": "2026-02-17",
  "startTime": "09:00:00",
  "endTime": "11:00:00",
  "purpose": "Meeting",
  "room": {
    "id": 2,
    "roomCode": "A101",
    "roomName": "Ruang Rapat",
    "capacity": 10,
    "location": "Gedung A",
    "roomStatus": "Available"
  }
}
```

- **Status Code:** 200 OK / 404 Not Found

---

### POST /bookings

Create a new booking.

- **Request Body:**

```json
{
  "roomId": 2,
  "userId": 3,
  "purpose": "Meeting",
  "date": "2026-02-17",
  "startTime": "09:00:00",
  "endTime": "11:00:00"
}
```

- **Response Example:**

```json
{
  "id": 1,
  "roomId": 2,
  "userId": 3,
  "statusId": 1,
  "date": "2026-02-17",
  "startTime": "09:00:00",
  "endTime": "11:00:00",
  "purpose": "Meeting"
}
```

- **Status Code:** 201 Created / 400 Bad Request
- **Validation:**
  - `roomId`, `userId` harus valid dan ada di database
  - `date`, `startTime`, `endTime` harus format valid
  - `purpose` tidak boleh kosong
  - Tidak boleh bentrok dengan booking lain pada waktu yang sama

---

### PUT /bookings/{id}

Update booking by ID.

- **Request Body:**

```json
{
  "date": "2026-02-18",
  "startTime": "10:00:00",
  "endTime": "12:00:00",
  "purpose": "Updated Meeting",
  "statusId": 2
}
```

- **Response Example:**
  _No Content_
- **Status Code:** 204 No Content / 400 Bad Request / 404 Not Found
- **Validation:**
  - `statusId` harus valid
  - `purpose` tidak boleh kosong
  - Tidak boleh bentrok dengan booking lain pada waktu yang sama

---

### DELETE /bookings/{id}

Delete booking by ID (soft delete).

- **Response Example:**

```json
{
  "message": "Data peminjaman berhasil dihapus"
}
```

- **Status Code:** 200 OK / 404 Not Found
- **Validation:**
  - `id` harus valid dan ada di database

---

### PUT /bookings/{id}/status

Update booking status by ID.

- **Request Body:**

```json
{
  "newStatusId": 2,
  "note": "Approved by admin"
}
```

- **Response Example:**

```json
{
  "message": "Status peminjaman berhasil diperbarui"
}
```

- **Status Code:** 200 OK / 400 Bad Request / 404 Not Found
- **Validation:**
  - `newStatusId` harus valid
  - `note` opsional, maksimal 500 karakter

---

## Room Module

### GET /bookings/rooms

Retrieve all rooms.

- **Response Example:**

```json
[
  {
    "id": 1,
    "roomCode": "A101",
    "roomName": "Ruang Rapat",
    "capacity": 10,
    "location": "Gedung A",
    "roomStatus": "Available"
  }
]
```

- **Status Code:** 200 OK

---

### GET /bookings/rooms/{id}

Retrieve room by ID.

- **Response Example:**

```json
{
  "id": 1,
  "roomCode": "A101",
  "roomName": "Ruang Rapat",
  "capacity": 10,
  "location": "Gedung A",
  "roomStatus": "Available"
}
```

- **Status Code:** 200 OK / 404 Not Found

---

### POST /bookings/rooms

Create a new room.

- **Request Body:**

```json
{
  "roomCode": "A101",
  "roomName": "Ruang Rapat",
  "capacity": 10,
  "location": "Gedung A",
  "roomStatus": "Available"
}
```

- **Response Example:**

```json
{
  "id": 1,
  "roomCode": "A101",
  "roomName": "Ruang Rapat",
  "capacity": 10,
  "location": "Gedung A",
  "roomStatus": "Available"
}
```

- **Status Code:** 201 Created / 400 Bad Request
- **Validation:**
  - `roomCode` harus unik
  - `roomName`, `location`, `roomStatus` tidak boleh kosong
  - `capacity` minimal 1

---

### PUT /bookings/rooms/{id}

Update room by ID.

- **Request Body:**

```json
{
  "roomName": "Ruang Rapat Besar",
  "capacity": 20,
  "location": "Gedung B",
  "roomStatus": "Available"
}
```

- **Response Example:**
  _No Content_
- **Status Code:** 204 No Content / 400 Bad Request / 404 Not Found
- **Validation:**
  - `roomName`, `location`, `roomStatus` tidak boleh kosong
  - `capacity` minimal 1

---

### DELETE /bookings/rooms/{id}

Delete room by ID (soft delete).

- **Response Example:**

```json
{
  "message": "Data ruangan berhasil dihapus"
}
```

- **Status Code:** 200 OK / 404 Not Found
- **Validation:**
  - `id` harus valid dan ada di database

---

### GET /bookings/rooms/availability

Check room availability for a date and time range.

- **Request Query:**

```
?date=2026-02-17&startTime=09:00:00&endTime=11:00:00
```

- **Response Example:**

```json
[
  {
    "id": 1,
    "roomCode": "A101",
    "roomName": "Ruang Rapat",
    "capacity": 10,
    "location": "Gedung A",
    "roomStatus": "Available",
    "isAvailable": true
  }
]
```

- **Status Code:** 200 OK / 400 Bad Request
- **Validation:**
  - `endTime` harus setelah `startTime`

---

## User Module

### GET /users

Retrieve all users.

- **Response Example:**

```json
[
  {
    "id": 1,
    "name": "Budi",
    "email": "budi@example.com",
    "role": "USER"
  }
]
```

- **Status Code:** 200 OK

---

### GET /users/{id}

Retrieve user by ID.

- **Response Example:**

```json
{
  "id": 1,
  "name": "Budi",
  "email": "budi@example.com",
  "role": "USER"
}
```

- **Status Code:** 200 OK / 404 Not Found

---

### POST /users

Create a new user.

- **Request Body:**

```json
{
  "name": "Budi",
  "email": "budi@example.com",
  "role": "USER"
}
```

- **Response Example:**

```json
{
  "id": 1,
  "name": "Budi",
  "email": "budi@example.com",
  "role": "USER"
}
```

- **Status Code:** 201 Created / 400 Bad Request
- **Validation:**
  - `name`, `email`, `role` tidak boleh kosong
  - `email` harus format valid dan unik

---

### PUT /users/{id}

Update user by ID.

- **Request Body:**

```json
{
  "name": "Budi Santoso",
  "role": "ADMIN"
}
```

- **Response Example:**
  _No Content_
- **Status Code:** 204 No Content / 400 Bad Request / 404 Not Found
- **Validation:**
  - `name`, `role` tidak boleh kosong

---

### DELETE /users/{id}

Delete user by ID (soft delete).

- **Response Example:**

```json
{
  "message": "Data user berhasil dihapus"
}
```

- **Status Code:** 200 OK / 404 Not Found
- **Validation:**
  - `id` harus valid dan ada di database

---

## Booking Status Module

### GET /booking-statuses

Retrieve all booking statuses.

- **Response Example:**

```json
[
  {
    "id": 1,
    "statusBooking": "pending",
    "statusName": "Pending"
  }
]
```

- **Status Code:** 200 OK

---

### GET /booking-statuses/{id}

Retrieve booking status by ID.

- **Response Example:**

```json
{
  "id": 1,
  "statusBooking": "pending",
  "statusName": "Pending"
}
```

- **Status Code:** 200 OK / 404 Not Found

---

### POST /booking-statuses

Create a new booking status.

- **Request Body:**

```json
{
  "statusBooking": "approved",
  "statusName": "Approved"
}
```

- **Response Example:**

```json
{
  "id": 2,
  "statusBooking": "approved",
  "statusName": "Approved"
}
```

- **Status Code:** 201 Created / 400 Bad Request
- **Validation:**
  - `statusBooking`, `statusName` tidak boleh kosong

---

### PUT /booking-statuses/{id}

Update booking status by ID.

- **Request Body:**

```json
{
  "statusBooking": "rejected",
  "statusName": "Rejected"
}
```

- **Response Example:**
  _No Content_
- **Status Code:** 204 No Content / 400 Bad Request / 404 Not Found
- **Validation:**
  - `statusBooking`, `statusName` tidak boleh kosong

---

### DELETE /booking-statuses/{id}

Delete booking status by ID.

- **Response Example:**

```json
{
  "message": "Status booking berhasil dihapus"
}
```

- **Status Code:** 200 OK / 404 Not Found
- **Validation:**
  - `id` harus valid dan ada di database

---

## Booking History Module

### GET /booking-histories

Retrieve all booking histories.

- **Response Example:**

```json
[
  {
    "id": 1,
    "bookingId": 1,
    "oldStatus": 1,
    "newStatus": 2,
    "changedBy": 3,
    "changedAt": "2026-02-17T09:00:00Z",
    "note": "Approved by admin"
  }
]
```

- **Status Code:** 200 OK

---

### GET /booking-histories/{id}

Retrieve booking history by ID.

- **Response Example:**

```json
{
  "id": 1,
  "bookingId": 1,
  "oldStatus": 1,
  "newStatus": 2,
  "changedBy": 3,
  "changedAt": "2026-02-17T09:00:00Z",
  "note": "Approved by admin"
}
```

- **Status Code:** 200 OK / 404 Not Found

---

### POST /booking-histories

Create a new booking history.

- **Request Body:**

```json
{
  "bookingId": 1,
  "oldStatus": 1,
  "newStatus": 2,
  "changedBy": 3,
  "note": "Approved by admin"
}
```

- **Response Example:**

```json
{
  "id": 1,
  "bookingId": 1,
  "oldStatus": 1,
  "newStatus": 2,
  "changedBy": 3,
  "changedAt": "2026-02-17T09:00:00Z",
  "note": "Approved by admin"
}
```

- **Status Code:** 201 Created / 400 Bad Request
- **Validation:**
  - `bookingId`, `oldStatus`, `newStatus`, `changedBy` harus valid dan ada di database
  - `note` opsional, maksimal 500 karakter

---