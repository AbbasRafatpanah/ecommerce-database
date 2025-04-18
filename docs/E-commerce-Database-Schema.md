# E-commerce Database Schema

## Core User Management System

### Users
- **id**: Unique identifier for each user
- **fullName**: User's complete name
- **profilePhoto**: Path to user's profile image
- **phoneNumber**: Contact phone number
- **isPhoneActived**: Boolean indicating if phone is verified
- **nationalCode**: National identification number
- **birthdate**: User's date of birth
- **job**: User's occupation
- **email**: Email address (for login and notifications)
- **password**: Encrypted password
- **registerDate**: Account creation date
- **role_id**: Foreign key to Roles table
- **lastLoginDate**: Last successful login timestamp (NEW)
- **isActive**: Account active status (NEW)
- **referralCode**: Unique code for referral program (NEW)
- **loyaltyPoints**: Reward points balance (NEW)
- **preferredLanguage**: User's language preference (NEW)
- **marketingConsent**: Boolean for marketing communications (NEW)

### Roles
- **id**: Unique identifier for each role
- **name**: Role name (e.g., Customer, Admin, Moderator)
- **description**: Detailed role description (NEW)
- **isDefault**: Whether this is a default role for new users (NEW)

### Permissions
- **id**: Unique identifier
- **permissionName**: Name of permission
- **parent_id**: For hierarchical permissions
- **description**: Explains what the permission allows (NEW)
- **isActive**: Whether permission is active (NEW)

### Role_permission
- **id**: Unique identifier
- **role_id**: Foreign key to Roles
- **permission_id**: Foreign key to Permissions

### UserAuthentication (NEW)
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **twoFactorEnabled**: Whether 2FA is activated
- **twoFactorMethod**: Method (SMS, email, app)
- **backupCodes**: Encrypted recovery codes
- **lastPasswordChange**: Date of last password update

### UserSessions (NEW)
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **token**: Session token
- **ipAddress**: IP address
- **userAgent**: Browser/device info
- **startTime**: Session start
- **lastActivity**: Last activity time
- **isActive**: Whether session is active

### UserNotifications (NEW)
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **type**: Notification type
- **title**: Notification title
- **message**: Notification content
- **isRead**: Read status
- **createdAt**: Creation timestamp
- **relatedEntityType**: Related entity (order, product, etc.)
- **relatedEntityId**: ID of related entity

### UserActivity (NEW)
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **activityType**: Type of activity
- **description**: Activity description
- **ipAddress**: IP address
- **timestamp**: When activity occurred
- **metadata**: Additional data (JSON)

### SocialMediaConnections (NEW)
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **provider**: Social media platform
- **providerId**: User ID on that platform
- **accessToken**: Encrypted access token
- **profileUrl**: Link to social profile
- **connectedAt**: Connection date

## Address Management

### Addresses
- **id**: Unique identifier
- **fullAddress**: Complete address
- **postalCode**: Postal/ZIP code
- **houseNumber**: Building/house number
- **receiverFirstName**: Recipient first name
- **receiverLastName**: Recipient last name
- **phone**: Contact phone
- **vahed**: Unit/apartment number
- **city_id**: Foreign key to cities
- **latitude**: Geographic coordinate (NEW)
- **longitude**: Geographic coordinate (NEW)
- **addressLabel**: Label for address (Home, Work, etc.) (NEW)
- **instructions**: Delivery instructions (NEW)

### address_users
- **id**: Unique identifier
- **address_id**: Foreign key to Addresses
- **user_id**: Foreign key to Users
- **isDefault**: Whether this is user's default address (NEW)

### cities
- **id**: Unique identifier
- **cityName**: Name of city
- **parent_id**: Parent region/state
- **countryCode**: ISO country code (NEW)
- **stateCode**: State/province code (NEW)
- **postcode**: Default postal code prefix (NEW)
- **timezone**: City timezone (NEW)

## Product Management

