# Apptile Web Tunnel SDK Documentation

### Integration

To integrate the SDK into your application, include the following CDN link in your HTML file:

```html
<script src="https://unpkg.com/@apptile/apptile-web-tunnel@latest/dist/index.min.js"></script>
```

To integrate the SDK into your React/Node application, import our npm package.

---

### General Usage

All actions are invoked using the format below:

```javascript
window.Apptile.[Module].[FunctionName](data)
  .then((response) => {
    console.log(response);
  })
  .catch((error) => {
    console.error(error);
  });
```

---

### Modules

1. App Module
2. Data Module
3. Cart Module
4. Customer Module
5. Navigation Module
6. Wishlist Module

---

### App Module
Majorly used for toast, haptic feedbacks and other functions. But is really usefull and only way to fetch Current Page Parameters. 
Few pages have fixed parameters like PDP (Product details page), PLP (Products listing page or Collection products page).
- **PDP** : {productHandle: string}
- **PLP** : {collectionHandle: string}
You should try to leverage currentPage params if user asks for a product page widget or collection page widget.

**Functions:**

- **toast(data: ToastData)**
  - Description: Displays a toast message.
  - Parameters:
    - message: string
    - type: "success" | "error" | "info" | "warning"
    - position: "top" | "bottom"
    - duration?: number
  - Returns: void

- **triggerHaptic(data: HapticData)**
  - Description: Triggers haptic feedback.
  - Parameters:
    - type: "tap"
  - Returns: Promise<AppResponse>

- **trackAnalytics(data: TrackAnalyticsData)**
  - Description: Tracks app usage analytics.
  - Parameters:
    - event: string
    - properties: { [key: string]: any }
  - Returns: Promise<AppResponse>

- **shareText(data: ShareTextData)**
  - Description: Shares text content from the app.
  - Parameters:
    - text: string
  - Returns: Promise<AppResponse>

- **getDeviceAndApptileInfo()**
  - Description: Fetches Current Page Params, Device and Apptile version info.
  - Parameters: None
  - Returns: Promise<ApptileInfomation>

- **getApptileThemeDetails()**
  - Description: Retrieves Apptile theme details.
  - Parameters: None
  - Returns: Promise<AppResponse>

#### Interfaces

```typescript
interface ToastData {
  message: string;
  type: "success" | "error" | "info" | "warning";
  position: "top" | "bottom";
  duration?: number;
}

interface HapticData {
  type: "tap";
}

interface TrackAnalyticsData {
  event: string;
  properties: { [key: string]: any };
}

interface ShareTextData {
  text: string;
}

interface ApptileInfomation {
  deepLinking: [
    {
      screenName: string,
      linkingURL: string
    }
  ];
  devicePlatform: "android" | "ios";
  frameworkVersion: string;
  apptileAppVersion: number;
  pageParams: {
    [key: string]: any
  }
}

interface AppResponse {
  [key: string]: any;
}
```

---

### Data Module

**Functions:**

- **getLocalStorageItem(data: LocalStorageData)**
  - Description: Retrieves an item from local storage.
  - Parameters:
    - key: string // Mandatory
  - Returns: Promise<DataResponse>

- **setLocalStorageItem(data: SetLocalStorageData)**
  - Description: Sets an item in local storage.
  - Parameters:
    - key: string // Mandatory
    - value: string | number | boolean | object | null // Mandatory
  - Returns: Promise<DataResponse>

- **getShop(data: GetShopParams)**
  - Description: Retrieves shop details.
  - Parameters: None
  - Returns: Promise<ShopResponse>

- **getProductByHandle(data: GetProductByHandleParams)**
  - Description: Retrieves a product by its handle.
  - Parameters:
    - productHandle: string // Mandatory
  - Returns: Promise<ProductResponse>

- **getProductByIds(data: GetProductByIdsParams)**
  - Description: Retrieves products by their IDs.
  - Parameters:
    - productIds: string[] // Mandatory
  - Returns: Promise<ProductsResponse>

