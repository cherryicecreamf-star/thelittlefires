# thelittlefires
<!doctype html>
<html lang="uk">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Тохи вогню — Шкільний Банк</title>
  <style>
    :root{--orange:#ff7a00;--orange-dark:#e66000;--bg:#fff8f0;--card:#fff;--muted:#666;}
    body{margin:0;background:linear-gradient(180deg,var(--bg),#fff);color:#222;font-family:Inter,system-ui,Arial;}
    header{display:flex;align-items:center;gap:16px;padding:18px 24px;border-bottom:4px solid rgba(255,122,0,0.12);background:linear-gradient(90deg,rgba(255,122,0,0.08),transparent)}
    header img{width:56px;height:56px;border-radius:10px;object-fit:cover}
    header h1{margin:0;font-size:20px;color:var(--orange-dark)}
    .container{max-width:980px;margin:28px auto;padding:0 20px}
    .grid{display:grid;grid-template-columns:1fr 360px;gap:20px}
    .card{background:var(--card);padding:18px;border-radius:12px;box-shadow:0 6px 18px rgba(20,20,30,0.04)}
    .big{padding:24px}
    label{display:block;margin:10px 0 6px 0;font-size:13px;color:var(--muted)}
    input,select,button,textarea{width:100%;padding:10px;border-radius:8px;border:1px solid #eee;font-size:14px}
    .btn{background:var(--orange);color:#fff;border:none;padding:10px 12px;border-radius:8px;cursor:pointer}
    .btn.secondary{background:transparent;color:var(--orange-dark);border:1px solid rgba(230,100,0,0.12)}
    .muted{color:var(--muted);font-size:13px}
    .balance{font-size:36px;font-weight:700;color:var(--orange-dark)}
    .small{font-size:13px}
    footer{margin-top:18px;text-align:center;color:var(--muted);font-size:13px}
    hr{border:none;border-top:1px solid #f2d9c9;margin:12px 0}
    @media(max-width:880px){.grid{grid-template-columns:1fr}}
  </style>
</head>
<body>
  <header>
    <img src="logo.png" alt="Логотип">
    <div>
      <h1>Тохи вогню — Шкільний Банк</h1>
      <div class="muted">Валюта: <strong>вогники</strong></div>
    </div>
  </header>

  <main class="container">
    <div class="grid">
      <section class="card big">
        <h2>Доступ</h2>

        <div style="display:flex;gap:8px;margin-bottom:12px">
          <button class="btn" id="tab-login">Увійти</button>
          <button class="btn secondary" id="tab-register">Реєстрація (учень)</button>
          <button class="btn secondary" id="tab-teacher-register">Реєстрація (вчитель)</button>
          <button class="btn secondary" id="tab-admin">Адмін</button>
        </div>

        <div id="area">
          <!-- Login -->
          <div id="login-area">
            <label>Email</label>
            <input id="login-email" placeholder="email@example.com">
            <label>Пароль</label>
            <input id="login-pass" type="password" placeholder="Пароль">
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn" id="btn-login">Увійти</button>
              <button class="btn secondary" id="btn-logout" style="display:none">Вийти</button>
            </div>
            <div id="login-msg" class="muted" style="margin-top:8px"></div>
          </div>

          <!-- Student register -->
          <div id="register-area" style="display:none">
            <h3 class="small">Реєстрація — учень</h3>
            <label>Ім'я</label>
            <input id="stu-name" placeholder="Ім'я">
            <label>Email</label>
            <input id="stu-email" placeholder="email@student.com">
            <label>Пароль</label>
            <input id="stu-pass" type="password" placeholder="Пароль">
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn" id="btn-register-stu">Зареєструватися</button>
            </div>
            <div id="reg-stu-msg" class="muted" style="margin-top:8px"></div>
          </div>

          <!-- Teacher register -->
          <div id="teacher-register-area" style="display:none">
            <h3 class="small">Реєстрація — вчитель</h3>
            <label>Ім'я</label>
            <input id="tech-name" placeholder="Ім'я (наприклад: Марія)">
            <label>Email</label>
            <input id="tech-email" placeholder="teacher@school.com">
            <label>Пароль</label>
            <input id="tech-pass" type="password" placeholder="Пароль">
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn" id="btn-register-teacher">Зареєструвати вчителя</button>
            </div>
            <div id="reg-tech-msg" class="muted" style="margin-top:8px"></div>
          </div>

          <!-- Student panel -->
          <div id="student-panel" style="display:none;margin-top:12px">
            <h3 class="small">Ваш гаманець</h3>
            <div>Привіт, <span id="me-name"></span></div>
            <div style="margin-top:12px" class="card">
              <div style="display:flex;justify-content:space-between;align-items:center">
                <div>
                  <div class="small">Баланс (вогники)</div>
                  <div id="me-balance" class="balance">0</div>
                </div>
                <div>
                  <button class="btn secondary" id="btn-refresh-balance">Оновити</button>
                </div>
              </div>
            </div>
            <div id="student-msg" class="muted" style="margin-top:8px"></div>
          </div>

          <!-- Admin panel -->
          <div id="admin-panel" style="display:none;margin-top:12px">
            <h3 class="small">Адмін-панель</h3>

            <label>Щомісячна сума для кожного учня (вогники)</label>
            <input id="monthly-amount" type="number" value="10">
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn" id="btn-distribute-monthly">Distribute monthly</button>
            </div>
            <div id="distribute-msg" class="muted" style="margin-top:8px"></div>

            <hr>

            <h4 class="small">Керування людьми</h4>
            <label>Додати учня (email)</label>
            <input id="admin-new-stu-email" placeholder="student@school.com">
            <label>Ім'я учня</label>
            <input id="admin-new-stu-name" placeholder="Ім'я">
            <label>Початковий баланс</label>
            <input id="admin-new-stu-balance" type="number" value="0">
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn" id="admin-create-student">Створити учня (DB)</button>
            </div>
            <div style="height:6px"></div>

            <label>Видалити користувача за UID</label>
            <input id="admin-remove-uid" placeholder="uid...">
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn" id="admin-remove-user">Видалити (DB)</button>
            </div>
            <div id="admin-msg" class="muted" style="margin-top:8px"></div>
          </div>

        </div>
      </section>

      <aside class="card">
        <h3>Інформація</h3>
        <div class="muted">Тепер реєстрація для адміна відключена: адміністратора додають вручну в Firebase Console → Authentication → Add user; потім у Realtime Database → /users/{adminUid} = { role: 'admin' }</div>
        <hr>
        <div class="muted small">Порада: після тестування обов'язково налаштуйте правила безпеки для Realtime Database, щоб лише авторизовані з ролями могли писати.</div>
      </aside>
    </div>

    <footer class="muted">Сайт для школи «Тохи вогню» — Банк вогників</footer>
  </main>

  <!-- Firebase compat -->
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script>

  <script>
    // ========= ВСТАВТЕ ТУТ СВІЙ firebaseConfig =========
    // const firebaseConfig = { apiKey: "...", authDomain: "...", databaseURL: "https://<PROJECT>-default-rtdb.firebaseio.com", projectId: "...", storageBucket: "...", messagingSenderId: "...", appId: "..." };
    // ===================================================
    // !!! Замість нижче - вставити свій блок
    const firebaseConfig = {
      /* вставити свій блок тут */
    };
    // Initialize
    firebase.initializeApp(firebaseConfig);
    const auth = firebase.auth();
    const db = firebase.database();

    // UI refs
    const tabLogin = document.getElementById('tab-login');
    const tabRegister = document.getElementById('tab-register');
    const tabTeacherReg = document.getElementById('tab-teacher-register');
    const tabAdmin = document.getElementById('tab-admin');

    const loginArea = document.getElementById('login-area');
    const registerArea = document.getElementById('register-area');
    const teacherRegisterArea = document.getElementById('teacher-register-area');
    const adminPanel = document.getElementById('admin-panel');
    const studentPanel = document.getElementById('student-panel');

    tabLogin.onclick = ()=>{ show('login'); };
    tabRegister.onclick = ()=>{ show('register'); };
    tabTeacherReg.onclick = ()=>{ show('teacherRegister'); };
    tabAdmin.onclick = ()=>{ show('admin'); };

    function show(name){
      loginArea.style.display = (name==='login')?'block':'none';
      registerArea.style.display = (name==='register')?'block':'none';
      teacherRegisterArea.style.display = (name==='teacherRegister')?'block':'none';
      adminPanel.style.display = (name==='admin')?'block':'none';
      studentPanel.style.display = (name==='student')?'block':'none';
    }

    // Login
    document.getElementById('btn-login').addEventListener('click', async ()=>{
      const email = document.getElementById('login-email').value.trim();
      const pass = document.getElementById('login-pass').value;
      const msg = document.getElementById('login-msg');
      msg.textContent = 'Зачекайте...';
      if(!email||!pass){ msg.textContent='Заповніть email і пароль'; return; }
      try{
        const cred = await auth.signInWithEmailAndPassword(email,pass);
        const uid = cred.user.uid;
        const userRec = (await db.ref('users/'+uid).once('value')).val() || {};
        const role = userRec.role;
        if(role==='student'){ showStudent(uid, userRec.name || email); msg.textContent=''; }
        else if(role==='teacher'){ msg.textContent='Увійшов вчитель — використайте адміністративні функції у Console або спеціальну панель (в майбутньому можна додати)'; }
        else if(role==='admin'){ show('admin'); msg.textContent='Вхід як адмін'; }
        else{ msg.textContent='Користувач не має призначеної ролі. Зверніться до адміністратора.'; await auth.signOut(); }
      }catch(e){ msg.textContent = 'Помилка: '+e.message; }
    });

    document.getElementById('btn-logout').addEventListener('click', ()=>{ auth.signOut(); location.reload(); });

    // Student register
    document.getElementById('btn-register-stu').addEventListener('click', async ()=>{
      const name = document.getElementById('stu-name').value.trim();
      const email = document.getElementById('stu-email').value.trim();
      const pass = document.getElementById('stu-pass').value;
      const msg = document.getElementById('reg-stu-msg');
      if(!name||!email||!pass){ msg.textContent='Заповніть всі поля'; return; }
      msg.textContent = 'Реєстрація...';
      try{
        const cred = await auth.createUserWithEmailAndPassword(email,pass);
        const uid = cred.user.uid;
        await db.ref('users/'+uid).set({role:'student', email, name});
        await db.ref('students/'+uid).set({name, balance:0});
        msg.textContent = 'Реєстрація пройшла успішно. Увійдіть.';
        // sign out to allow login flow
        await auth.signOut();
      }catch(e){ msg.textContent = 'Помилка: '+e.message; }
    });

    // Teacher register (creates auth user + role teacher)
    document.getElementById('btn-register-teacher').addEventListener('click', async ()=>{
      const name = document.getElementById('tech-name').value.trim();
      const email = document.getElementById('tech-email').value.trim();
      const pass = document.getElementById('tech-pass').value;
      const msg = document.getElementById('reg-tech-msg');
      if(!name||!email||!pass){ msg.textContent='Заповніть всі поля'; return; }
      msg.textContent = 'Реєстрація вчителя...';
      try{
        const cred = await auth.createUserWithEmailAndPassword(email,pass);
        const uid = cred.user.uid;
        await db.ref('users/'+uid).set({role:'teacher', email, name});
        msg.textContent = 'Вчитель зареєстрований. Ви можете виходити та увійти під новим обліковим записом.';
        await auth.signOut();
      }catch(e){ msg.textContent = 'Помилка: '+e.message; }
    });

    // Admin actions
    document.getElementById('btn-distribute-monthly').addEventListener('click', async ()=>{
      const amt = parseInt(document.getElementById('monthly-amount').value||0);
      const msg = document.getElementById('distribute-msg');
      if(!amt || amt===0){ msg.textContent='Вкажіть суму більшу за 0'; return; }
      msg.textContent = 'Нарахування...';
      try{
        const snap = await db.ref('students').once('value');
        const students = snap.val() || {};
        const updates = {};
        for(const sid in students){
          const cur = Number(students[sid].balance||0);
          updates['/students/'+sid+'/balance'] = cur + amt;
          // optionally log transaction
          const tx = { studentId: sid, amount: amt, by: 'admin-monthly', ts: Date.now() };
          const txKey = db.ref('transactions').push().key;
          updates['/transactions/'+txKey] = tx;
        }
        await db.ref().update(updates);
        msg.textContent = 'Готово — нараховано всім учням по '+amt+' вогників';
      }catch(e){ msg.textContent = 'Помилка: '+e.message; }
    });

    // Admin create student (DB record). Note: recommend to create Auth user via Console for full login.
    document.getElementById('admin-create-student').addEventListener('click', async ()=>{
      const email = document.getElementById('admin-new-stu-email').value.trim();
      const name = document.getElementById('admin-new-stu-name').value.trim();
      const bal = parseInt(document.getElementById('admin-new-stu-balance').value||0);
      const msg = document.getElementById('admin-msg');
      if(!email||!name){ msg.textContent='Вкажіть email та ім\'я'; return; }
      try{
        // create DB student
        const newRef = await db.ref('students').push({name, balance: bal, email});
        // Add to users as student (without Auth). For Auth create user via Console.
        await db.ref('users/'+newRef.key).set({role:'student', email, name});
        msg.textContent = `Учень створений (DB id: ${newRef.key}). Рекомендовано створити Auth-обліковий запис у Firebase Console з цим email.`;
      }catch(e){ msg.textContent = 'Помилка: '+e.message; }
    });

    // Admin remove user by UID (DB only)
    document.getElementById('admin-remove-user').addEventListener('click', async ()=>{
      const uid = document.getElementById('admin-remove-uid').value.trim();
      const msg = document.getElementById('admin-msg');
      if(!uid){ msg.textContent='Введіть UID'; return; }
      try{
        await db.ref('users/'+uid).remove();
        await db.ref('students/'+uid).remove();
        msg.textContent = `Користувач ${uid} видалений з DB (Authentication слід видалити в Console, якщо потрібно).`;
      }catch(e){ msg.textContent = 'Помилка: '+e.message; }
    });

    // Show student UI
    async function showStudent(uid, name){
      document.getElementById('me-name').textContent = name || '';
      show('student');
      await loadBalance(uid);
    }
    async function loadBalance(uid){
      const snap = await db.ref('students/'+uid).once('value');
      const data = snap.val() || {};
      document.getElementById('me-balance').textContent = Number(data.balance||0);
    }
    document.getElementById('btn-refresh-balance').addEventListener('click', async ()=>{
      const user = auth.currentUser;
      if(user) await loadBalance(user.uid);
    });

    // Auth state listener: show logout if logged in
    auth.onAuthStateChanged(user=>{
      if(user){
        document.getElementById('btn-logout').style.display = 'inline-block';
      } else {
        document.getElementById('btn-logout').style.display = 'none';
      }
    });

  </script>
</body>
</html>