### categories
- **id**: Unique identifier
- **name**: Category name
- **url**: SEO-friendly URL slug
- **imageName**: Category image
- **isActived**: Active status
- **isMain**: Whether it's a main category
- **type**: Category type
- **description**: Category description
- **parent_id**: Parent category
- **metaTitle**: SEO title (NEW)
- **metaDescription**: SEO description (NEW)
- **metaKeywords**: SEO keywords (NEW)
- **displayOrder**: Sorting order (NEW)
- **showInMenu**: Whether to show in navigation (NEW)
- **icon**: Icon identifier/class (NEW)

### products
- **id**: Unique identifier
- **name**: Product name
- **url**: SEO-friendly URL slug
- **createDate**: Creation date
- **updateDate**: Last update date
- **imageName**: Main product image
- **isPublish**: Publication status
- **description**: Product description
- **brand_id**: Foreign key to brands
- **sku**: Stock keeping unit (NEW)
- **barcode**: Product barcode (NEW)
- **weight**: Product weight (NEW)
- **dimensions**: Product dimensions (NEW)
- **metaTitle**: SEO title (NEW)
- **metaDescription**: SEO description (NEW)
- **metaKeywords**: SEO keywords (NEW)
- **isDigital**: Whether product is digital (NEW)
- **hasVariants**: Whether product has variants (NEW)
- **minPurchaseQty**: Minimum order quantity (NEW)
- **maxPurchaseQty**: Maximum order quantity (NEW)
- **averageRating**: Calculated average rating (NEW)
- **reviewCount**: Number of reviews (NEW)
- **videoUrl**: Product demo video (NEW)

### category_products
- **id**: Unique identifier
- **category_id**: Foreign key to categories
- **product_id**: Foreign key to products
- **isPrimary**: Whether it's the primary category (NEW)
- **displayOrder**: Display order within category (NEW)

### brands
- **id**: Unique identifier
- **name**: Brand name
- **url**: SEO-friendly URL slug
- **imageName**: Brand logo
- **description**: Brand description
- **foundedYear**: Year founded (NEW)
- **countryOfOrigin**: Country of origin (NEW)
- **websiteUrl**: Brand website (NEW)
- **isOfficial**: Whether it's an official partner (NEW)
- **metaTitle**: SEO title (NEW)
- **metaDescription**: SEO description (NEW)

### images
- **id**: Unique identifier
- **imageName**: Image file name
- **type**: Image type
- **parent_id**: ID of parent entity
- **altText**: Alternative text (NEW)
- **title**: Image title (NEW)
- **displayOrder**: Display order (NEW)
- **size**: File size (NEW)
- **width**: Image width (NEW)
- **height**: Image height (NEW)

### productReviews
- **id**: Unique identifier
- **review**: Full review text
- **abstractReview**: Review summary
- **positivePoints**: Positive aspects
- **negativePoints**: Negative aspects
- **summary**: Review summary
- **product_id**: Foreign key to products
- **user_id**: Reviewer (Foreign key to Users) (NEW)
- **rating**: Numerical rating (NEW)
- **verified**: Whether reviewer purchased product (NEW)
- **helpfulCount**: Number of users finding review helpful (NEW)
- **reportCount**: Number of reports for inappropriate content (NEW)
- **createdAt**: Review date (NEW)
- **status**: Review status (pending/approved/rejected) (NEW)
- **adminResponse**: Response from seller/admin (NEW)

### property
- **id**: Unique identifier
- **title**: Property title
- **type**: Property type
- **helpText**: Explanatory text
- **value**: Property value
- **isKeyProp**: Whether it's a key property
- **product_id**: Foreign key to products
- **isFilterable**: Whether can be used in filters (NEW)
- **isComparable**: Whether can be used in comparisons (NEW)
- **displayOrder**: Display order (NEW)
- **unit**: Measurement unit (NEW)

### ProductTags (NEW)
- **id**: Unique identifier
- **name**: Tag name
- **slug**: SEO-friendly URL slug
- **description**: Tag description
- **createdAt**: Creation date

### ProductTagRelations (NEW)
- **id**: Unique identifier
- **product_id**: Foreign key to products
- **tag_id**: Foreign key to ProductTags