- **getProductRecommendations(data: GetProductRecommendationsParams)**
  - Description: Retrieves product recommendations.
  - Parameters:
    - productId: string // Mandatory
    - intent: "RELATED" | "COMPLEMENTARY"
  - Returns: Promise<ProductsResponse>

- **searchProducts(data: SearchProductsParams)**
  - Description: Searches for products.
  - Parameters:
    - query: string // Mandatory
    - sortKey: "BEST_SELLING" | "CREATED_AT" | "ID" | "PRICE" | "PRODUCT_TYPE" | "RELEVANCE" | "TITLE" | "UPDATED_AT" // Mandatory
    - reverse: boolean
    - first: number // Mandatory
    - after: number
  - Returns: Promise<ProductsResponse>

- **getCollectionProductsById(data: GetCollectionProductsByIdParams)**
  - Description: Retrieves products in a collection by ID.
  - Parameters:
    - id: string // Mandatory
    - sortKey: "BEST_SELLING" | "COLLECTION_DEFAULT" | "CREATED" | "ID" | "MANUAL" | "PRICE" | "RELEVANCE" | "TITLE" // Mandatory
    - reverse: boolean
    - first: number // Mandatory
    - after: string
    - filters: string
  - Returns: Promise<ProductsResponse>

- **getCollectionProductsByHandle(data: GetCollectionProductsByHandleParams)**
  - Description: Retrieves products in a collection by handle.
  - Parameters:
    - collectionHandle: string // Mandatory
    - sortKey: "BEST_SELLING" | "COLLECTION_DEFAULT" | "CREATED" | "ID" | "MANUAL" | "PRICE" | "RELEVANCE" | "TITLE" // Mandatory
    - reverse: boolean
    - first: number // Mandatory
    - after: string
    - filters: string
  - Returns: Promise<ProductsResponse>

- **getCollectionDetailsByHandle(data: GetCollectionDetailsByHandleParams)**
  - Description: Retrieves collection details by handle.
  - Parameters:
    - collectionHandle: string // Mandatory
  - Returns: Promise<CollectionResponse>

- **getCollections(data: GetCollectionsParams)**
  - Description: Retrieves collections.
  - Parameters:
    - first: number // Mandatory
    - after: string
    - reverse: boolean
    - sortKey: "ID" | "RELEVANCE" | "TITLE" | "UPDATED_AT" // Mandatory
  - Returns: Promise<CollectionsResponse>

- **getBlog(data: GetBlogParams)**
  - Description: Retrieves a blog by ID.
  - Parameters:
    - blogId: string
  - Returns: Promise<BlogResponse>

- **getBlogs(data: GetBlogsParams)**
  - Description: Retrieves a list of blogs.
  - Parameters:
    - first: number // Mandatory
    - after: string
    - query: string // Mandatory
    - reverse: boolean
    - sortKey: "HANDLE" | "ID" | "RELEVANCE" | "TITLE" // Mandatory
  - Returns: Promise<BlogsResponse>

- **getArticle(data: GetArticleParams)**
  - Description: Retrieves an article by blog and article handle.
  - Parameters:
    - blogHandle: string
    - articleHandle: string
  - Returns: Promise<ArticleResponse>

- **getArticles(data: GetArticlesParams)**
  - Description: Retrieves a list of articles.
  - Parameters:
    - query: string // Mandatory
    - first: number // Mandatory
    - after: string
    - sortKey: "AUTHOR" | "BLOG_TITLE" | "ID" | "PUBLISHED_AT" | "RELEVANCE" | "TITLE" | "UPDATED_AT" // Mandatory
    - reverse: boolean
  - Returns: Promise<ArticlesResponse>

- **getBlogByHandle(data: GetBlogByHandleParams)**
  - Description: Retrieves a blog by handle.
  - Parameters:
    - blogHandle: string
  - Returns: Promise<BlogResponse>

#### Interfaces

