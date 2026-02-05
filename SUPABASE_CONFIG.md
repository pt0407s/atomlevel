# Supabase Configuration for Custom Username/Password Auth

## Important: Disable Email Confirmation

Since we're using synthetic emails (username@stoichmaster.local), you need to disable email confirmation:

### Step 1: Disable Email Confirmation
1. Go to your Supabase dashboard: [app.supabase.com](https://app.supabase.com)
2. Select your project
3. Go to **Authentication** → **Providers** → **Email**
4. Toggle **"Confirm email"** to **OFF**
5. Click **Save**

### Step 2: Disable Google OAuth (Optional)
1. Go to **Authentication** → **Providers** → **Google**
2. Toggle to **OFF**
3. Click **Save**

### Step 3: Configure Site URL
1. Go to **Authentication** → **URL Configuration**
2. Set **Site URL** to your deployed URL:
   ```
   https://your-app.vercel.app
   ```
3. Add **Redirect URLs**:
   ```
   https://your-app.vercel.app
   https://your-app.vercel.app/**
   http://localhost:8000
   http://localhost:8000/**
   ```

## Username & Password Rules

### Username Validation:
- ✅ Min 5 characters
- ✅ Max 18 characters
- ✅ No spaces
- ✅ Only letters, numbers, `_`, `.`, `-`

### Password Validation:
- ✅ Min 8 characters
- ✅ Max 18 characters
- ✅ No spaces
- ✅ Only letters, numbers, `_`, `.`, `-`, `@`, `$`, `%`

## How It Works

1. User creates account with username and password
2. System validates username and password format
3. System checks if username is already taken
4. System creates synthetic email: `username@stoichmaster.local`
5. Supabase stores user with synthetic email
6. User signs in with username (converted to synthetic email)
7. Username is stored in user metadata and database

## Testing

1. Start local server: `python3 -m http.server 8000`
2. Open: `http://localhost:8000`
3. Click **"Sign In"**
4. Click **"Sign In with Username"**
5. Click **"Sign Up"** tab
6. Create account with:
   - Username: `test_user` (5-18 chars)
   - Password: `test@123` (8-18 chars)
7. Sign in with same credentials

## Troubleshooting

**"Email confirmation required"**
- Make sure you disabled email confirmation in Supabase

**"Username already taken"**
- Try a different username

**Validation errors**
- Check that username/password meet the requirements above

**"Invalid username or password"**
- Make sure you're using the exact username and password you signed up with
