# own-telegram-cloud-storgae-web
This is a frontend website where you can add your credentials than you can use telegram as a unlimited cloud storage and all upload file directly transferred  to you teligram bot.

# 🗃️ Telnik - Telegram Bot File Manager (Firebase-Backed)

Telnik is a simple and stylish file manager web interface that stores your file metadata in a **Firebase Realtime Database** and uses your **Telegram Bot** to manage the actual files (such as upload and download).

This single HTML file acts as a complete front-end application, requiring no backend server as it interacts directly with the Firebase and Telegram APIs.

---

## 🚀 Key Features

* **Telegram Bot Integration:** Uploads files directly to Telegram via the `sendDocument` API and facilitates downloads using the `getFile` API.
* **Firebase Realtime Database:** Stores all file metadata (name, size, category, Telegram `file_id`) in real-time.
* **Visual File Management:** Includes features for creating folders, uploading files, editing file details, and batch deleting or moving items.
* **Intuitive UI:** A modern, dark-themed, and responsive design built using Tailwind CSS and the Poppins font.
* **Folder Navigation:** Easy navigation between the root and sub-folders, complete with breadcrumbs for organizing files.

---

## 🛠️ Setup & Configuration

To run this project, you need a **Telegram Bot** and a **Firebase Project**.

### 1. Firebase Setup

1.  **Create a Firebase Project:** Go to the [Firebase console](https://console.firebase.google.com/) and create a new project.
2.  **Add a Web App:** Add a web app to your project and copy the provided `firebaseConfig`.
3.  **Enable Realtime Database:** Navigate to "Realtime Database" and create a database. For testing, you may set the Security Rules to ignore `$uid` authentication (or implement proper rules for production):
    ```json
    {
      "rules": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
    ```
4.  **Update Configuration in HTML:** Fill in your Firebase configuration inside the `<script type="module">` tag of the HTML file:

    ```javascript
    // NOTE: Replace with your actual Firebase configuration
    const firebaseConfig = {
        apiKey: "YOUR_API_KEY",
        authDomain: "YOUR_AUTH_DOMAIN",
        databaseURL: "YOUR_DATABASE_URL",
        projectId: "YOUR_PROJECT_ID",
        storageBucket: "YOUR_STORAGE_BUCKET",
        messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
        appId: "YOUR_APP_ID",
        measurementId: "YOUR_MEASUREMENT_ID"
    };
    // ...
    ```

### 2. Telegram Bot Setup

1.  **Create a Bot:** Use [@BotFather](https://t.me/BotFather) on Telegram to create a new bot and obtain your **BOT\_TOKEN**.
2.  **Get the Chat ID:** Obtain the **CHAT\_ID** of the chat (private chat or channel/group) where you want to store files.
    * **Private Chat:** Use a bot like `@getidsbot`.
    * **Channel/Group:** Make the bot an **Admin** in the channel/group, send a message in it, and then check the URL `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates` to find the chat ID (it will be a negative number, e.g., `-1001234567890`).
3.  **Update Configuration in HTML:** Fill in your Telegram credentials inside the main `<script>` tag of the HTML file:

    ```javascript
    const BOT_TOKEN = 'YOUR_BOT_TOKEN'; // fill here
    const CHAT_ID = 'YOUR_CHAT_ID';     // fill here (e.g., -1234567890)
    const TELEGRAM_API_URL = `https://api.telegram.org/bot${BOT_TOKEN}`;
    // ...
    ```

---

## 👨‍💻 Usage

1.  Save the HTML file with all the configurations mentioned above.
2.  Open the file directly in your browser (`file:///path/to/your/file.html`) or upload it to a static hosting service (like Firebase Hosting, Netlify, Vercel).
3.  Wait for the **connection status** to turn green ("✅ Firebase & Telegram Bot connected").
4.  You can now start using the File Manager:
    * **New Folder:** Create new folders to organize your files.
    * **Upload File:** Select and upload files to your Telegram chat and Firebase.
    * **Navigation:** Navigate between folders using the sidebar and breadcrumbs.
    * **Batch Actions:** Select multiple files and folders to **Delete** or **Move** them simultaneously.

---

## ⚠️ Important Notes

* **File Size Limit:** Files uploaded via the Telegram Bot API's `sendDocument` method are typically limited to around **50 MB**.
* **Security:** In this setup, if you do not implement proper authentication, the Firebase Realtime Database rules could allow public access. Ensure you use **Firebase Authentication** and enforce rules to only allow authorized users to read/write data.
* **Delete Operation:** When a folder is deleted, all files within that folder (and its sub-folders) are **moved** to the **'Others'** default folder. The files are **NOT** deleted from Telegram; only the file metadata is updated in Firebase.
* **Move Operation:** Moving a folder will also **rename the category paths** of all files and sub-folders inside it to match the new destination path.

---

## 📦 Dependencies

This project uses only CDN (Content Delivery Network) links and requires no Node.js or package manager to run.

* **Tailwind CSS:** Utility-first CSS framework.
* **Iconify:** For functional and stylish icons.
* **Google Firebase JS SDK:** For Realtime Database interaction.
