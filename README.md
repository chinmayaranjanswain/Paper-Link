
# 🖨️ ScanPrint - Automated Cloud Printing Kiosk

![Project Status](https://img.shields.io/badge/Status-In_Development-orange)
![License](https://img.shields.io/badge/License-MIT-blue)

ScanPrint is an automated, self-service cloud printing solution. It allows users to walk up to a printer, scan a QR code, upload their document via a mobile web app, pay online, and instantly receive their physical printout without any human intervention.

## 🚀 Features

* **QR Code Access:** Frictionless entry for users via a mobile-responsive web app.
* **Multi-Format Upload:** Supports PDF, DOCX, JPG, and PNG file uploads.
* **Dynamic Pricing Engine:** Automatically calculates cost based on page count and color preferences (B&W vs. Color).
* **Integrated Payments:** Secure checkout process for instant payment verification.
* **Automated Hardware Bridge:** A local compute node that continuously polls the cloud queue and triggers the physical printer automatically.
* **Privacy First:** Print jobs are automatically wiped from the database once the hardware bridge confirms a successful print.

## 🛠️ Tech Stack

This project is divided into a cloud-based web application and a local hardware bridge.

**Web Application (Cloud)**
* **Frontend:** React.js, Tailwind CSS (Mobile-first design)
* **Backend:** Node.js, Express.js
* **Database:** MongoDB (Queue management and transaction logs)
* **Storage:** AWS S3 / Cloudinary (Temporary file storage)
* **Payments:** Stripe / Razorpay API

**Hardware Bridge (Local)**
* **Environment:** Raspberry Pi (Raspberry Pi OS) / Linux Machine
* **Scripting:** Python
* **Print Server:** CUPS (Common UNIX Printing System)

## 🏗️ System Architecture

1. **Client Interface:** User scans QR -> Uploads File -> Pays via Payment Gateway.
2. **Cloud Server:** Webhook verifies payment -> File is moved to the `Ready_To_Print` MongoDB collection.
3. **Hardware Bridge:** A Python script on the local Raspberry Pi polls the database every 3 seconds.
4. **Execution:** The Pi downloads the file, sends it to the USB-connected printer via CUPS, and sends a "Success" callback to the server to delete the file.

## 💻 Installation & Setup

### Prerequisites
* Node.js and npm installed
* MongoDB instance running
* Python 3.x installed on the local hardware bridge
* A printer connected to the local machine configured with CUPS

### 1. Cloud Setup (Web App)
```bash
# Clone the repository
git clone [https://github.com/chinmayaranjanswain/scanprint.git](https://github.com/chinmayaranjanswain/scanprint.git)
cd scanprint

# Install dependencies for backend
cd backend
npm install

# Install dependencies for frontend
cd ../frontend
npm install

# Set up environment variables
# Create a .env file in the backend directory with your MongoDB URI, Payment API keys, etc.

# Run the development servers
# (Run in separate terminal windows)
cd backend && npm run dev
cd frontend && npm start
````

### 2\. Hardware Bridge Setup (Local Machine/Raspberry Pi)

```bash
# Navigate to the hardware bridge directory
cd hardware-bridge

# Install required Python packages
pip install requests pycups

# Configure your printer name in the script
# Run the polling script
python print_spooler.py
```

## 👨‍💻 Author

**Chinmaya**

  * GitHub: [@chinmayaranjanswain](https://www.google.com/search?q=https://github.com/chinmayaranjanswain)
  * Portfolio: [chinmaya.netlify.app](https://www.google.com/search?q=https://chinmaya.netlify.app)

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](https://www.google.com/search?q=LICENSE) file for details.

