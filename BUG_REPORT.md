# Bug #1: 419 CSRF Token Mismatch

# Category: Backend Config Issue
# File: bootstrap/app.php

# Summary:
Login/register was failing with 419 CSRF error because statefulApi Sanctum session-based auth was enabled, but the app uses React with bearer token-based authentication.

# Fix:
Removed statefulApi() from bootstrap/app.php since CSRF/session middleware is not needed for Bearer token auth.