```typescript
// Data Module Interfaces
interface LocalStorageData {
  key: string;
}

interface SetLocalStorageData {
  key: string;
  value: string | number | boolean | object | null;
}

interface GetShopParams {}

interface GetProductByHandleParams {
    productHandle: string;
};

interface GetProductByIdsParams {
    productIds: string[];
};

interface GetProductRecommendationsParams {
    productId: string;
    intent: "RELATED" | "COMPLEMENTARY";
};

interface SearchProductsParams {
    query: string;
    sortKey: "BEST_SELLING" | "CREATED_AT" | "ID" | "PRICE" | "PRODUCT_TYPE" | "RELEVANCE" | "TITLE" | "UPDATED_AT" | "VENDOR";
    reverse: boolean;
    first: number;
    after: number;
};

interface GetCollectionProductsByIdParams {
    id: string;
    sortKey: "BEST_SELLING" | "COLLECTION_DEFAULT" | "CREATED" | "ID" | "MANUAL" | "PRICE" | "RELEVANCE" | "TITLE";
    reverse: boolean;
    first: number;
    after: string;
    filters: string;
};

interface GetCollectionProductsByHandleParams {
    collectionHandle: string;
    sortKey: "BEST_SELLING" | "COLLECTION_DEFAULT" | "CREATED" | "ID" | "MANUAL" | "PRICE" | "RELEVANCE" | "TITLE";
    reverse: boolean;
    first: number;
    after: string;
    filters: string;
};

interface GetCollectionDetailsByHandleParams {
    collectionHandle: string;
};

interface GetCollectionsParams {
    first: number;
    after: string;
    reverse: boolean;
    sortKey: "ID" | "RELEVANCE" | "TITLE" | "UPDATED_AT";
};

interface GetBlogParams {
    blogId: string;
};

interface GetBlogsParams {
    first: number;
    after: string;
    query: string;
    reverse: boolean;
    sortKey: "HANDLE" | "ID" | "RELEVANCE" | "TITLE";
};

interface GetArticleParams {
    blogHandle: string;
    articleHandle: string;
};

interface GetArticlesParams {
    query: string;
    first: number;
    after: string;
    sortKey: "AUTHOR" | "BLOG_TITLE" | "ID" | "PUBLISHED_AT" | "RELEVANCE" | "TITLE" | "UPDATED_AT";
    reverse: boolean;
};

interface GetBlogByHandleParams {
    blogHandle: string;
};

interface DataResponse {
  [key: string]: any;
}

// Product-related interfaces
interface ProductImage {
  id: string;
  src: string;
}

interface ProductVariant {
  id: string;
  title: string;
  barcode: string | null;
  availableForSale: boolean;
  sku: string | null;
  weight: number;
  weightUnit: string;
  quantityAvailableForSale: number;
  isInStock: boolean;
  featuredImage: string;
  price: number;
  salePrice: number;
  displayPrice: string;
  displaySalePrice: string;
  image: ProductImage;
}

interface Product {
  id: string;
  handle: string;
  title: string;
  description: string;
  productType: string;
  vendor: string;
  featuredImage: string;
  images: ProductImage[];
  variants: ProductVariant[];
  tags: string[];
  totalInventory: number;
  createdAt: string;
  updatedAt: string;
  publishedAt: string;
}

interface ProductResponse {
  data: Product;
}

interface ProductsResponse {
  data: Product[];
}

// Shop-related interfaces
interface ShopDomain {
  host: string;
  url: string;
}

interface ShopPaymentSettings {
  acceptedCardBrands: string[];
  cardVaultUrl: string;
  countryCode: string;
  currencyCode: string;
  enabledPresentmentCurrencies: string[];
  shopifyPaymentsAccountId: string | null;
  supportedDigitalWallets: string[];
}

interface ShopPolicy {
  title: string;
  url: string;
}

interface BrandColors {
  primary: string[];
  secondary: string[];
}

interface ShopBrand {
  coverImage: string | null;
  logo: string | null;
  shortDescription: string | null;
  slogan: string | null;
  squareLogo: string | null;
  colors: BrandColors;
}

interface Shop {
  id: string;
  name: string;
  description: string | null;
  moneyFormat: string;
  primaryDomain: ShopDomain;
  paymentSettings: ShopPaymentSettings;
  privacyPolicy: ShopPolicy | null;
  refundPolicy: ShopPolicy | null;
  shippingPolicy: ShopPolicy | null;
  subscriptionPolicy: ShopPolicy | null;
  termsOfService: ShopPolicy | null;
  brand: ShopBrand;
  shipsToCountries: string[];
}

interface ShopResponse {
  data: { 
    shop: Shop;
  }
}

// Query parameter interface
interface GetShopParams {
  // Empty interface as there are no required parameters for getShop
}

// Collection-related interfaces
interface CollectionSEO {
  title: string[];
  description: string[];
}

interface CollectionImage {
  id: string;
  url: string;
}

interface Collection {
  id: string;
  title: string;
  handle: string;
  description: string;
  descriptionHtml: string;
  featuredImage: string;
  onlineStoreUrl: string;
  seo: CollectionSEO;
  updatedAt: string;
  metafields: any[];
}

interface CollectionRawData {
  collectionByHandle: {
    id: string;
    title: string;
    handle: string;
    description: string;
    descriptionHtml: string;
    image: CollectionImage;
    onlineStoreUrl: string;
    seo: CollectionSEO;
    updatedAt: string;
    metafields: any[];
  }
}

interface Collection {
  id: string;
  title: string;
  handle: string;
  featuredImage: string;
  description: string;
  descriptionHtml: string;
  metafields: any[];
  _raw: CollectionRawData;
}

interface CollectionResponse {
    data: Collection;
}

interface CollectionsResponse {
    data: Collection[];
}

// Blog-related interfaces
interface Blog {
  id: string;
  title: string;
  handle: string;
  description: string | null;
  descriptionHtml: string | null;
  post_count: number;
}

interface BlogsResponse {
  data: Blog[];
}
interface BlogResponse {
  data: Blog;
}

// Article-related interfaces
interface ArticleImage {
  id: string;
  altText: string | null;
  src: string;
}

interface ArticleCategory {
  id: string;
  title: string;
  handle: string;
  description: string | null;
  descriptionHtml: string | null;
  post_count: number;
}

interface Article {
  id: string;
  title: string;
  handle: string;
  content: string;
  contentHtml: string;
  excerpt: string;
  excerptHtml: string;
  AuthorBio: string | null;
  AuthorName: string;
  modifiedAt: string | null;
  publishedAt: string;
  tags: string[];
  comments: any[];
  category: ArticleCategory;
  image: ArticleImage;
}

interface ArticlesResponse {
  data: Article[];
}

interface ArticleResponse {
  data: Article;
}

interface IData {
  getLocalStorageItem(data: LocalStorageData): Promise<DataResponse>;
  setLocalStorageItem(data: SetLocalStorageData): Promise<DataResponse>;
  getShop(data: GetShopParams): Promise<ShopResponse>;
  getProductByHandle(data: GetProductByHandleParams): Promise<ProductResponse>;
  getProductByIds(data: GetProductByIdsParams): Promise<ProductsResponse>;
  getProductRecommendations(data: GetProductRecommendationsParams): Promise<ProductsResponse>;
  searchProducts(data: SearchProductsParams): Promise<ProductsResponse>;
  getCollectionProductsById(data: GetCollectionProductsByIdParams): Promise<ProductsResponse>;
  getCollectionProductsByHandle(data: GetCollectionProductsByHandleParams): Promise<ProductsResponse>;
  getCollectionDetailsByHandle(data: GetCollectionDetailsByHandleParams): Promise<CollectionResponse>;
  getCollections(data: GetCollectionsParams): Promise<CollectionsResponse>;
  getBlogByHandle(data: GetBlogByHandleParams): Promise<BlogResponse>;
  getBlog(data: GetBlogParams): Promise<BlogResponse>;
  getBlogs(data: GetBlogsParams): Promise<BlogsResponse>;
  getArticle(data: GetArticleParams): Promise<ArticleResponse>;
  getArticles(data: GetArticlesParams): Promise<ArticlesResponse>;
}
```

