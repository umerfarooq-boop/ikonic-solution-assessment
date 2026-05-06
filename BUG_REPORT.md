# Bug #1: 419 CSRF Token Mismatch

# Category: Backend Config Issue
# File: bootstrap/app.php

# Summary:
Login/register was failing with 419 CSRF error because statefulApi Sanctum session-based auth was enabled, but the app uses React with bearer token-based authentication.

# Fix:
Removed statefulApi() from bootstrap/app.php since CSRF/session middleware is not needed for Bearer token auth.


# Bug #2: 422 Error Not Shown on Login

# Category: Frontend Error Handling
# Files: AuthContext.js, Login.js (frontend)

# Summary:
Login was crashing on 422 (invalid credentials) because errors were not handled properly. The API error was not caught in AuthContext, and the Login page was not displaying any error message to the user.

# Fix:
Added proper try/catch in both AuthContext login() and Login.js so the error is handled and shown in the UI instead of crashing the app.


# Bug #3: Cart Resets on Refresh

# Category: Frontend State Issue
# File: CartContext.js
# Summary:
Cart items disappeared after refresh because state was only stored in memory and not reloaded from API.
# Fix:
Added useEffect to call fetchCart() on app load when token exists, so cart data is restored after refresh.


# Bug #5: Cart Not Updating After Login

# Category: Frontend State Issue
# File: Cart.js

# Summary:
Cart was not updating after login because fetchCart() only ran once on mount and did not react to user changes.
# Fix:
Updated useEffect dependency from [] to [user] so cart reloads when user logs in.


# Bug #5: Cart Not Updating After Login

# Category: Frontend State Issue
# File: Cart.js

# Summary:
Cart was not updating after login because fetchCart() only ran once on mount and did not react to user changes.
# Fix:
Updated useEffect dependency from [] to [user] so cart reloads when user logs in.

# Bug #6: Product Stock Not Reduced
# Category: Backend
# File: Checkout Controller

# Summary:
Stock was not decreasing after checkout, allowing unlimited purchases.

# Fix:
# Decremented product stock during order creation.

# Bug #7: No Stock Validation
# Category: Backend
# Summary:
Users could order more items than available stock.
# Fix:
Added stock validation before checkout.

# Bug #8: Missing Payment Authorization
# Category: Backend Security

# Summary:
Users could process payment for others' orders.

# Fix:
Restricted order access to the authenticated user only.

# UI Issue when add product show alert box user not cancel it if cancel refresh the page

# add confirm box here add also here try catch for better error



# Bug #9: Missing Database Transaction in Checkout
# Category: Backend / Database

# Summary:
Checkout operations were not wrapped in a transaction, causing partial/inconsistent data if any step failed.

# Fix:
Wrapped all checkout DB operations inside DB::transaction() to ensure rollback on failure.




# Critical Issue #10 

# not add try catch failuer not erorr handling here