### RelatedProducts (NEW)
- **id**: Unique identifier
- **product_id**: Foreign key to products
- **related_product_id**: Foreign key to products
- **relationType**: Relation type (similar, accessory, upsell, etc.)
- **displayOrder**: Display order

### ProductBundles (NEW)
- **id**: Unique identifier
- **name**: Bundle name
- **description**: Bundle description
- **discount**: Discount percentage
- **startDate**: Availability start
- **endDate**: Availability end
- **isActive**: Active status

### ProductBundleItems (NEW)
- **id**: Unique identifier
- **bundle_id**: Foreign key to ProductBundles
- **product_id**: Foreign key to products
- **quantity**: Product quantity in bundle
- **price**: Optional custom price

### DigitalProductFiles (NEW)
- **id**: Unique identifier
- **product_id**: Foreign key to products
- **filename**: File name
- **filePath**: Path to file
- **fileSize**: Size in bytes
- **downloadCount**: Number of downloads
- **maxDownloads**: Maximum allowed downloads
- **expiryDays**: Days until download link expires
- **version**: File version

## Product Inventory and Pricing

### guarantees
- **id**: Unique identifier
- **title**: Guarantee title
- **description**: Detailed description (NEW)
- **durationMonths**: Duration in months (NEW)
- **coverageType**: What's covered (NEW)
- **provider**: Who provides the guarantee (NEW)
- **terms**: Terms and conditions (NEW)

### sellers
- **id**: Unique identifier
- **name**: Seller name
- **phone**: Contact phone
- **registerDate**: Registration date
- **userName**: Login username
- **password**: Encrypted password
- **email**: Contact email
- **timleySupply**: Timely supply rating
- **postingWarranty**: Posting warranty
- **returnedStatus**: Return policy status
- **purchaseConsent**: Purchase consent
- **voteCount**: Number of votes
- **balance**: Account balance
- **recieves**: Payments received
- **deliveryTime**: Average delivery time
- **storeDescription**: Business description (NEW)
- **storeLogo**: Logo image (NEW)
- **storeSlug**: SEO-friendly URL (NEW)
- **taxId**: Tax identification (NEW)
- **bankAccountInfo**: Payment details (NEW)
- **verificationStatus**: Account verification status (NEW)
- **commissionRate**: Platform commission percentage (NEW)
- **sellerLevel**: Seller level/tier (NEW)

### sellersPrices
- **id**: Unique identifier
- **price**: Regular price
- **offerPrice**: Sale price
- **count**: Inventory count
- **sellersInventoryCount**: Seller's inventory
- **maxPurchaseCount**: Maximum purchase quantity
- **completelySatisfied**: Rating count
- **Satisfied**: Rating count
- **neutral**: Rating count
- **disSatisfied**: Rating count
- **completelyDisSatisfied**: Rating count
- **guarantee_id**: Foreign key to guarantees
- **productOption_id**: Foreign key to productOption
- **product_id**: Foreign key to products
- **seller_id**: Foreign key to sellers
- **costPrice**: Seller's cost (NEW)
- **isDefault**: Whether default offer for product (NEW)
- **leadTime**: Processing time before shipping (NEW)
- **availabilityStatus**: In stock, backorder, etc. (NEW)
- **minimumOrderQuantity**: Minimum order quantity (NEW)
- **restockDate**: Expected restock date if out of stock (NEW)

### productPrices
- **id**: Unique identifier
- **submitDate**: Submission date
- **price**: Regular price
- **discountPersent**: Discount percentage
- **discountPrice**: Discounted price
- **isAvailable**: Availability status
- **sellerPrice_id**: Foreign key to sellersPrices
- **productOptions_id**: Foreign key to productOptions
- **specialOfferText**: Promotional text (NEW)
- **startDate**: Promotional price start date (NEW)
- **endDate**: Promotional price end date (NEW)
- **isDefaultPrice**: Whether this is default price (NEW)

### productOptions
- **id**: Unique identifier
- **type**: Option type
- **name**: Option name
- **value**: Option value
- **displayOrder**: Display order (NEW)
- **priceModifier**: Price adjustment amount (NEW)
- **priceModifierType**: Fixed or percentage (NEW)
- **sku**: SKU extension for this option (NEW)
- **image**: Option image (like color swatch) (NEW)

