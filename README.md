# ftgo-order-service-test

Repositori ini merupakan skenario pengujian dan pengujian yang dilakukan pada aplikasi ftgo.

## Authors

- Annisa Dinda Gantini | 211524003
- Berliana Elfada | 211524004
- Cintia Ningsih | 211524005
- Suci Awalia Gardara | 211524027
- Yane Pradita | 211524029

## Test Scenario
#### Create Order
- Pengujian kemampuan sistem untuk melakukan penambahan pada order yang sudah dibuat
  - Memastikan order berhasil dibuat dan ditambahkan ke sistem
#### Revise Order
- Pengujian kemampuan sistem untuk melakukan perubahan pada order yang sudah dibuat
  - Memastikan perubahan order berhasil disimpan.
    - Memastikan detail order yang ditampilkan sesuai dengan perubahan yang dilakukan oleh pengguna.
#### Cancel Order
- Pengujian kemampuan sistem untuk membatalkan order yang sudah dibuat
  - Memastikan order berhasil dibatalkan dan dihapus dari sistem

### Endpoint 
    1. Penambahan Order: POST/orders
    2. Perubahan Order: POST/orders/{orderId}/revise
    3. Pembatalan Order: POST/orders/{orderId}/cancel

| Feature       | Create Order                                                   |
|---------------|----------------------------------------------------------------|
| Requirements  | As a consumer of the Order Service, I should be able to create an order |
| Scenario      | 1. Given a valid consumer id and restaurant id                 |
|               | 2. Given invalid consumer id                                  |
|               | 3. Given invalid restaurant id                                |
|               | 4. Given invalid menuItem id                                  |
|               | 5. Order data with incomplete fields                          |

| Feature       | Revise Order                                                   |
|---------------|----------------------------------------------------------------|
| Requirements  | As a consumer of the Order Service, I should be able to revise an order |
| Scenario     | 1. Change the order data with the order ID in the database     |
|               | 2. Change the order menu data whose menu ID is in the database |
|               | 3. Changing order menu data whose menu ID does not exist in the database |
|               | 4. Changing order data with the order ID not existing in the database |

| Feature       | Cancel Order                                                   |
|---------------|----------------------------------------------------------------|
| Requirements  | As a consumer of the Order Service, I should be able to cancel an order |
| Scenario      | 1. Cancellation of an order with the order ID in the database  |
|               | 2. Cancellation of an order with the order ID not in the database |

### Preconditions
Sebelum membuat pesanan harus menambahkan data consumer dan data restaurant terlebih dahulu, kelompok kami membuat data consumer dan data restaurant sebagai berikut : 
 #### Membuat Data Customer
| End Point | POST /consumers create | 
| ---- | ------ | 
| Value | {<br>"name": {<br> "firstName": "Rikeu",<br> "lastName": "Wilson"<br> }<br> }| 
 #### Membuat Data Customer
| End Point            | POST /restaurants create |
|----------------------|---------------------------|
| **Value**            | {<br> "address": {<br> "city": "Bandung",<br> "state": "Jawa Barat",<br> "street1": "Jln Braga",<br> "street2": "Jln Siliwangi",<br> "zip": "40111"<br> },<br> "menu": {<br> "menuItems": [<br> {<br> "id": "F01",<br> "name": "Chicken Katsu",<br> "price": "10.99"<br> },<br> {<br> "id": "F02",<br> "name": "Chicken Curry",<br> "price": "12.99"<br> }<br> ]<br> },<br> "name": "The Little Katsu"<br> } |