---

### Cart Module

**Functions:**

- **addToCart(data)**
  - Description: Adds an item to the cart.
  - Parameters:
    - productId: string
    - variantId?: string
    - sellingPlanId?: string
    - quantity: number
  - Returns: Promise<CartResponse>

- **updateNote(data)**
  - Description: Updates the cart note.
  - Parameters:
    - note: string
  - Returns: void

- **updateAttributes(data)**
  - Description: Updates cart attributes.
  - Parameters:
    - attributes: { [key: string]: string }
  - Returns: void

- **removeFromCart(data)**
  - Description: Removes an item from the cart.
  - Parameters:
    - productId: string
    - variantId?: string
    - quantity: number
  - Returns: void

- **applyDiscount(data)**
  - Description: Applies a discount to the cart.
  - Parameters:
    - discountCode: string
  - Returns: Promise<CartResponse>

- **removeAllDiscounts()**
  - Description: Removes all discounts.
  - Parameters: None
  - Returns: void

- **getCartDetails()**
  - Description: Retrieves cart details.
  - Parameters: None
  - Returns: Promise<CartResponse>

#### Interfaces

```typescript
// Cart Module Interfaces
interface LineItem {
  productId: string;
  variantId?: string;
  sellingPlanId?: string;
  quantity: number;
}

interface CartResponse {
  message: string;
  data: Cart;
}

interface Cart {
  id: string;
  checkoutUrl: string;
  note: string;
  createdAt: string;
  updatedAt: string;
  ready: boolean | null;
  cartId: string;
  subtotalAmount: number;
  totalAmount: number;
  totalDutyAmount: number | null;
  totalTaxAmount: number | null;
  checkoutChargeAmount: number;
  displaySubtotalAmount: string;
  displayTotalAmount: string;
  displayTotalDutyAmount: string | null;
  displayTotalTaxAmount: string | null;
  displayCheckoutChargeAmount: string;
  buyerIdentity: BuyerIdentity;
  discountCodes: DiscountCode[];
  lines: CartLine[];
  checkoutLineItemData: CheckoutLineItem[];
  automaticCartDiscount: AutomaticCartDiscount;
}

interface BuyerIdentity {
  countryCode: string;
  customerId: string | null;
  email: string | null;
  phone: string | null;
  deliveryAddressPreferences: DeliveryAddressPreference[];
}

interface DeliveryAddressPreference {
  // Define fields if available, currently empty in the JSON
}

interface DiscountCode {
  // Define fields if available, currently empty in the JSON
}

interface CartLine {
  cartLineId: string;
  id: string;
  quantity: number;
  attributes: Attribute[];
  lineItemDiscount: number;
  displayLineItemDiscount: string | null;
  variant: Variant;
}

interface Attribute {
  // Define fields if available, currently empty in the JSON
}

interface Variant {
  product: Product;
  id: string;
  title: string;
  barcode: string | null;
  availableForSale: boolean;
  sku: string | null;
  weight: number;
  weightUnit: string;
  quantityAvailableForSale: number;
  isInStock: boolean;
  featuredImage: string;
  price: number;
  salePrice: number;
  displayPrice: string;
  displaySalePrice: string;
  metafields: Metafield[];
  image: Image;
  variantOptions: VariantOption[];
}

interface Product {
  title: string;
  handle: string;
  id: string;
  productType: string;
  tags: string[];
  totalInventory: number;
  vendor: string;
}

interface Metafield {
  // Define fields if available, currently empty in the JSON
}

interface Image {
  id: string;
  altText: string | null;
  src: string;
}

interface VariantOption {
  // Define fields if available, currently empty in the JSON
}

interface CheckoutLineItem {
  id: string;
  quantity: number;
  variantId: string;
}

interface AutomaticCartDiscount {
  totalDiscount: number;
  discountTitle: string;
  lineItemDiscount: LineItemDiscount[];
}

interface LineItemDiscount {
  title: string;
  amount: number;
  currencyCode: string;
}
```

