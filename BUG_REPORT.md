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



