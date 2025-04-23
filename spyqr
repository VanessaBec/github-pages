<!DOCTYPE html>
<html>
<head>
  <title>Transmisión de Cámara con Firebase</title>
  <!-- Importa Firebase -->
  <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-firestore-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.6.0/firebase-storage-compat.js"></script>
</head>
<body>
  <video id="localVideo" autoplay muted></video>
  <button onclick="startStream()">Iniciar Transmisión</button>

  <script>
    // Configura Firebase (reemplaza con tus datos)
    const firebaseConfig = {
      apiKey: "TU_API_KEY",
      authDomain: "TU_PROYECTO.firebaseapp.com",
      projectId: "TU_PROYECTO",
      storageBucket: "TU_PROYECTO.appspot.com",
      messagingSenderId: "TU_SENDER_ID",
      appId: "TU_APP_ID"
    };
    firebase.initializeApp(firebaseConfig);
    const db = firebase.firestore();

    let localStream;

    async function startStream() {
      try {
        localStream = await navigator.mediaDevices.getUserMedia({ video: true });
        document.getElementById("localVideo").srcObject = localStream;
        
        // Captura frames y súbelos a Firebase Storage cada 2 segundos (simulación)
        setInterval(() => {
          const canvas = document.createElement("canvas");
          canvas.width = 640;
          canvas.height = 480;
          const ctx = canvas.getContext("2d");
          ctx.drawImage(document.getElementById("localVideo"), 0, 0, canvas.width, canvas.height);
          
          // Convierte el frame a imagen y súbelo a Firebase
          canvas.toBlob((blob) => {
            const fileRef = firebase.storage().ref().child(`frames/${Date.now()}.jpg`);
            fileRef.put(blob).then(() => {
              console.log("Frame subido");
            });
          }, "image/jpeg", 0.7);
        }, 2000);
      } catch (error) {
        alert("Error: " + error.message);
      }
    }
  </script>
</body>
</html>
