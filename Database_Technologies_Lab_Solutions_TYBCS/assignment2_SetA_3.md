# Assignment 2 — Set C
## Hotel Database

## 1. Create database and collections

```javascript
use Hotel

db.createCollection("Customer")
db.createCollection("Room")
db.createCollection("Booking")
```

## 2. Insert 10 Customers

```javascript
db.Customer.insertMany([
  {customerId:"101",name:"Rani",contactNumber:"9845671237",email:"rani@example.com",address:"Satara"},
  {customerId:"102",name:"Amit",contactNumber:"9845671238",email:"amit@example.com",address:"Pune"},
  {customerId:"103",name:"Priya",contactNumber:"9845671239",email:"priya@example.com",address:"Mumbai"},
  {customerId:"104",name:"Rahul",contactNumber:"9845671240",email:"rahul@example.com",address:"Satara"},
  {customerId:"105",name:"Sneha",contactNumber:"9845671241",email:"sneha@example.com",address:"Nashik"},
  {customerId:"106",name:"Karan",contactNumber:"9845671242",email:"karan@example.com",address:"Pune"},
  {customerId:"107",name:"Neha",contactNumber:"9845671243",email:"neha@example.com",address:"Kolhapur"},
  {customerId:"108",name:"Rohan",contactNumber:"9845671244",email:"rohan@example.com",address:"Satara"},
  {customerId:"109",name:"Pooja",contactNumber:"9845671245",email:"pooja@example.com",address:"Pune"},
  {customerId:"110",name:"Vikas",contactNumber:"9845671246",email:"vikas@example.com",address:"Mumbai"}
])
```

## 3. Insert 10 Rooms

```javascript
db.Room.insertMany([
  {roomNumber:101,roomType:"Deluxe",rentPerDay:3500,availabilityStatus:"Available"},
  {roomNumber:102,roomType:"Standard",rentPerDay:2200,availabilityStatus:"Booked"},
  {roomNumber:103,roomType:"Suite",rentPerDay:6000,availabilityStatus:"Available"},
  {roomNumber:104,roomType:"Deluxe",rentPerDay:3500,availabilityStatus:"Available"},
  {roomNumber:105,roomType:"Standard",rentPerDay:2200,availabilityStatus:"Available"},
  {roomNumber:106,roomType:"Suite",rentPerDay:6000,availabilityStatus:"Booked"},
  {roomNumber:107,roomType:"Deluxe",rentPerDay:3500,availabilityStatus:"Booked"},
  {roomNumber:108,roomType:"Standard",rentPerDay:2200,availabilityStatus:"Available"},
  {roomNumber:109,roomType:"Deluxe",rentPerDay:3500,availabilityStatus:"Available"},
  {roomNumber:110,roomType:"Suite",rentPerDay:6000,availabilityStatus:"Available"}
])
```

## 4. Insert 10 Bookings

```javascript
db.Booking.insertMany([
  {bookingId:"B101",customerName:"Rani",roomNumber:101,checkInDate:ISODate("2026-09-01"),checkOutDate:ISODate("2026-09-03"),totalBill:7000},
  {bookingId:"B102",customerName:"Amit",roomNumber:102,checkInDate:ISODate("2026-09-02"),checkOutDate:ISODate("2026-09-04"),totalBill:4400},
  {bookingId:"B103",customerName:"Priya",roomNumber:103,checkInDate:ISODate("2026-09-03"),checkOutDate:ISODate("2026-09-05"),totalBill:12000},
  {bookingId:"B104",customerName:"Rahul",roomNumber:104,checkInDate:ISODate("2026-09-04"),checkOutDate:ISODate("2026-09-06"),totalBill:7000},
  {bookingId:"B105",customerName:"Sneha",roomNumber:105,checkInDate:ISODate("2026-09-05"),checkOutDate:ISODate("2026-09-07"),totalBill:4400},
  {bookingId:"B106",customerName:"Karan",roomNumber:106,checkInDate:ISODate("2026-09-06"),checkOutDate:ISODate("2026-09-08"),totalBill:12000},
  {bookingId:"B107",customerName:"Neha",roomNumber:107,checkInDate:ISODate("2026-09-07"),checkOutDate:ISODate("2026-09-09"),totalBill:7000},
  {bookingId:"B108",customerName:"Rohan",roomNumber:108,checkInDate:ISODate("2026-09-08"),checkOutDate:ISODate("2026-09-10"),totalBill:4400},
  {bookingId:"B109",customerName:"Pooja",roomNumber:109,checkInDate:ISODate("2026-09-09"),checkOutDate:ISODate("2026-09-11"),totalBill:7000},
  {bookingId:"B110",customerName:"Vikas",roomNumber:110,checkInDate:ISODate("2026-09-10"),checkOutDate:ISODate("2026-09-12"),totalBill:12000}
])
```

## 5. Display all documents

```javascript
db.Customer.find().pretty()
db.Room.find().pretty()
db.Booking.find().pretty()
```

## 6. Delete customers 102, 105 and 107

```javascript
db.Customer.deleteMany({ customerId: { $in: ["102", "105", "107"] } })
```

## 7. Find Booking by Booking ID

```javascript
db.Booking.find({ bookingId: "B103" })
```

## 8. Count Customers and Rooms

```javascript
db.Customer.countDocuments()
db.Room.countDocuments()
```

## 9. Find customers from Satara

```javascript
db.Customer.find({ address: "Satara" })
```

## 10. Remove a specific booking

```javascript
db.Booking.deleteOne({ bookingId: "B110" })
```

## 11. Display Rani with specified contact number

```javascript
db.Customer.find({
  name: "Rani",
  contactNumber: "9845671237"
})
```

## 12. Display a room number and rent

```javascript
db.Room.find(
  { roomNumber: 101 },
  { _id: 0, roomNumber: 1, rentPerDay: 1 }
)
```

## 13. Remove booking by customer name

```javascript
db.Booking.deleteOne({ customerName: "Vikas" })
```

## 14. Find rooms by availability

```javascript
db.Room.find({ availabilityStatus: "Available" })
```

## 15. Find Deluxe rooms

```javascript
db.Room.find({ roomType: "Deluxe" })
```

## 16. Remove all Customer documents

```javascript
db.Customer.deleteMany({})
```

## 17. Delete all documents in Booking

```javascript
db.Booking.deleteMany({})
```

## 18. Drop Hotel database

```javascript
db.dropDatabase()
```

## Result
The Hotel database and all three collections were created and the required insert, search, count, delete, and database-drop operations were implemented.
