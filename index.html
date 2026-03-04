<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Облачное приложение + DM</title>
<style>
body { font-family: 'Inter', sans-serif; background: #f4f7f6; display: flex; flex-direction: column; align-items: center; padding: 20px; }
.container { width: 100%; max-width: 500px; background: white; padding: 25px; border-radius: 12px; box-shadow:0 4px 15px rgba(0,0,0,0.05); margin-bottom: 20px; }
.auth-bar { background: white; padding: 15px; border-radius: 12px; margin-bottom: 0px; display: flex; align-items: center; gap: 15px; box-shadow: 0 2px 10px rgba(0,0,0,0.05); }
.user-avatar { width: 40px; height: 40px; border-radius: 50%; border: 2px solid #007bff; }
input { width: 100%; padding: 12px; margin: 8px 0; border: 1px solid #ddd; border-radius: 6px; box-sizing: border-box; }
button { background: #007bff; color: white; border: none; padding: 12px; border-radius: 5px; width: 100%; font-weight: 600; cursor: pointer; transition: 0.3s; }
button:hover { background: #0056b3; }
button:disabled { background: #ccc; }
.logout-btn { background: #ff4757; padding: 8px 15px; width: auto; font-size: 14px; }
.post { background: #fff; border: 1px solid #eaeaea; padding: 15px; margin-top: 15px; border-radius: 8px; width: 100%; position: relative;}
.post-header { display: flex; align-items: center; gap: 10px; margin-bottom: 10px; }
.post-avatar { width: 30px; height: 30px; border-radius: 50%; }
.like-btn { cursor: pointer; border: none; background: #f8f9fa; padding: 5px 12px; border-radius: 20px; margin-top: 10px; }
.delete-btn { cursor: pointer; border: none; background: #ff4757; color: white; padding: 5px 10px; border-radius: 5px; font-size: 12px; position: absolute; top: 10px; right: 10px; z-index: 10; }
.time { font-size: 11px; color: #999; margin-left: auto; }
.post img { max-width:100%; margin-top:10px; border-radius:8px; }

/* Чат */
#chatContainer { display: none; flex-direction: column; width: 100%; max-width: 500px; margin-bottom: 20px; }
#chatBox { border: 1px solid #ccc; padding: 10px; height: 300px; overflow-y: auto; margin-bottom: 10px; background: #f9f9f9; border-radius:8px; }
.my { text-align: right; color: blue; margin: 5px 0; }
.other { text-align: left; color: black; margin: 5px 0; }
</style>
</head>
<body>

<!-- Авторизация -->
<div id="authSection" class="container" style="text-align:center;">
  <button id="loginBtn">Войти через Google</button>
  <div id="userInfo" style="display: none;" class="auth-bar">
    <img id="userPhoto" class="user-avatar" src="" alt="Avatar">
    <span id="userName" style="font-weight: bold;"></span>
    <button id="logoutBtn" class="logout-btn">Выйти</button>
  </div>
</div>

<!-- Форма создания поста -->
<div id="messageForm" class="container" style="display: none;">
  <h3>Создать запись</h3>
  <input type="text" id="name" placeholder="Имя профиля" readonly>
  <input type="email" id="email" placeholder="Ваш Email" readonly>
  <input type="text" id="content" placeholder="Что у вас нового?">
  <input type="file" id="imageInput" accept="image/*">
  <button id="postBtn">Опубликовать в облако</button>
</div>

<!-- Лента постов -->
<div id="feed" style="width: 100%; max-width: 500px;"></div>

<!-- Чат -->
<div id="chatContainer" class="container">
  <h3>Чат с пользователем</h3>
  <div id="chatBox"></div>
  <input id="messageInput" placeholder="Сообщение">
  <button id="sendBtn">Отправить</button>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-app.js";
import { getFirestore, collection, addDoc, doc, onSnapshot, serverTimestamp, updateDoc, increment, query, orderBy, getDoc, setDoc } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-firestore.js";
import { getAuth, signInWithPopup, GoogleAuthProvider, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-auth.js";
import { getStorage, ref, uploadBytes, getDownloadURL, deleteObject } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-storage.js";

// 🔥 Вставь сюда свой Firebase Config
const firebaseConfig = {
  apiKey: "ВАШ_API_KEY",
  authDomain: "ВАШ_PROJECT.firebaseapp.com",
  projectId: "ВАШ_PROJECT_ID",
  storageBucket: "ВАШ_PROJECT.appspot.com",
  messagingSenderId: "ВАШ_SENDER_ID",
  appId: "ВАШ_APP_ID"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
const auth = getAuth(app);
const provider = new GoogleAuthProvider();
const storage = getStorage(app);

// Элементы
const loginBtn = document.getElementById('loginBtn');
const logoutBtn = document.getElementById('logoutBtn');
const userInfo = document.getElementById('userInfo');
const messageForm = document.getElementById('messageForm');
const userNameElem = document.getElementById('userName');
const userPhotoElem = document.getElementById('userPhoto');
const nameInput = document.getElementById('name');
const emailInput = document.getElementById('email');
const contentInput = document.getElementById('content');
const postBtn = document.getElementById('postBtn');
const feed = document.getElementById('feed');

const chatContainer = document.getElementById('chatContainer');
const chatBox = document.getElementById('chatBox');
const messageInput = document.getElementById('messageInput');
const sendBtn = document.getElementById('sendBtn');

let currentChatId = null;

// Авторизация
loginBtn.onclick = () => signInWithPopup(auth, provider);
logoutBtn.onclick = () => signOut(auth);

onAuthStateChanged(auth, async (user) => {
  if(user){
    loginBtn.style.display = "none";
    userInfo.style.display = "flex";
    messageForm.style.display = "block";

    userNameElem.textContent = user.displayName;
    userPhotoElem.src = user.photoURL || 'https://via.placeholder.com/40';
    nameInput.value = user.displayName;
    emailInput.value = user.email;

    // Сохраняем пользователя
    await setDoc(doc(db, "users", user.uid), {
      uid: user.uid,
      name: user.displayName,
      email: user.email,
      photoURL: user.photoURL,
      createdAt: serverTimestamp()
    }, { merge:true });

    loadPosts();

  } else {
    loginBtn.style.display = "inline-block";
    userInfo.style.display = "none";
    messageForm.style.display = "none";
  }
});

// Публикация поста с изображением
postBtn.onclick = async () => {
  const content = contentInput.value.trim();
  const file = document.getElementById('imageInput').files[0];

  if(!content && !file) return alert("Введите текст или выберите картинку!");

  let imageUrl = "";

  try {
    if(file){
      const storageRef = ref(storage, `posts/${auth.currentUser.uid}_${Date.now()}_${file.name}`);
      await uploadBytes(storageRef, file);
      imageUrl = await getDownloadURL(storageRef);
    }

    await addDoc(collection(db, "requests"), {
      uid: auth.currentUser.uid,
      name: auth.currentUser.displayName,
      email: auth.currentUser.email,
      photo: auth.currentUser.photoURL || '',
      text: content,
      image: imageUrl,
      likes: 0,
      timestamp: serverTimestamp()
    });

    contentInput.value = "";
    document.getElementById('imageInput').value = "";

  } catch(e){
    alert("Ошибка при публикации! Проверьте правила Firebase.");
    console.error(e);
  }
};

// Лента постов
function loadPosts(){
  const q = query(collection(db, "requests"), orderBy("timestamp", "desc"));
  onSnapshot(q, (snapshot) => {
    feed.innerHTML = "";
    snapshot.forEach(docItem => {
      const data = docItem.data();
      const postDiv = document.createElement("div");
      postDiv.className = "post";
      postDiv.innerHTML = `
        <div class="post-header">
          <img src="${data.photo || 'https://via.placeholder.com/30'}" class="post-avatar">
          <b>${data.name}</b>
          <span class="time">${data.timestamp ? data.timestamp.toDate().toLocaleTimeString() : ''}</span>
        </div>
        <p>${data.text || ''}</p>
        ${data.image ? `<img src="${data.image}">` : ''}
        <button class="like-btn" onclick="processLike('${docItem.id}')">👍 ${data.likes || 0}</button>
        ${auth.currentUser && auth.currentUser.uid === data.uid ? `<button class="delete-btn" onclick="deletePost('${docItem.id}','${data.image}')">Удалить</button>` : ''}
        <button onclick="openChat('${data.uid}','${data.name}')" style="margin-top:5px;">💬 Написать</button>
      `;
      feed.appendChild(postDiv);
    });
  });
}

// Лайк
window.processLike = async (id) => {
  await updateDoc(doc(db, "requests", id), { likes: increment(1) });
};

// Удаление
window.deletePost = async (id, imageUrl) => {
  if(!confirm("Удалить этот пост?")) return;
  try {
    await deleteDoc(doc(db, "requests", id));
    if(imageUrl){
      const imgRef = ref(storage, imageUrl);
      await deleteObject(imgRef);
    }
  } catch(e){ console.error(e); }
};

// ===== Личные сообщения =====
window.openChat = async (receiverUid, receiverName) => {
  const user = auth.currentUser;
  if(receiverUid === user.uid) return alert("Нельзя писать себе");

  const chatId = [user.uid, receiverUid].sort().join("_");
  currentChatId = chatId;

  const chatRef = doc(db, "chats", chatId);
  const chatSnap = await getDoc(chatRef);
  if(!chatSnap.exists()){
    await setDoc(chatRef, { participants: [user.uid, receiverUid], updatedAt: serverTimestamp() });
  }

  chatContainer.style.display = "flex";
  chatBox.innerHTML = `<b>Чат с ${receiverName}</b><br>`;
  loadMessages(chatId);
};

function loadMessages(chatId){
  const q = query(collection(db, "chats", chatId, "messages"), orderBy("timestamp", "asc"));
  onSnapshot(q, snapshot => {
    chatBox.innerHTML = `<b>Чат:</b><br>`;
    snapshot.forEach(doc => {
      const data = doc.data();
      const p = document.createElement("p");
      p.className = data.senderId === auth.currentUser.uid ? "my" : "other";
      p.textContent = data.text;
      chatBox.appendChild(p);
    });
    chatBox.scrollTop = chatBox.scrollHeight;
  });
}

// Отправка сообщения
sendBtn.onclick = async () => {
  const text = messageInput.value.trim();
  if(!text || !currentChatId) return;

  await addDoc(collection(db, "chats", currentChatId, "messages"), {
    text,
    senderId: auth.currentUser.uid,
    timestamp: serverTimestamp()
  });

  await updateDoc(doc(db, "chats", currentChatId), { updatedAt: serverTimestamp() });
  messageInput.value = "";
};
</script>
</body>
</html>
