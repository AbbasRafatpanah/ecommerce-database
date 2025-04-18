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
- **lastLoginDate**: Last successful login timestamp  
- **isActive**: Account active status  
- **referralCode**: Unique code for referral program  
- **loyaltyPoints**: Reward points balance  
- **preferredLanguage**: User's language preference  
- **marketingConsent**: Boolean for marketing communications  

### Roles
- **id**: Unique identifier for each role
- **name**: Role name (e.g., Customer, Admin, Moderator)
- **description**: Detailed role description  
- **isDefault**: Whether this is a default role for new users  

### Permissions
- **id**: Unique identifier
- **permissionName**: Name of permission
- **parent_id**: For hierarchical permissions
- **description**: Explains what the permission allows  
- **isActive**: Whether permission is active  

### Role_permission
- **id**: Unique identifier
- **role_id**: Foreign key to Roles
- **permission_id**: Foreign key to Permissions

### UserAuthentication  
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **twoFactorEnabled**: Whether 2FA is activated
- **twoFactorMethod**: Method (SMS, email, app)
- **backupCodes**: Encrypted recovery codes
- **lastPasswordChange**: Date of last password update

### UserSessions  
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **token**: Session token
- **ipAddress**: IP address
- **userAgent**: Browser/device info
- **startTime**: Session start
- **lastActivity**: Last activity time
- **isActive**: Whether session is active

### UserNotifications  
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **type**: Notification type
- **title**: Notification title
- **message**: Notification content
- **isRead**: Read status
- **createdAt**: Creation timestamp
- **relatedEntityType**: Related entity (order, product, etc.)
- **relatedEntityId**: ID of related entity

### UserActivity  
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **activityType**: Type of activity
- **description**: Activity description
- **ipAddress**: IP address
- **timestamp**: When activity occurred
- **metadata**: Additional data (JSON)

### SocialMediaConnections  
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
- **latitude**: Geographic coordinate  
- **longitude**: Geographic coordinate  
- **addressLabel**: Label for address (Home, Work, etc.)  
- **instructions**: Delivery instructions  

### address_users
- **id**: Unique identifier
- **address_id**: Foreign key to Addresses
- **user_id**: Foreign key to Users
- **isDefault**: Whether this is user's default address  

### cities
- **id**: Unique identifier
- **cityName**: Name of city
- **parent_id**: Parent region/state
- **countryCode**: ISO country code  
- **stateCode**: State/province code  
- **postcode**: Default postal code prefix  
- **timezone**: City timezone  

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
- **metaTitle**: SEO title  
- **metaDescription**: SEO description  
- **metaKeywords**: SEO keywords  
- **displayOrder**: Sorting order  
- **showInMenu**: Whether to show in navigation  
- **icon**: Icon identifier/class  

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
- **sku**: Stock keeping unit  
- **barcode**: Product barcode  
- **weight**: Product weight  
- **dimensions**: Product dimensions  
- **metaTitle**: SEO title  
- **metaDescription**: SEO description  
- **metaKeywords**: SEO keywords  
- **isDigital**: Whether product is digital  
- **hasVariants**: Whether product has variants  
- **minPurchaseQty**: Minimum order quantity  
- **maxPurchaseQty**: Maximum order quantity  
- **averageRating**: Calculated average rating  
- **reviewCount**: Number of reviews  
- **videoUrl**: Product demo video  

### category_products
- **id**: Unique identifier
- **category_id**: Foreign key to categories
- **product_id**: Foreign key to products
- **isPrimary**: Whether it's the primary category  
- **displayOrder**: Display order within category  

### brands
- **id**: Unique identifier
- **name**: Brand name
- **url**: SEO-friendly URL slug
- **imageName**: Brand logo
- **description**: Brand description
- **foundedYear**: Year founded  
- **countryOfOrigin**: Country of origin  
- **websiteUrl**: Brand website  
- **isOfficial**: Whether it's an official partner  
- **metaTitle**: SEO title  
- **metaDescription**: SEO description  

### images
- **id**: Unique identifier
- **imageName**: Image file name
- **type**: Image type
- **parent_id**: ID of parent entity
- **altText**: Alternative text  
- **title**: Image title  
- **displayOrder**: Display order  
- **size**: File size  
- **width**: Image width  
- **height**: Image height  

