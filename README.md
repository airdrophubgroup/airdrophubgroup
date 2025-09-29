🚀 How to Run the Airdrop Mini‑App (Local & Cloud)

Below is a single, copy‑paste‑ready guide that will get your app running on macOS / Linux (and works on Windows with PowerShell).

It covers:

Local development – backend + frontend  
Running the full flow (World ID → claim)  
Optional: Deploy to the cloud (Vercel/Render/Netlify)  
1️⃣  Prerequisites
Item	Why it matters	How to install
Node.js ≥ 20	Needed for Vite, Express, ethers	brew install node (macOS)
sudo apt-get install -y nodejs npm (Ubuntu)
Git	Clone the repo	brew install git (macOS)
sudo apt-get install -y git (Ubuntu)
MetaMask	Connect wallet	Install from Chrome/Firefox or mobile
World ID SDK	Verify users	Included in the repo (auto‑loaded in the mini‑app)
2️⃣  Clone the Repository
git clone https://github.com/YourUser/airdrophubgroup.git
cd airdrophubgroup

You should now see two folders: frontend/ and backend/.

3️⃣  Set Up Environment Variables

Create a .env file in each folder (copy the example if it exists).

3.1  frontend/.env
VITE_WORLD_ID_PROJECT_ID=YOUR_WORLDID_PROJECT_ID
VITE_RPC_URL=https://goerli.infura.io/v3/YOUR_INFURA_KEY   # or mainnet URL
VITE_STAKING_ADDRESS=0xYourStakingContractAddress
VITE_CLAIM_ENDPOINT=http://localhost:3001/api/claim       # dev URL
3.2  backend/.env
MAINNET_RPC=https://goerli.infura.io/v3/YOUR_INFURA_KEY   # or mainnet URL
BACKEND_PRIVATE_KEY=0xYourBackendWalletPrivateKey
STAKING_ADDRESS=0xYourStakingContractAddress



Tip:  



For testing use Goerli (or Optimism Goerli).  
For production switch to Mainnet URLs and the mainnet contract address.


4️⃣  Install Dependencies
# Backend
cd backend
npm install


Frontend



cd ../frontend
npm install

5️⃣  Run the Application Locally
5.1  Start the Backend (Claim Service)

Open a terminal window, go to backend/, and run:

npm run dev   # or: node api/claim.js

You should see:

Claim service running on 3001
5.2  Start the Frontend (Mini‑App)

Open another terminal window, go to frontend/, and run:

npm run dev

You’ll see something like:

vite v5.0.0  ready in 1.2s
➜  Local:   http://localhost:5173/

Open that URL in your browser.

6️⃣  Quick Test Flow
Open MetaMask and switch to the network you set in .env (Goerli for testing).  
Open the mini‑app at http://localhost:5173.  
Click “Verify with World ID” – the World ID SDK will pop up; approve the request.  
After verification, click “Claim 10 AHG”.  
The backend will sponsor the gas and mint 10 AHG to your wallet.  
You’ll see a success message + transaction hash in the app.  
Verify the AHG balance on Goerli Explorer or in MetaMask.

If the claim succeeds, the app is working!

7️⃣  Deploy to the Cloud (Optional)
7.1  Backend (Vercel / Render / Netlify)
Create a new project and point it to the backend/ folder.  
Add the following environment variables in the platform’s secrets UI:

MAINNET_RPC
BACKEND_PRIVATE_KEY
STAKING_ADDRESS
Deploy.

The endpoint will be https://.vercel.app/api/claim.
7.2  Frontend (Vercel / Render / Netlify)
Create a new project and point it to the frontend/ folder.  
Add these environment variables:

VITE_WORLD_ID_PROJECT_ID
VITE_RPC_URL
VITE_STAKING_ADDRESS
VITE_CLAIM_ENDPOINT (point to the backend URL from 7.1)
Deploy.

The app will be live at https://.vercel.app.
8️⃣  What to Do Next
Next Step	Why	How
Switch to Mainnet	Users will claim on the real network	Update .env files with mainnet RPC and contract addresses, restart both servers
Add monitoring	Keep the gas‑sponsor wallet funded	Set up Etherscan alerts or a Discord webhook
Auto‑top‑up	No manual intervention	Run the topup.js script (or a small Docker container)
Publish a README	Helps others (or future you) understand the project	Document the deployment steps and environment variables
🎉 You’re All Set!

Run the commands above, test the flow, and you’ll have a fully functional airdrop mini‑app that’s ready to go live.  

If you run into any errors or need help with a specific step, just let me know!

Copy