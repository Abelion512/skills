# Supabase Security Best Practices

## 1. Row Level Security (RLS)
- **Always Enable:** Every table must have RLS enabled.
- **Policies:** Define precise SELECT, INSERT, UPDATE, DELETE policies.
- **Check `public`:** Never use `public` role for sensitive data. Use `authenticated` or specific roles.
- **Service Role:** Use only in Edge Functions/Server side, never on client.

## 2. Authentication
- **Email/Password:** Require email confirmation.
- **Social Auth:** Configure correctly with production keys.
- **Sessions:** Use secure, HTTP-only cookies if possible (SSR).

## 3. Database Functions
- **Security Definer:** Be extremely careful. Runs with owner privileges.
- **Search Path:** Always set `search_path` to prevent hijacking.

## 4. API & Network
- **Rate Limiting:** Enable Supabase Rate Limiting.
- **Custom Domains:** Use custom domain for cleaner cookies/CORS.