## Test Result
### Create Order
#### Scenario-001 : Given a valid consumer ID and restaurant ID
| Scenario            | Given a valid consumer ID and restaurant ID  |
|---------------------|---------------------------------------------|
| Preconditions      | Aplikasi FTGO sudah dijalankan <br> Semua Microservice beroperasi |
| Test Data          | json<br> {<br>   "consumerId": 1,<br>   "deliveryAddress": {<br>     "city": "Cimahi",<br>     "state": "Indonesia",<br>     "street1": "jln Cihanjuang Blok A",<br>     "street2": "jln Cihanjuang Blok B",<br>     "zip": "55578"<br>   },<br>   "deliveryTime": "2024-04-05T12:30:09.913Z",<br>   "lineItems": [<br>     {<br>       "menuItemId": "F01",<br>       "quantity": 1<br>     }<br>   ],<br>   "restaurantId": 1<br> } |
| Step To Execute    | Membuka swagger UI pada localhost:8082/orders/index.html<br> Cari bagian di mana input JSON request body di bagian POST / orders, lalu klik Try it Out.<br> Tuliskan JSON di Test Data untuk membuat pesanan.<br> Klik tombol "Execute" untuk mengirimkan request ke server. |
| Expected Result    | Consumer berhasil melakukan pemesanan, detail pesanan terkait dengan id consumer dan id restaurant. |
| Actual Result      | Pada actual result ini mengkonfirmasi bahwa API untuk membuat pesanan berhasil dijalankan. Sistem telah menerima request untuk membuat pesanan baru  dengan data yang valid, memprosesnya dan menghasilkan orderId: 2 |
| Response body      | json<br> {<br>   "orderId": 2<br> }  |
| Response headers   | connection: keep-alive <br> content-type: application/json <br> date: Fri05 Apr 2024 12:48:11 GMT <br> keep-alive: timeout=60 <br> transfer-encoding: chunked <br> zipkin-trace-id: 8cbcc467db55638c |
| Test Result        | PASS |

#### Scenario-002 : Given invalid consumer id
| Scenario            | Given invalid consumer id                                                                                                    |
|---------------------|------------------------------------------------------------------------------------------------------------------------------|
| Preconditions      | Aplikasi FTGO sudah dijalankan <br> Semua Microservice beroperasi                                                           |
| Test Data          | json <br> {<br>   "consumerId": 5,<br>   "deliveryAddress": {<br>     "city": "Cimahi",<br>     "state": "Indonesia",<br>     "street1": "jln Cihanjuang Blok A",<br>     "street2": "jln Cihanjuang Blok B",<br>     "zip": "55578"<br>   },<br>   "deliveryTime": "2024-04-05T12:30:09.913Z",<br>   "lineItems": [<br>     {<br>       "menuItemId": "F01",<br>       "quantity": 1<br>     }<br>   ],<br>   "restaurantId": 1<br> } |
| Step To Execute    | Membuka swagger UI pada localhost:8082/orders/index.html <br> Cari bagian di mana input JSON request body di bagian POST / orders, lalu klik Try it Out. <br> Tuliskan JSON di Test Data untuk membuat pesanan. <br> Klik tombol "Execute" untuk mengirimkan request ke server. |
| Expected Result    | Proses untuk membuat pesanan gagal. Sistem akan memberikan respons error yang menunjukkan bahwa consumer id yang diberikan invalid atau not found. Kemudian, tidak ada pesanan yang dibuat dan tersimpan pada sistem. |
| Actual Result      | Pada actual result ini mengkonfirmasi bahwa API untuk membuat pesanan berhasil dijalankan. Sistem telah menerima request untuk membuat pesanan baru  dengan data yang valid, memprosesnya dan menghasilkan orderId : 4 |
| Response body      | json <br> {<br>   "orderId": 4<br> } |
| Response headers   | connection: keep-alive <br> content-type: application/json <br> date: Fri05 Apr 2024 13:32:55 GMT <br> keep-alive: timeout=60 <br> transfer-encoding: chunked <br> zipkin-trace-id: af8b1ea624eca55b |
| Test Result        | FAIL |

#### Scenario-003 : Given invalid restaurant id
| Scenario            | Given invalid restaurant id                                                                                                  |
|---------------------|------------------------------------------------------------------------------------------------------------------------------|
| Preconditions      | Aplikasi FTGO sudah dijalankan                                                                                                |
| Test Data          | json <br> { <br>   "consumerId": 1, <br>   "deliveryAddress": { <br>     "city": "Cimahi", <br>     "state": "Indonesia", <br>     "street1": "jln Cihanjuang Blok A", <br>     "street2": "jln Cihanjuang Blok B", <br>     "zip": "55578" <br>   }, <br>   "deliveryTime": "2024-04-05T12:30:09.913Z", <br>   "lineItems": [<br>     {<br>       "menuItemId": "F02",<br>       "quantity": 3<br>     }<br>   ],<br>   "restaurantId": 3 <br> }  |
| Step To Execute    | Membuka swagger UI pada localhost:8082/orders/index.html <br> Cari bagian di mana input JSON request body di bagian POST / orders, lalu klik Try it Out. <br> Tuliskan JSON di Test Data untuk membuat pesanan. <br> Klik tombol "Execute" untuk mengirimkan request ke server. |
| Expected Result    | Proses untuk membuat pesanan gagal. Sistem akan memberikan pesan error yang menunjukkan bahwa restaurant id yang diberikan tidak ditemukan. Kemudian tidak ada pesanan yang dibuat dan disimpan. |
| Actual Result      | Actual result menampilkan pesan error yang menunjukkan bahwa restaurant id yang diberikan tidak ditemukan. Sehingga pesanan gagal dibuat. |
| Response body      | json <br> { <br>   "timestamp": "2024-04-05T12:53:26.323+0000", <br>   "status": 500, <br>   "error": "Internal Server Error", <br>   "message": "Restaurant not found with id 3", <br>   "path": "/orders" <br> }  |
| Response headers   | connection: close <br> content-type: application/json <br> date: Fri05 Apr 2024 12:53:26 GMT <br> transfer-encoding: chunked <br> zipkin-trace-id: 7806d9df9b444886 |
| Test Result        | PASS |