### InventoryHistory (NEW)
- **id**: Unique identifier
- **seller_id**: Foreign key to sellers
- **product_id**: Foreign key to products
- **productOption_id**: Foreign key to productOptions
- **previousCount**: Previous inventory count
- **newCount**: Updated inventory count
- **changeReason**: Reason for change
- **changeDate**: Date of inventory change
- **changedBy**: User who made the change
- **notes**: Additional notes

### TierPricing (NEW)
- **id**: Unique identifier
- **sellerPrice_id**: Foreign key to sellersPrices
- **minimumQuantity**: Minimum quantity for tier
- **price**: Price at this tier
- **discount**: Discount percentage

## Customer Engagement

### comments
- **id**: Unique identifier
- **title**: Comment title
- **comment**: Comment content
- **positivePoints**: Positive aspects
- **negativePoints**: Negative aspects
- **isSuggested**: Recommendation status
- **isConfirmed**: Moderation status
- **product_id**: Foreign key to products
- **user_id**: Foreign key to Users
- **rating**: Star rating (NEW)
- **commentDate**: Date posted (NEW)
- **helpfulCount**: Number of helpful votes (NEW)
- **reportCount**: Number of inappropriate reports (NEW)
- **purchaseVerified**: Whether from verified purchaser (NEW)
- **adminResponse**: Response from seller/admin (NEW)

### questions
- **id**: Unique identifier
- **question**: Question text
- **createDate**: Creation date
- **answerCount**: Number of answers
- **isConfirmed**: Moderation status
- **user_id**: Foreign key to Users
- **product_id**: Foreign key to products
- **status**: Question status (NEW)
- **isHelpful**: Whether marked as helpful (NEW)
- **helpfulCount**: Number of helpful votes (NEW)
- **viewCount**: Number of views (NEW)

### answers
- **id**: Unique identifier
- **answer**: Answer text
- **like**: Number of likes
- **createDate**: Creation date
- **isConfirmed**: Moderation status
- **user_id**: Foreign key to Users
- **question_id**: Foreign key to questions
- **isBestAnswer**: Whether marked as best answer (NEW)
- **isFromSeller**: Whether from product seller (NEW)
- **isFromAdmin**: Whether from admin (NEW)
- **helpfulCount**: Number of helpful votes (NEW)
- **unhelpfulCount**: Number of unhelpful votes (NEW)

### comment_user_like
- **id**: Unique identifier
- **isLiked**: Like status
- **comment_id**: Foreign key to comments
- **user_id**: Foreign key to Users
- **timestamp**: When like was given (NEW)

### answer_user_like
- **id**: Unique identifier
- **isLiked**: Like status
- **answer_id**: Foreign key to answers
- **user_id**: Foreign key to Users
- **timestamp**: When like was given (NEW)

### ProductSubscriptions (NEW)
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **product_id**: Foreign key to products
- **notificationType**: Type of notification
- **createdAt**: Subscription date
- **isActive**: Active status

### UserWishlists (NEW)
- **id**: Unique identifier
- **name**: Wishlist name
- **description**: Wishlist description
- **isPublic**: Privacy status
- **createdAt**: Creation date
- **user_id**: Foreign key to Users

### WishlistItems (NEW)
- **id**: Unique identifier
- **wishlist_id**: Foreign key to UserWishlists
- **product_id**: Foreign key to products
- **addedAt**: Date added
- **notes**: User notes
- **priority**: User priority level

### ProductComparisons (NEW)
- **id**: Unique identifier
- **sessionId**: Browser session ID
- **user_id**: Foreign key to Users (optional)
- **createdAt**: Creation time
- **updatedAt**: Last update time

### ComparisonItems (NEW)
- **id**: Unique identifier
- **comparison_id**: Foreign key to ProductComparisons
- **product_id**: Foreign key to products
- **addedAt**: Date added

## Marketing & Promotions

