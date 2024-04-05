# ftgo-order-service-test

Repositori ini merupakan skenario pengujian dan pengujian yang dilakukan pada aplikasi ftgo.

## Authors

- Annisa Dinda Gantini | 211524003
- Berliana Elfada | 211524004
- Cintia Ningsih | 211524005
- Suci Awalia Gardara | 211524027
- Yane Pradita | 211524029

## Test Scenario
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
                        |

