# 🏆 ChiboyDatabase Registration System

A modern and secure user registration system built using **HTML, CSS, JavaScript**, and **Supabase** as the backend.  
It allows new users to register, automatically generates a unique identification ID (£ID), stores all registration details in Supabase, and provides instant verification links through Telegram, WhatsApp, or Facebook.

---

## 🚀 Features

- Beautiful and responsive registration form  
- 11-digit phone number validation  
- Stores all user details in **Supabase** (cloud database)  
- Generates a unique £ID for each user  
- Displays a congratulatory popup after successful registration  
- One-click copy for the £ID  
- Direct verification links:
  - **Telegram** → [https://t.me/chiboydatabase](https://t.me/chiboydatabase)
  - **WhatsApp** → Pre-filled message to `+2347064173933`
  - **Facebook** → Your Facebook user page  
- Automatic form reset on successful registration  

---

## 🧱 Technologies Used

| Layer | Technology |
|-------|-------------|
| Frontend | HTML5, CSS3, JavaScript |
| Backend | Supabase (PostgreSQL + API) |
| Hosting | Can be deployed via Vercel, Netlify, or any web server |
| Database Policies | Row Level Security with insert permission for `anon` |

---

## 🗃️ Database Setup (Supabase)

### 1️⃣ Create a Supabase Project
- Go to [https://supabase.com](https://supabase.com)
- Create a new project
- Copy your **Project URL** and **anon public key**

### 2️⃣ Create the Table
In your **Supabase SQL Editor**, paste and run:

```sql
create table public.chiboy_users (
  id bigint generated always as identity primary key,
  fullname text not null,
  email text not null unique,
  phone text not null,
  password text not null,
  registration_id text not null unique,
  status text default 'pending',
  created_at timestamp with time zone default now()
);

alter table public.chiboy_users enable row level security;

create policy "Allow insert for anonymous users"
on public.chiboy_users
for insert
to anon
with check (true);