### promotions
- **id**: Unique identifier
- **type**: Promotion type
- **startDate**: Start date
- **endDate**: End date
- **dateProductAdd**: Date products were added
- **campainName**: Campaign name
- **category_id**: Foreign key to categories
- **brand_id**: Foreign key to brands
- **description**: Promotion details (NEW)
- **discountType**: Percentage or fixed amount (NEW)
- **discountValue**: Discount amount/percentage (NEW)
- **couponCode**: Optional coupon code (NEW)
- **usageLimit**: Maximum usage count (NEW)
- **usageCount**: Current usage count (NEW)
- **minimumOrderAmount**: Order threshold (NEW)
- **isActive**: Active status (NEW)
- **applyToShipping**: Whether applies to shipping (NEW)

### addToPromotions
- **id**: Unique identifier
- **price**: Promotional price
- **count**: Inventory count
- **maxOrderCount**: Maximum order quantity
- **reminingCount**: Remaining inventory
- **type**: Promotion type
- **startDate**: Start date
- **endDate**: End date
- **sellersprice_id**: Foreign key to sellersPrices
- **promotion_id**: Foreign key to promotions
- **listingPriority**: Display priority (NEW)
- **promotionalText**: Marketing message (NEW)
- **soldCount**: Number of units sold (NEW)

### discountCode
- **id**: Unique identifier
- **count**: Usage count
- **startDate**: Start date
- **endDate**: End date
- **value**: Discount value
- **minOrderPrice**: Minimum order value
- **maxUse**: Maximum usage count
- **firstOrder**: First order only flag
- **product_id**: Foreign key to products
- **code**: Actual coupon code (NEW)
- **discountType**: Percentage or fixed (NEW)
- **description**: Coupon description (NEW)
- **isActive**: Active status (NEW)
- **usageLimit**: Total usage limit (NEW)
- **perUserLimit**: Usage limit per user (NEW)
- **usedCount**: Times already used (NEW)
- **categories**: Applicable categories (NEW)

### banners
- **id**: Unique identifier
- **type**: Banner type
- **title**: Banner title
- **imageName**: Banner image
- **url**: Click destination
- **isActive**: Active status
- **startDate**: Start date (NEW)
- **endDate**: End date (NEW)
- **position**: Display position (NEW)
- **displayOrder**: Display order (NEW)
- **impressions**: View count (NEW)
- **clicks**: Click count (NEW)
- **targetDevice**: Desktop/mobile/all (NEW)
- **description**: Banner description (NEW)

### LoyaltyProgram (NEW)
- **id**: Unique identifier
- **name**: Program name
- **description**: Program description
- **pointsPerCurrency**: Points earned per currency unit
- **minimumRedeemPoints**: Minimum points for redemption
- **conversionRate**: Points to currency conversion
- **expiryMonths**: Months until points expire
- **isActive**: Program active status

### LoyaltyHistory (NEW)
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **points**: Points earned/redeemed
- **type**: Earn or redeem
- **description**: Transaction description
- **orderId**: Related order if applicable
- **createdAt**: Transaction date
- **expiryDate**: When points expire
- **balance**: Current balance after transaction

### GiftCards (NEW)
- **id**: Unique identifier
- **code**: Gift card code
- **initialValue**: Starting value
- **currentBalance**: Remaining balance
- **currency**: Currency code
- **createdAt**: Creation date
- **expiryDate**: Expiration date
- **purchaser_id**: Foreign key to Users (buyer)
- **recipient_id**: Foreign key to Users (recipient)
- **recipientEmail**: Email for delivery
- **recipientName**: Recipient name
- **message**: Personal message
- **status**: Active/redeemed/expired
- **isDigital**: Digital or physical card

### ReferralProgram (NEW)
- **id**: Unique identifier
- **name**: Program name
- **description**: Program description
- **referrerReward**: Reward for referrer
- **referredReward**: Reward for new customer
- **minimumOrderAmount**: Order threshold for reward
- **isActive**: Program active status
- **termsAndConditions**: Program terms

### Referrals (NEW)
- **id**: Unique identifier
- **referrer_id**: Foreign key to Users (referrer)
- **referred_id**: Foreign key to Users (new customer)
- **referralCode**: Tracking code used
- **status**: Pending/completed/rewarded
- **registeredAt**: Registration date
- **firstOrderId**: First order ID
- **rewardStatus**: Reward status
- **referrerRewardId**: Referrer reward reference
- **referredRewardId**: New customer reward reference

