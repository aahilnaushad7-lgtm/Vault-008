<!DOCTYPE html>
<html>
<head>
<title>THE TWAN FILES</title>
<style>
body {
    margin:0;
    background:black;
    color:#00ff88;
    font-family: "Courier New", monospace;
    overflow:hidden;
}

/* Full-page glitch overlay */
body::before {
    content:"";
    position:absolute;
    top:0; left:0;
    width:100%; height:100%;
    background: repeating-linear-gradient(
        0deg,
        rgba(0,255,136,0.05),
        rgba(0,255,136,0.05) 2px,
        transparent 2px,
        transparent 4px
    );
    animation: flicker 0.2s infinite;
    pointer-events:none;
}

@keyframes flicker {
    0% { opacity: 0.9; }
    50% { opacity: 1; }
    100% { opacity: 0.9; }
}

.center {
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%, -50%);
    text-align:center;
}

input {
    background:black;
    border:1px solid #00ff88;
    color:#00ff88;
    padding:8px;
    text-align:center;
}

button {
    background:black;
    border:1px solid #00ff88;
    color:#00ff88;
    padding:6px 15px;
    cursor:pointer;
    margin-top:10px;
}

.hidden { display:none; }

.terminal {
    padding:30px;
    height:100vh;
    overflow-y:auto;
}

.file {
    cursor:pointer;
    margin:10px 0;
}

.file:hover {
    color:white;
}
</style>
</head>

<body>

<!-- LOGIN PAGE -->
<div id="login" class="center">
    <h1>▓▓▓ THE TWAN FILES ▓▓▓</h1>
    <p>ACCESS GATEWAY INITIALIZED</p>
    <p>Enter Passphrase:</p>
    <input type="password" id="passwordInput">
    <br>
    <button onclick="checkPassword()">ENTER</button>
    <p id="error"></p>
</div>

<!-- FILE LIST PAGE -->
<div id="fileList" class="terminal hidden">
    <h2>> TWAN DIRECTORY</h2>
    <div id="filesContainer"></div>
</div>

<!-- FILE VIEW PAGE -->
<div id="fileView" class="terminal hidden">
    <pre id="fileContent"></pre>
</div>

<script>
const files = [
    {
        name: "THE CONSTITUTIONAL VALUE OF TWAN",
        content: `• Loyalty above all.\n• Secrecy is survival.\n• Unity ensures power.\n`
    },
    {
        name: "PUNISHMENTS..",
        content: `1. Neural Override — System disruption at first warning.\n2. Blackout Isolation — Forced log-off and signal block.\n3. Memory Fragmentation — Data access revoked temporarily.\n4. Flash Override — Sudden interface glitches.\n5. Contact Revocation — All network comms disabled.\n6. Permanent Removal — User flagged from main directory.\n7. Internal Lockdown — Restricted access to all files.\n8. Obsidian Wrath — Account trace initiated.\n9. Identity Deletion — Digital footprint erased.\n10. Digital Exile — Complete ban from TWAN network.\n`
    },
    {
        name: "THE MEMBERS",
        content: `1. Shannon — Slave Dynasty\n2. Aahil — Ming Dynasty\n3. Ahmed — King of Slaves\n4. Amr — L-CET\n5. Kris — THE GUY..\n6. Zayan — CHARGER\n7. Aadhinath — STICKMAN\n8. Mike — THE ENDGAME\n`
    }
];

function checkPassword() {
    const password = document.getElementById("passwordInput").value;
    if(password === "region") {
        document.getElementById("login").classList.add("hidden");
        showFileList();
    } else {
        document.getElementById("error").innerText = "ACCESS DENIED — TRACE INITIATED.";
    }
}

function showFileList() {
    const container = document.getElementById("filesContainer");
    container.innerHTML = "";
    files.forEach((file,index)=>{
        const div = document.createElement("div");
        div.className = "file";
        div.innerText = "📁 " + file.name;
        div.onclick = () => openFile(index);
        container.appendChild(div);
    });
    document.getElementById("fileList").classList.remove("hidden");
}

function typeWriter(text, element, callback) {
    let i=0;
    function typing() {
        if(i<text.length){
            element.innerHTML += text.charAt(i);
            i++;
            setTimeout(typing,25);
        } else {
            if(callback) callback();
        }
    }
    typing();
}

function openFile(index) {
    const file = files[index];
    const fileView = document.getElementById("fileView");
    const fileContent = document.getElementById("fileContent");
    document.getElementById("fileList").classList.add("hidden");
    fileView.classList.remove("hidden");
    fileContent.innerHTML = `> Opening file: ${file.name}\n---------------------------------\n\n`;
    typeWriter(file.content, fileContent, () => {
        setTimeout(()=> {
            fileView.classList.add("hidden");
            showFileList();
        },10000); // Auto return after 10 seconds
    });
}
</script>

</body>
</html>
