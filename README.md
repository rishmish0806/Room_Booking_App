# Room Booking App

A meeting room booking app I built using Next.js 14, Appwrite, and Tailwind CSS. Users can browse rooms, check availability, and make reservations. There's also a heatmap on each room's page that shows how busy it is across the next two weeks — which ended up being my favorite part to build.

🔗 Live: [bookit-app-alpha.vercel.app](https://bookit-app-alpha.vercel.app)

---

## What it does

- Sign up / log in with secure session handling via Appwrite
- Browse available meeting rooms with capacity and amenity info
- Book a room by picking a date and time slot — duplicate bookings are prevented
- View and cancel your own bookings from a personal dashboard
- See a 14-day availability heatmap on each room's detail page (green = free, yellow = filling up, red = fully booked)
- Toast notifications for all actions so you always know what happened
- Works on mobile too

---

## The heatmap

This was the most interesting feature to build. Instead of making users click through slots one by one to find a free time, the heatmap shows the next 14 days at a glance — each cell is a time slot, colored by how booked it is.

It's all powered by the existing bookings collection — no new database tables. On the server side, bookings for a room are fetched in one query, grouped by date and time slot, and then the occupancy percentage is computed per slot. The grid itself is just Tailwind CSS classes — no charting library. Since it's a Next.js Server Component, the aggregation runs on the server and nothing extra ships to the client.

---

## Tech used

- **Next.js 14** (App Router)
- **Appwrite** for auth, database, and storage
- **Tailwind CSS** for styling
- **Luxon** for date/time handling
- **React Toastify** for notifications
- **React Icons**
- Deployed on **Vercel**

---

## Folder structure

```
bookit-app/
├── app/                        # Pages and layouts (App Router)
│   └── rooms/[id]/             # Room detail page + heatmap
├── components/
│   ├── RoomCard.jsx
│   ├── BookingForm.jsx
│   └── AvailabilityHeatmap.jsx
├── config/                     # Appwrite setup
├── context/                    # Auth state via React Context
├── middleware.js               # Protects routes that need login
└── ...config files
```

---

## Running it locally

You'll need Node 18+ and an Appwrite Cloud account.

```bash
git clone https://github.com/your-username/bookit-app.git
cd bookit-app
npm install
```

Rename `.env.example` to `.env.local` and add your Appwrite credentials:

```env
NEXT_PUBLIC_APPWRITE_ENDPOINT=https://cloud.appwrite.io/v1
NEXT_PUBLIC_APPWRITE_PROJECT=your_project_id
NEXT_APPWRITE_KEY=your_api_key
NEXT_PUBLIC_APPWRITE_DATABASE=your_database_id
NEXT_PUBLIC_APPWRITE_COLLECTION_ROOMS=your_rooms_collection_id
NEXT_PUBLIC_APPWRITE_COLLECTION_BOOKINGS=your_bookings_collection_id
NEXT_PUBLIC_APPWRITE_STORAGE_BUCKET=your_storage_bucket_id
```

Then:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

---

## Screenshot

![BookIt App](./public/images/screen.png)

---

## License

MIT