### EmailCampaigns (NEW)
- **id**: Unique identifier
- **name**: Campaign name
- **subject**: Email subject
- **content**: Email content (HTML)
- **targetSegment**: Target user segment
- **scheduledDate**: Scheduled send date
- **status**: Draft/scheduled/sent
- **sentCount**: Number of recipients
- **openCount**: Open count
- **clickCount**: Click count
- **createdBy**: Creator user ID

### AbandonedCartRecovery (NEW)
- **id**: Unique identifier
- **cart_id**: Foreign key to carts
- **user_id**: Foreign key to Users
- **emailSent**: Whether email was sent
- **emailSentAt**: Email send time
- **recovered**: Whether cart was recovered
- **recoveredAt**: Recovery timestamp
- **discount_id**: Potential recovery incentive

## Shopping Experience

### carts
- **id**: Unique identifier
- **coockie**: Session cookie
- **updateDate**: Last update
- **shippingType**: Shipping method
- **user_id**: Foreign key to Users
- **address_id**: Foreign key to Addresses
- **sellersPrice_id**: Foreign key to sellersPrices
- **createdAt**: Creation date (NEW)
- **status**: Active/abandoned/converted (NEW)
- **couponCode**: Applied coupon (NEW)
- **ip**: User IP address (NEW)
- **userAgent**: Browser info (NEW)
- **currency**: Currency code (NEW)
- **subtotal**: Items subtotal (NEW)
- **discountAmount**: Total discounts (NEW)
- **taxAmount**: Total taxes (NEW)
- **shippingAmount**: Shipping cost (NEW)
- **grandTotal**: Final amount (NEW)

### cartDetails
- **id**: Unique identifier
- **count**: Item quantity
- **price**: Price at addition time
- **cart_id**: Foreign key to carts
- **sellersPrice_id**: Foreign key to sellersPrices
- **addedAt**: Date added to cart (NEW)
- **productOption_id**: Foreign key to productOptions (NEW)
- **isGift**: Whether item is a gift (NEW)
- **giftMessage**: Gift message (NEW)
- **customizationData**: Custom options JSON (NEW)

### favoriteLists
- **id**: Unique identifier
- **coockie**: Session cookie
- **updateDate**: Last update
- **user_id**: Foreign key to Users
- **name**: List name (NEW)
- **isPublic**: Privacy setting (NEW)
- **shareUrl**: Shareable URL (NEW)
- **description**: List description (NEW)

### FavoriteItems (NEW)
- **id**: Unique identifier
- **favoriteList_id**: Foreign key to favoriteLists
- **product_id**: Foreign key to products
- **addedAt**: Date added
- **notes**: User notes

## Order Management

### orders
- **id**: Unique identifier
- **recipientName**: Recipient name
- **recipientPhone**: Recipient phone
- **recipientAddress**: Delivery address
- **recipientPostalCode**: Postal code
- **sumAmount**: Order total
- **amountPayable**: Amount to pay
- **paymentStatus**: Payment status
- **user_id**: Foreign key to Users
- **orderNumber**: Human-readable order number (NEW)
- **orderDate**: Order creation date (NEW)
- **orderStatus**: Order status (NEW)
- **currency**: Currency code (NEW)
- **subtotal**: Items subtotal (NEW)
- **discountAmount**: Total discounts (NEW)
- **taxAmount**: Total taxes (NEW)
- **shippingAmount**: Shipping cost (NEW)
- **couponCode**: Applied coupon code (NEW)
- **notes**: Order notes (NEW)
- **giftMessage**: Gift message (NEW)
- **ipAddress**: Customer IP (NEW)
- **userAgent**: Browser info (NEW)
- **source**: Order source (web/app/marketplace) (NEW)