### productReviews
- **id**: Unique identifier
- **review**: Full review text
- **abstractReview**: Review summary
- **positivePoints**: Positive aspects
- **negativePoints**: Negative aspects
- **summary**: Review summary
- **product_id**: Foreign key to products
- **user_id**: Reviewer (Foreign key to Users)  
- **rating**: Numerical rating  
- **verified**: Whether reviewer purchased product  
- **helpfulCount**: Number of users finding review helpful  
- **reportCount**: Number of reports for inappropriate content  
- **createdAt**: Review date  
- **status**: Review status (pending/approved/rejected)  
- **adminResponse**: Response from seller/admin  

### property
- **id**: Unique identifier
- **title**: Property title
- **type**: Property type
- **helpText**: Explanatory text
- **value**: Property value
- **isKeyProp**: Whether it's a key property
- **product_id**: Foreign key to products
- **isFilterable**: Whether can be used in filters  
- **isComparable**: Whether can be used in comparisons  
- **displayOrder**: Display order  
- **unit**: Measurement unit  

### ProductTags  
- **id**: Unique identifier
- **name**: Tag name
- **slug**: SEO-friendly URL slug
- **description**: Tag description
- **createdAt**: Creation date

### ProductTagRelations  
- **id**: Unique identifier
- **product_id**: Foreign key to products
- **tag_id**: Foreign key to ProductTags

### RelatedProducts  
- **id**: Unique identifier
- **product_id**: Foreign key to products
- **related_product_id**: Foreign key to products
- **relationType**: Relation type (similar, accessory, upsell, etc.)
- **displayOrder**: Display order

### ProductBundles  
- **id**: Unique identifier
- **name**: Bundle name
- **description**: Bundle description
- **discount**: Discount percentage
- **startDate**: Availability start
- **endDate**: Availability end
- **isActive**: Active status

### ProductBundleItems  
- **id**: Unique identifier
- **bundle_id**: Foreign key to ProductBundles
- **product_id**: Foreign key to products
- **quantity**: Product quantity in bundle
- **price**: Optional custom price

### DigitalProductFiles  
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
- **description**: Detailed description  
- **durationMonths**: Duration in months  
- **coverageType**: What's covered  
- **provider**: Who provides the guarantee  
- **terms**: Terms and conditions  

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
- **storeDescription**: Business description  
- **storeLogo**: Logo image  
- **storeSlug**: SEO-friendly URL  
- **taxId**: Tax identification  
- **bankAccountInfo**: Payment details  
- **verificationStatus**: Account verification status  
- **commissionRate**: Platform commission percentage  
- **sellerLevel**: Seller level/tier  

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
- **costPrice**: Seller's cost  
- **isDefault**: Whether default offer for product  
- **leadTime**: Processing time before shipping  
- **availabilityStatus**: In stock, backorder, etc.  
- **minimumOrderQuantity**: Minimum order quantity  
- **restockDate**: Expected restock date if out of stock  

### productPrices
- **id**: Unique identifier
- **submitDate**: Submission date
- **price**: Regular price
- **discountPersent**: Discount percentage
- **discountPrice**: Discounted price
- **isAvailable**: Availability status
- **sellerPrice_id**: Foreign key to sellersPrices
- **productOptions_id**: Foreign key to productOptions
- **specialOfferText**: Promotional text  
- **startDate**: Promotional price start date  
- **endDate**: Promotional price end date  
- **isDefaultPrice**: Whether this is default price  

### productOptions
- **id**: Unique identifier
- **type**: Option type
- **name**: Option name
- **value**: Option value
- **displayOrder**: Display order  
- **priceModifier**: Price adjustment amount  
- **priceModifierType**: Fixed or percentage  
- **sku**: SKU extension for this option  
- **image**: Option image (like color swatch)  

### InventoryHistory  
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

### TierPricing  
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
- **rating**: Star rating  
- **commentDate**: Date posted  
- **helpfulCount**: Number of helpful votes  
- **reportCount**: Number of inappropriate reports  
- **purchaseVerified**: Whether from verified purchaser  
- **adminResponse**: Response from seller/admin  

### questions
- **id**: Unique identifier
- **question**: Question text
- **createDate**: Creation date
- **answerCount**: Number of answers
- **isConfirmed**: Moderation status
- **user_id**: Foreign key to Users
- **product_id**: Foreign key to products
- **status**: Question status  
- **isHelpful**: Whether marked as helpful  
- **helpfulCount**: Number of helpful votes  
- **viewCount**: Number of views  

### answers
- **id**: Unique identifier
- **answer**: Answer text
- **like**: Number of likes
- **createDate**: Creation date
- **isConfirmed**: Moderation status
- **user_id**: Foreign key to Users
- **question_id**: Foreign key to questions
- **isBestAnswer**: Whether marked as best answer  
- **isFromSeller**: Whether from product seller  
- **isFromAdmin**: Whether from admin  
- **helpfulCount**: Number of helpful votes  
- **unhelpfulCount**: Number of unhelpful votes  

