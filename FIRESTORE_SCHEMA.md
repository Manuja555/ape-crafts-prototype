# cloud firestore schema for ape-crafts prototype (MVP)

this outline the core collections and their expected document structure for the prototype

-----------

## `user` Collection

* **Purpose** Store all the information related to sellers and buyers
* **Document ID** Firebase UID


```json
{
    "email": "user@example.com",
    "userType": "artisan", // or "buyer"
    "name": "The Clay Pot Studio", // Artisan's shop name or Buyer's display name
    "bio": "Hand-crafted pottery from local Sri Lankan clay.", // Optional, for artisans
    "contactNumber": "+94771234567", // Optional, for artisans
    "profileImageUrl": "[https://firebasestorage.googleapis.com/v0/b/](https://firebasestorage.googleapis.com/v0/b/)...", // Optional, URL to Firebase Storage image
    "createdAt": "<timestamp>", // Firebase FieldValue.serverTimestamp()
    "lastActive": "<timestamp>" // Firebase FieldValue.serverTimestamp(), updated on login/activity
}
```
## `product` Collection

* **Purpose** Store all product details listed by the sellers

```json
{
    "sellerID" : "user234",
    "productName" : "Mask kandyan",
    "productDesc":"lorem ipsum",
    "productPrice": 100.00,
    "productImageUrls": ["links.com", "links.com"],
    "productCategory": "jewelry",
    "productTags": ["handmade", "local"],
    "createdAt" : "<timestamp>",
    "AVGratings" : 3.5,
    "status" : "available",
    "reviewCount" : 24,

}
```
## `review` Collection
* **Purpose** Store all reviews left by buyers on products

```json
{
    "productID" : "product_ID_123",
    "BuyerID" : "user123",
    "rating" : 4.5,
    "reviewText" : "lorem ipsum",
    "reviewDate" : "<timestamp>",
    "sentiment" : "positive"
}
```
## `inquiries` Collection
* **Purpose** Store all inquiries made by buyers on products

```json
{

    "productID" : "product_ID_123",
    "BuyerID" : "user123",
    "SellerID" : "seller_ID_123",
    "Status" : "initiated", //responded cancelled resolved initiated
    "createdAt" : "<timestamp>",
    "updatedAt" : "<timestamp>",

    ## `messages` Collection
    * **Purpose** Store all messages exchanged between buyers and sellers during inquiries
    {
        "senderID" : "user123",
        "message" : "lorem ipsum",
        "sentTime" : "<timestamp>"

    }

}



