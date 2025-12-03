Hawk-Eye: Volleyball Evaluation App

Hawk-Eye is a mobile-friendly React application designed to streamline the evaluation process at volleyball tryouts. Coaches can quickly score players on key skills, manage rosters via CSV import, and view real-time leaderboards to make data-driven decisions.

🚀 Features

Player Evaluation Interface: * Score players on a 0-10 scale for 7 specific skills: Hitting, Passing, Defense, Setting, Serving, Voice/Presence, and Potential.

Real-time "Total Score" calculation.

Roster Management:

Add players manually or Bulk Import via CSV.

Filter players by Grade or Position during evaluation for focused tryout sessions.

Data Persistence: * All data is saved automatically to the browser's Local Storage, preventing data loss during refreshes.

Analytics & Reports:

Results Tab: Sortable list of all evaluated players.

Reports Tab: Generate specific ranked lists (Overall, By Grade, By Position).

CSV Export: Download full data or specific reports for offline use.

🛠️ Tech Stack

React: Frontend framework.

Tailwind CSS: Styling and responsive design.

Lucide React: Iconography.

Vite: Build tool (Recommended).

📦 Installation & Setup

Clone the repository

git clone [https://github.com/yourusername/hawk-eye.git](https://github.com/yourusername/hawk-eye.git)
cd hawk-eye


Install dependencies

npm install


Run the development server

npm run dev


Build for production

npm run build


📋 Usage Guide

1. Importing Players (CSV)

To bulk upload a roster, create a .csv file with the following columns (no header row required, but order matters):

First Name

Last Name

Jersey Number

Grade (7-12)

Position (Outside, Middle, Right Side, Setter, Libero/DS)

Example CSV content:

Jane,Doe,10,9,Setter
Sarah,Smith,12,11,Libero/DS


2. Evaluating

Navigate to the Eval tab.

Use the Filter By options to select a specific Grade or Position group (e.g., "Grade 9" or "Setters").

Select a player from the dropdown.

Adjust sliders for each skill.

Click Save Evaluation.

3. Exporting Results

Go to the Results or Reports tab.

Click Export to download the current view as a .csv file compatible with Excel or Google Sheets.

☁️ Deployment

This app is "static" and can be easily deployed to Netlify, Vercel, or GitHub Pages.

For Netlify:

Drag and drop your dist folder (created after running npm run build) into Netlify's manual deploy page.

Or connect your GitHub repository to Netlify and set the build command to npm run build and publish directory to dist.

📄 License

This project is licensed under the MIT License.