### OrderItems (NEW)
- **id**: Unique identifier
- **order_id**: Foreign key to orders
- **product_id**: Foreign key to products
- **seller_id**: Foreign key to sellers
- **sellerPrice_id**: Foreign key to sellersPrices
- **productOption_id**: Foreign key to productOptions
- **quantity**: Ordered quantity
- **price**: Price at order time
- **discount**: Discount amount
- **tax**: Tax amount
- **subtotal**: Item subtotal
- **status**: Item status
- **sku**: Product SKU

### OrderStatusHistory (NEW)
- **id**: Unique identifier
- **order_id**: Foreign key to orders
- **status**: Status value
- **comment**: Status comment
- **isCustomerNotified**: Notification status
- **createdBy**: User who changed status
- **createdAt**: Status change timestamp

### payments (NEW)
- **id**: Unique identifier
- **order_id**: Foreign key to orders
- **amount**: Payment amount
- **method**: Payment method
- **status**: Payment status
- **transactionId**: Payment gateway reference
- **currency**: Currency code
- **paymentDate**: Date of payment
- **gatewayResponse**: Gateway response data
- **billingAddress**: Billing address
- **last4**: Last 4 digits of card
- **cardType**: Card type if applicable

### shipments
- **id**: Unique identifier
- **status**: Shipment status
- **sendDate**: Ship date
- **deliveryDate**: Delivery date
- **sendMethod**: Shipping method
- **postalBarCode**: Tracking code
- **shipmentCost**: Shipping cost
- **sumAmount**: Shipment total
- **order_id**: Foreign key to orders
- **trackingUrl**: Tracking URL (NEW)
- **carrier**: Shipping carrier (NEW)
- **expectedDeliveryDate**: Estimated delivery (NEW)
- **actualDeliveryDate**: Actual delivery (NEW)
- **signedBy**: Signature information (NEW)
- **weight**: Package weight (NEW)
- **dimensions**: Package dimensions (NEW)
- **shippingNotes**: Special instructions (NEW)

### ShipmentItems (NEW)
- **id**: Unique identifier
- **shipment_id**: Foreign key to shipments
- **orderItem_id**: Foreign key to OrderItems
- **quantity**: Quantity shipped
- **tracking_number**: Individual tracking

### Returns (NEW)
- **id**: Unique identifier
- **order_id**: Foreign key to orders
- **user_id**: Foreign key to Users
- **requestDate**: Return request date
- **reason**: Return reason
- **status**: Return status
- **approvedBy**: Admin approver
- **resolutionType**: Refund/replacement
- **refundAmount**: Refund amount if applicable
- **notes**: Return notes
- **returnLabel**: Return shipping label

### ReturnItems (NEW)
- **id**: Unique identifier
- **return_id**: Foreign key to Returns
- **orderItem_id**: Foreign key to OrderItems
- **quantity**: Quantity returned
- **reason**: Item-specific return reason
- **condition**: Returned item condition
- **status**: Processing status

### Invoices (NEW)
- **id**: Unique identifier
- **order_id**: Foreign key to orders
- **invoiceNumber**: Invoice number
- **invoiceDate**: Invoice date
- **dueDate**: Payment due date
- **amount**: Invoice amount
- **status**: Invoice status
- **pdfPath**: Path to PDF invoice
- **notes**: Invoice notes

## Analytics & Additional Features

### SearchLogs (NEW)
- **id**: Unique identifier
- **query**: Search term
- **user_id**: Foreign key to Users (optional)
- **sessionId**: Browser session
- **timestamp**: Search time
- **resultsCount**: Number of results
- **categoryFilter**: Applied category filter
- **priceFilter**: Applied price filter
- **otherFilters**: Other filters (JSON)
- **resultClicked**: Whether a result was clicked
- **clickedProductId**: Clicked product if any

### ProductViews (NEW)
- **id**: Unique identifier
- **product_id**: Foreign key to products
- **user_id**: Foreign key to Users (optional)
- **sessionId**: Browser session
- **timestamp**: View time
- **duration**: View duration seconds
- **referrer**: Referring page/URL
- **device**: Device type
- **ip**: IP address
- **userAgent**: Browser info

