# Thrifty backend setup (free)

Thrifty now saves accounts and data in a free Supabase project, so your login and numbers work on any device.
You need two files: `thrifty-cloud.html` (the app) and `supabase-schema.sql` (the database setup).

## 1. Create the free project
1. Go to supabase.com and sign up (the Free plan costs $0).
2. Create a new project. Choose a name, a database password (save it somewhere), and the region closest to your users.
3. Wait until the project finishes setting up.

## 2. Create the database table
1. In your project, open the **SQL Editor**.
2. Paste the whole contents of `supabase-schema.sql` and press **Run**.
3. This creates the `user_data` table, turns on Row Level Security so each person only sees their own data, and adds the "delete my account" function.

## 3. Connect the app
1. In **Project Settings**, open the **API** page.
2. Copy the **Project URL** and the **anon (public) key**. The anon key is meant to be public. Row Level Security protects the data. Never use the `service_role` key in this file.
3. Open `thrifty-cloud.html` in a text editor. Near the top of the script, replace the two lines:
   - `PASTE_YOUR_SUPABASE_URL_HERE` with your Project URL
   - `PASTE_YOUR_SUPABASE_ANON_KEY_HERE` with your anon key

## 4. Email settings
- By default Supabase asks new users to confirm their email. The app handles this: after sign-up it says to check the email, then the user logs in.
- To skip confirmation while testing, turn off email confirmation in the project's **Authentication** settings.
- The free plan's built-in email sender is rate limited. For real users, connect your own email provider later.

## 5. Put it online
The page needs a web address so confirmation and reset-password emails can link back to it.
1. Upload `thrifty-cloud.html` to a free static host such as GitHub Pages, Cloudflare Pages or Netlify. Name it `index.html` if the host expects that.
2. In **Authentication**, open the **URL Configuration** page and set the Site URL (and add it to the redirect URLs) to your page's address.

## 6. Try it
Create an account, add an expense, press Save, then log in from another browser or phone. Your data should be there.

## Good to know
- Free Supabase projects pause after a week with no activity. Open the project in the dashboard to wake it up.
- Data is stored as one JSON document per person. That is simple and fast to build on. If you later want reports across all users, move to separate tables for expenses, budgets and liabilities.
- Passwords are handled by Supabase Auth. Thrifty never stores them.
- The advice on the Home tab is still rule-based. A real AI model would be a separate step and needs a server function to keep its key secret.
  
