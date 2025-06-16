# firebase cloud functions for the ape-crafts API blueprint

 outlines the essential Firebase Cloud Functions that will serve as the backend API for the Ape Crafts prototype, as well as background functions for AI processing.

 ## Callable Functions / HTTPS- Triggered Functions

 1. **`AddOrUpdateProfile` (Callable function)**
    * **Purpose :** Handling user profile creation after registration or updating existing user profile. Ensuring that the `User Type` is set correctly and the other profile fields are safely stored.
    * **Input :** `user_id`, `user_type`, `email`, `phone_number`, `bio`(optional), `profileImgURL` (optional)
    * **Output :** Success / Error message

2. **`Addproduct` (Callable function)**
    * **Purpose :** Handling product creation for Sellers. Ensures the product details are stored acurately.
    * **Input :**  `UID`,' `product_id`, `product_name`, `product_description`, `price`, `Category`, `Image URL`
    * **Output :** `ProductID` of the new product.

3. **`UpdateProduct` (Callable Function)**
    * **purpose "** Updating existing product details for Sellers.
    * **Input :** `UID`, `ProductID`, and the fields to be updated {`product_id`, `product_name`, `product_description`, `price`, `Category`, `Image URL`}
    * **Output :** Success / Error message

4. **`DeleteProduct` (Callable Function)**
    * **Purpose :** Deleting a product from the database for Sellers.
    * **Input :** `UID`, `ProductID`
    * **Output :** Success / Error message

5. **`InitiatePurchaseInquiry` (Callable Function)**
    * **Purpose :** creating a new `inquiry` document when the buyer show ineterst in a product.
    * **Input :** `BuyerID`, `ProductID`, `SellerID`, 
    * **Output :** `InquiryID` of the new inquiry document.

6. **`SendMessage` (Callable Function)** 
    * **Purpose :** Adds a new message document to the `messages` sub-collection within a specific `inquiry`
    * **Input :** `text`, `SenderID`, `InquiryID`,
    * **Output :** Success / Error message

7. **`SendReview` (Callable Function)**
    * **Purpose :** Adds a new review document to the `reviews` sub-collection within a specific `product`
    * **Input :** `text`, `SenderID`, `ProductID`, `Rating`,
    * **Output :** `ReviewerID` / Error message

8. **`GetTrendInsights` (Callable Function)**
    * **Purpose :** Returns simple AI-driven insights (e.g., top 3 categories by number of listings, most inquired      products) by querying Firestore and applying basic Python logic
    * **Input :** None
    * **Output :** A JSON Object containing the insights

9. **`processPayment` (HTTP Trigger)**
    * **Purpose:** Serves as a secure endpoint for handling callbacks/requests from external Sri Lankan payment gateways. Protects API keys and sensitive transaction logic.
    * **Inputs:** Payment gateway specific payload.
    * **Outputs:** Payment confirmation/error to the gateway, and updates Firestore accordingly.
-----

## Background-Triggered Functions (Automated)

1.  **`analyzeReviewSentiment` (Firestore Trigger: `onCreate` or `onWrite` on `reviews` collection)**
    * **Purpose:** This function triggers automatically whenever a new `review` document is created in Firestore. It will perform sentiment analysis on the `text` field using Python (NLTK/Scikit-Learn).
    * **Inputs:** The new `review` document data.
    * **Outputs:** Updates the `sentiment` field within the original `reviews` document. (Optional: Could also update `averageRating` and `reviewCount` fields in the associated `product` document).