### SalesStats (NEW)
- **id**: Unique identifier
- **date**: Statistics date
- **product_id**: Foreign key to products (optional)
- **category_id**: Foreign key to categories (optional)
- **brand_id**: Foreign key to brands (optional)
- **seller_id**: Foreign key to sellers (optional)
- **ordersCount**: Number of orders
- **itemsSold**: Number of items
- **revenue**: Total revenue
- **profit**: Total profit
- **averageOrderValue**: Average order amount
- **conversionRate**: Conversion percentage

### CustomerSegments (NEW)
- **id**: Unique identifier
- **name**: Segment name
- **description**: Segment description
- **criteria**: Segmentation rules (JSON)
- **createdAt**: Creation date
- **updatedAt**: Last update
- **memberCount**: Number of members

### CustomerSegmentMembers (NEW)
- **id**: Unique identifier
- **segment_id**: Foreign key to CustomerSegments
- **user_id**: Foreign key to Users
- **addedAt**: Date added to segment

### ContentPages (NEW)
- **id**: Unique identifier
- **title**: Page title
- **slug**: SEO-friendly URL
- **content**: Page content (HTML)
- **metaTitle**: SEO title
- **metaDescription**: SEO description
- **createdAt**: Creation date
- **updatedAt**: Last update
- **status**: Published/draft
- **author_id**: Content creator
- **pageType**: Type of page

### BlogPosts (NEW)
- **id**: Unique identifier
- **title**: Post title
- **slug**: SEO-friendly URL
- **summary**: Brief summary
- **content**: Post content
- **featuredImage**: Main image
- **metaTitle**: SEO title
- **metaDescription**: SEO description
- **author_id**: Foreign key to Users
- **publishDate**: Publication date
- **status**: Published/draft
- **viewCount**: Number of views
- **commentCount**: Number of comments
- **tags**: Post tags (comma-separated)

### BlogCategories (NEW)
- **id**: Unique identifier
- **name**: Category name
- **slug**: SEO-friendly URL
- **description**: Category description
- **parent_id**: Parent category if any

### BlogPostCategories (NEW)
- **id**: Unique identifier
- **post_id**: Foreign key to BlogPosts
- **category_id**: Foreign key to BlogCategories

### BlogComments (NEW)
- **id**: Unique identifier
- **post_id**: Foreign key to BlogPosts
- **user_id**: Foreign key to Users
- **content**: Comment text
- **createdAt**: Submission date
- **status**: Moderation status
- **parentComment_id**: Parent comment if reply

### SupportTickets (NEW)
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **subject**: Ticket subject
- **message**: Initial message
- **status**: Open/closed/pending
- **priority**: Priority level
- **department**: Handling department
- **createdAt**: Creation date
- **closedAt**: Closing date
- **order_id**: Related order if applicable
- **product_id**: Related product if applicable

### TicketResponses (NEW)
- **id**: Unique identifier
- **ticket_id**: Foreign key to SupportTickets
- **user_id**: Responder user ID
- **isStaff**: Whether from staff member
- **message**: Response text
- **createdAt**: Response time
- **attachments**: Attachment paths (JSON)

### TaxRules (NEW)
- **id**: Unique identifier
- **countryCode**: Country code
- **stateCode**: State/province code
- **zipCode**: ZIP/postal code range
- **taxRate**: Tax percentage
- **taxName**: Tax name
- **priority**: Application priority
- **productType**: Product type it applies to
- **isActive**: Active status

### Currencies (NEW)
- **id**: Unique identifier
- **code**: Currency code
- **name**: Currency name
- **symbol**: Currency symbol
- **exchangeRate**: Exchange rate to base
- **isDefault**: Default currency flag
- **isActive**: Active status
- **decimalPlaces**: Decimal places to show
- **symbolPosition**: Symbol position (before/after)

### Settings (NEW)
- **id**: Unique identifier
- **section**: Settings section
- **key**: Setting key
- **value**: Setting value
- **type**: Value type
- **isPublic**: Public visibility
- **description**: Setting description

### Translations (NEW)
- **id**: Unique identifier
- **languageCode**: Language code
- **translationKey**: Translation key
- **translationValue**: Translated text
- **section**: Website section 