### comment_user_like
- **id**: Unique identifier
- **isLiked**: Like status
- **comment_id**: Foreign key to comments
- **user_id**: Foreign key to Users
- **timestamp**: When like was given  

### answer_user_like
- **id**: Unique identifier
- **isLiked**: Like status
- **answer_id**: Foreign key to answers
- **user_id**: Foreign key to Users
- **timestamp**: When like was given  

### ProductSubscriptions  
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **product_id**: Foreign key to products
- **notificationType**: Type of notification
- **createdAt**: Subscription date
- **isActive**: Active status

### UserWishlists  
- **id**: Unique identifier
- **name**: Wishlist name
- **description**: Wishlist description
- **isPublic**: Privacy status
- **createdAt**: Creation date
- **user_id**: Foreign key to Users

### WishlistItems  
- **id**: Unique identifier
- **wishlist_id**: Foreign key to UserWishlists
- **product_id**: Foreign key to products
- **addedAt**: Date added
- **notes**: User notes
- **priority**: User priority level

### ProductComparisons  
- **id**: Unique identifier
- **sessionId**: Browser session ID
- **user_id**: Foreign key to Users (optional)
- **createdAt**: Creation time
- **updatedAt**: Last update time

### ComparisonItems  
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
- **description**: Promotion details  
- **discountType**: Percentage or fixed amount  
- **discountValue**: Discount amount/percentage  
- **couponCode**: Optional coupon code  
- **usageLimit**: Maximum usage count  
- **usageCount**: Current usage count  
- **minimumOrderAmount**: Order threshold  
- **isActive**: Active status  
- **applyToShipping**: Whether applies to shipping  

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
- **listingPriority**: Display priority  
- **promotionalText**: Marketing message  
- **soldCount**: Number of units sold  

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
- **code**: Actual coupon code  
- **discountType**: Percentage or fixed  
- **description**: Coupon description  
- **isActive**: Active status  
- **usageLimit**: Total usage limit  
- **perUserLimit**: Usage limit per user  
- **usedCount**: Times already used  
- **categories**: Applicable categories  

### banners
- **id**: Unique identifier
- **type**: Banner type
- **title**: Banner title
- **imageName**: Banner image
- **url**: Click destination
- **isActive**: Active status
- **startDate**: Start date  
- **endDate**: End date  
- **position**: Display position  
- **displayOrder**: Display order  
- **impressions**: View count  
- **clicks**: Click count  
- **targetDevice**: Desktop/mobile/all  
- **description**: Banner description  

### LoyaltyProgram  
- **id**: Unique identifier
- **name**: Program name
- **description**: Program description
- **pointsPerCurrency**: Points earned per currency unit
- **minimumRedeemPoints**: Minimum points for redemption
- **conversionRate**: Points to currency conversion
- **expiryMonths**: Months until points expire
- **isActive**: Program active status

### LoyaltyHistory  
- **id**: Unique identifier
- **user_id**: Foreign key to Users
- **points**: Points earned/redeemed
- **type**: Earn or redeem
- **description**: Transaction description
- **orderId**: Related order if applicable
- **createdAt**: Transaction date
- **expiryDate**: When points expire
- **balance**: Current balance after transaction

### GiftCards  
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

### ReferralProgram  
- **id**: Unique identifier
- **name**: Program name
- **description**: Program description
- **referrerReward**: Reward for referrer
- **referredReward**: Reward for new customer
- **minimumOrderAmount**: Order threshold for reward
- **isActive**: Program active status
- **termsAndConditions**: Program terms

### Referrals  
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

### EmailCampaigns  
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

### AbandonedCartRecovery  
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
- **createdAt**: Creation date  
- **status**: Active/abandoned/converted  
- **couponCode**: Applied coupon  
- **ip**: User IP address  
- **userAgent**: Browser info  
- **currency**: Currency code  
- **subtotal**: Items subtotal  
- **discountAmount**: Total discounts  
- **taxAmount**: Total taxes  
- **shippingAmount**: Shipping cost  
- **grandTotal**: Final amount  

### cartDetails
- **id**: Unique identifier
- **count**: Item quantity
- **price**: Price at addition time
- **cart_id**: Foreign key to carts
- **sellersPrice_id**: Foreign key to sellersPrices
- **addedAt**: Date added to cart  
- **productOption_id**: Foreign key to productOptions  
- **isGift**: Whether item is a gift  
- **giftMessage**: Gift message  
- **customizationData**: Custom options JSON  