---

### Customer Module

**Functions:**

- **getCurrentCustomer()**
  - Description: Retrieves the current customer.
  - Parameters: None
  - Returns: Promise<CustomerResponse>

- **getSession()**
  - Description: Retrieves session data.
  - Parameters: None
  - Returns: Promise<AccessTokenResponse>

- **setSession(data)**
  - Description: Sets session data.
  - Parameters:
    - customerAccessToken: string
    - customerSessionToken: string
  - Returns: Promise<CustomerResponse>

- **logout()**
  - Description: Logs out the customer.
  - Parameters: None
  - Returns: void

#### Interfaces

```typescript
// Customer Module Interfaces
interface SessionData {
  customerAccessToken: string;
  customerSessionToken: string;
  storefrontSessionToken: string;
}

interface LoggedInUser {
  id: string;
  firstName: string;
  lastName: string;
  acceptsMarketing: boolean;
  email: string;
  tags: string[];
  phone: string | null;
  defaultAddress: MailingAddress;
  addresses: MailingAddress[];
}

interface MailingAddress {
  id: string;
  firstName: string | null;
  lastName: string | null;
  address1: string;
  address2: string | null;
  city: string;
  company: string | null;
  country: string;
  latitude: number | null;
  longitude: number | null;
  phone: string | null;
  state: string;
  zip: string;
  formatted: string[];
}

interface AccessToken {
  accessToken: string;
  expiresAt: string;
}

interface CustomerResponse {
  message: string;
  data: LoggedInUser;
}

interface AccessTokenResponse {
  message: string;
  data: AccessToken;
}
```

