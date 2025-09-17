# ZK Blind Guess Game

## Overview

ZK Blind Guess is an interactive game built with and powered by zero-knowledge proofs using the Noir language and Aztec's Barretenberg library. The game challenges players to navigate a path of tiles, where only the correct sequence (hidden on the server-side) allows success. Upon winning, a ZK proof is generated to verify that the player's path matches the secret path without revealing the secret itself. The proof is hashed, and both the proof and its hash can be copied and verified in-app.

This project demonstrates practical use of ZK proofs in gaming, ensuring privacy and verifiability. It uses Poseidon2 hashing for the public commitment and UltraHonk for proof generation.

The game is a static web app (HTML + JS), making it easy to host and run locally or online.

### Features
- **Navigate tiles** using mouse clicks.
- **ZK Proof Integration**: On success, generate a proof that your path matches the secret without exposing it.
- **Hashing & Verification**: Public hash of the secret path is shown upfront. Proof hash is computed (SHA-256) for easy sharing/verification.
- **Copy & Verify UI**: Buttons to copy public hash, proof, and proof hash. In-app verifier checks the proof hash.

### Tech Stack
- **Frontend/Graphics**: Three.js, OrbitControls, GSAP (for animations).
- **ZK Proofs**: Noir (circuit compilation & execution), Aztec's Barretenberg (Poseidon2 hashing, UltraHonk backend).
- **WASM Dependencies**: Noir WASM modules for circuit handling.
- **No External Servers**: Everything runs client-side in the browser.

## Setup & Installation

### Prerequisites
- A modern web browser (Chrome/Firefox recommended for WASM support).
- No additional installations needed; all dependencies are loaded via CDNs or imports.

### Running Locally
1. Clone the repository:
   ```
   git clone https://github.com/Atunde-SS/Zk-Blind-Guess.git
   ```
2. Navigate to the project directory:
   ```
   cd Zk-Blind-Guess
   ```
3. Open `index.html` in your browser (e.g., right-click and "Open with" or use a local server like `npx serve` for better handling of modules). or run `npm run dev` in your terminal

The game will load automatically. Click on tiles to play choose wisely!

### For Developers: Recreating the Project from Scratch
If you want to build this from scratch (e.g., for learning or customization):

1. Create a new directory:
   ```
   mkdir zk-blind-guess
   cd zk-blind-guess
   ```

2. Create `index.html` with the provided HTML content (see the code in this repo or the user's query for the exact markup).

3. Create `app.js` with the provided JavaScript code (again, from this repo or query).

4. Ensure the importmap in `index.html` points to Three.js CDNs correctly.

5. Test by opening `index.html` in a browser.

To customize:
- Adjust `numRows` and `numCols` in `app.js` for longer/shorter games.
- Modify the Noir circuit in `getCircuit()` for different logic.
- Add more visuals or levels using Three.js.

## How the ZK Proof Works
- **Secret Path**: Randomly generated array (e.g., [0, 1, 0] for left/right choices).
- **Public Hash**: Poseidon2 hash of the secret path, displayed upfront.
- **User Path**: Collected from player clicks.
- **Circuit**: Noir circuit asserts `user_path == secret_path` and `hash(secret_path) == public_hash`.
- **Proof Generation**: Execute circuit, generate UltraHonk proof.
- **Proof Hash**: SHA-256 digest of the proof for quick verification.
- **Verification**: In-app hash comparison (or use external tools for full ZK verify).

<img width="1867" height="795" alt="image" src="https://github.com/user-attachments/assets/cb8a0d18-be95-45ff-8496-fda914ffacf9" />