### favoriteLists
- **id**: Unique identifier
- **coockie**: Session cookie
- **updateDate**: Last update
- **user_id**: Foreign key to Users
- **name**: List name  
- **isPublic**: Privacy setting  
- **shareUrl**: Shareable URL  
- **description**: List description  

### FavoriteItems  
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
- **orderNumber**: Human-readable order number  
- **orderDate**: Order creation date  
- **orderStatus**: Order status  
- **currency**: Currency code  
- **subtotal**: Items subtotal  
- **discountAmount**: Total discounts  
- **taxAmount**: Total taxes  
- **shippingAmount**: Shipping cost  
- **couponCode**: Applied coupon code  
- **notes**: Order notes  
- **giftMessage**: Gift message  
- **ipAddress**: Customer IP  
- **userAgent**: Browser info  
- **source**: Order source (web/app/marketplace)  

### OrderItems  
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

### OrderStatusHistory  
- **id**: Unique identifier
- **order_id**: Foreign key to orders
- **status**: Status value
- **comment**: Status comment
- **isCustomerNotified**: Notification status
- **createdBy**: User who changed status
- **createdAt**: Status change timestamp

### payments  
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
- **trackingUrl**: Tracking URL  
- **carrier**: Shipping carrier  
- **expectedDeliveryDate**: Estimated delivery  
- **actualDeliveryDate**: Actual delivery  
- **signedBy**: Signature information  
- **weight**: Package weight  
- **dimensions**: Package dimensions  
- **shippingNotes**: Special instructions  

### ShipmentItems  
- **id**: Unique identifier
- **shipment_id**: Foreign key to shipments
- **orderItem_id**: Foreign key to OrderItems
- **quantity**: Quantity shipped
- **tracking_number**: Individual tracking

### Returns  
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

### ReturnItems  
- **id**: Unique identifier
- **return_id**: Foreign key to Returns
- **orderItem_id**: Foreign key to OrderItems
- **quantity**: Quantity returned
- **reason**: Item-specific return reason
- **condition**: Returned item condition
- **status**: Processing status

### Invoices  
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

### SearchLogs  
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

### ProductViews  
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

### SalesStats  
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

### CustomerSegments  
- **id**: Unique identifier
- **name**: Segment name
- **description**: Segment description
- **criteria**: Segmentation rules (JSON)
- **createdAt**: Creation date
- **updatedAt**: Last update
- **memberCount**: Number of members

### CustomerSegmentMembers  
- **id**: Unique identifier
- **segment_id**: Foreign key to CustomerSegments
- **user_id**: Foreign key to Users
- **addedAt**: Date added to segment

### ContentPages  
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

### BlogPosts  
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

### BlogCategories  
- **id**: Unique identifier
- **name**: Category name
- **slug**: SEO-friendly URL
- **description**: Category description
- **parent_id**: Parent category if any

### BlogPostCategories  
- **id**: Unique identifier
- **post_id**: Foreign key to BlogPosts
- **category_id**: Foreign key to BlogCategories

### BlogComments  
- **id**: Unique identifier
- **post_id**: Foreign key to BlogPosts
- **user_id**: Foreign key to Users
- **content**: Comment text
- **createdAt**: Submission date
- **status**: Moderation status
- **parentComment_id**: Parent comment if reply

### SupportTickets  
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

### TicketResponses  
- **id**: Unique identifier
- **ticket_id**: Foreign key to SupportTickets
- **user_id**: Responder user ID
- **isStaff**: Whether from staff member
- **message**: Response text
- **createdAt**: Response time
- **attachments**: Attachment paths (JSON)

### TaxRules  
- **id**: Unique identifier
- **countryCode**: Country code
- **stateCode**: State/province code
- **zipCode**: ZIP/postal code range
- **taxRate**: Tax percentage
- **taxName**: Tax name
- **priority**: Application priority
- **productType**: Product type it applies to
- **isActive**: Active status

### Currencies  
- **id**: Unique identifier
- **code**: Currency code
- **name**: Currency name
- **symbol**: Currency symbol
- **exchangeRate**: Exchange rate to base
- **isDefault**: Default currency flag
- **isActive**: Active status
- **decimalPlaces**: Decimal places to show
- **symbolPosition**: Symbol position (before/after)

### Settings  
- **id**: Unique identifier
- **section**: Settings section
- **key**: Setting key
- **value**: Setting value
- **type**: Value type
- **isPublic**: Public visibility
- **description**: Setting description

### Translations  
- **id**: Unique identifier
- **languageCode**: Language code
- **translationKey**: Translation key
- **translationValue**: Translated text
- **section**: Website section 