---

### Navigation Module

**Functions:**

- **openProduct(data)**
  - Description: Opens a product page.
  - Parameters:
    - productHandle: string
  - Returns: void

- **openCollection(data)**
  - Description: Opens a collection page.
  - Parameters:
    - collectionHandle: string
  - Returns: void

- **openScreen(data)**
  - Description: Opens a screen in the app.
  - Parameters:
    - screenId: string
  - Returns: void

#### Interfaces

```typescript
// Navigation Module Interfaces
interface ProductData {
  productHandle: string;
}

interface CollectionData {
  collectionHandle: string;
}

interface ScreenData {
  screenId: string;
}
```

---

### Wishlist Module

**Functions:**

- **addToWishlist(data: WishlistItem)**
  - Description: Adds an item to the wishlist.
  - Parameters:
    - productId: string
    - productHandle: string
  - Returns: void

- **removeFromWishlist(data: WishlistItem)**
  - Description: Removes an item from the wishlist.
  - Parameters:
    - productId: string
    - productHandle: string
  - Returns: void

#### Interfaces

```typescript
// Wishlist Module Interfaces
interface WishlistItem {
  productId: string;
  productHandle: string;
}
```

---

### Code Examples

**Display a Toast Message**

```javascript
window.Apptile.app.toast({ message: "Welcome!", type: "info", position: "top" })
  .then(response => console.log(response))
  .catch(error => console.error(error));
```

**Add an Item to the Cart**

```javascript
window.Apptile.cart.addToCart({ productId: "12345", quantity: 1 })
  .then(response => console.log(response))
  .catch(error => console.error(error));
```

**Retrieve Current Customer**

```javascript
window.Apptile.customer.getCurrentCustomer()
  .then(response => console.log(response))
  .catch(error => console.error(error));
```

**Open a Product Page**

```javascript
window.Apptile.navigation.openProduct({ productHandle: "example-product" })
  .then(response => console.log(response))
  .catch(error => console.error(error));
```