#### Scenario-004 : Given invalid menuItem ID
| Scenario            | Given invalid menuItem ID                                                                                                   |
|---------------------|------------------------------------------------------------------------------------------------------------------------------|
| Preconditions      | Aplikasi FTGO sudah dijalankan                                                                                                |
| Test Data          | json <br> { <br>   "consumerId": 1, <br>   "deliveryAddress": { <br>     "city": "Cimahi", <br>     "state": "Indonesia", <br>     "street1": "jln Cihanjuang Blok A", <br>     "street2": "jln Cihanjuang Blok B", <br>     "zip": "55578" <br>   }, <br>   "deliveryTime": "2024-04-05T12:30:09.913Z", <br>   "lineItems": [<br>     {<br>       "menuItemId": "F05",<br>       "quantity": 1<br>     }<br>   ],<br>   "restaurantId": 1 <br> }  |
| Step To Execute    | Membuka swagger UI pada localhost:8082/orders/index.html <br> Cari bagian di mana input JSON request body di bagian POST / orders, lalu klik Try it Out. <br> Tuliskan JSON di Test Data untuk membuat pesanan. <br> Klik tombol "Execute" untuk mengirimkan request ke server. |
| Expected Result    | Sistem memberikan pesan error yang menunjukkan bahwa menuItem ID yang diberikan invalid atau not found. Pesanan gagal dibuat dan tidak tersimpan ke dalam sistem. |
| Actual Result      | Actual result menunjukkan bahwa sistem memberikan pesan error karena ID menu item invalid. Sehingga, tidak ada pesanan yang dibuat. |
| Response body      | json <br> { <br>   "timestamp": "2024-04-05T12:56:43.016+0000", <br>   "status": 500, <br>   "error": "Internal Server Error", <br>   "message": "Invalid menu item id F05", <br>   "path": "/orders" <br> }  |
| Response headers   | connection: close <br> content-type: application/json <br> date: Fri05 Apr 2024 12:56:43 GMT <br> transfer-encoding: chunked <br> zipkin-trace-id: c6124df38d57bc33 |
| Test Result        | PASS |

#### Scenario-005 : Order data with incomplete fields
| Scenario            | Order data with incomplete fields                                                                                         |
|---------------------|------------------------------------------------------------------------------------------------------------------------------|
| Preconditions      | Aplikasi FTGO sudah dijalankan                                                                                                |
| Test Data          | json <br> { <br>   "consumerId": 1, <br>   "deliveryAddress": { <br>     "city": "Bandung", <br>     "state": "Indonesia", <br>     "zip": "23345" <br>   }, <br>   "deliveryTime": "2024-04-05T15:52:36.893Z", <br>   "lineItems": [<br>     {<br>       "menuItemId": "F01"<br>     }<br>   ],<br>   "restaurantId": 1 <br> }  |
| Step To Execute    | Membuka swagger UI pada localhost:8082/orders/index.html <br> Cari bagian di mana input JSON request body di bagian POST / orders, lalu klik Try it Out. <br> Tuliskan JSON di Test Data untuk membuat pesanan. <br> Klik tombol "Execute" untuk mengirimkan request ke server. |
| Expected Result    |                                                                                                                                 |
| Actual Result      |                                                                                                                                 |
| Response body      | json <br> { <br>   "orderId": 7 <br> }  |
| Response headers   | connection: keep-alive <br> content-type: application/json <br> date: Fri05 Apr 2024 13:00:03 GMT <br> keep-alive: timeout=60 <br> transfer-encoding: chunked <br> zipkin-trace-id: c9824df38d57bc32 |
| Test Result        | FAIL |
