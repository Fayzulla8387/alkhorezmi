# Firebase sozlash qo'llanmasi (8-sinf CS Foundation sayti)

Papka tarkibi: `public/` (sayt fayllari), `firestore.rules` (xavfsizlik qoidalari), `firebase.json`.

## 1. Loyiha yaratish
1. https://console.firebase.google.com → **Add project** → nom bering (masalan `cs8-foundation`) → Google Analytics kerak emas.

## 2. Web ilova va config
1. Project overview → **</> (Web)** → ilova nomini yozing → **Register app** (Hosting'ni hozircha tanlamang).
2. Chiqqan `firebaseConfig` qiymatlarini `public/firebase-config.js` fayliga ko'chiring.

## 3. Authentication
1. **Build → Authentication → Get started → Sign-in method → Email/Password → Enable → Save**.
2. **Users → Add user**: Email `mentor@cs8.uz`, Parol — **mentorlar uchun umumiy parol** (kamida 6 belgi, murakkab qiling). Mentorlar saytda "Mentor" bo'limiga faqat shu parolni yozib kiradi.
3. O'quvchilar login'i avtomatik `login@cs8.uz` ko'rinishida saqlanadi (haqiqiy pochta kerak emas).

## 4. Firestore
1. **Build → Firestore Database → Create database** → Production mode → joylashuv (masalan `eur3` yoki `europe-west`) → Enable.
2. **Rules** tabiga `firestore.rules` faylidagi matnni to'liq qo'ying → **Publish**.

## 5. Hosting va deploy
```
npm install -g firebase-tools
firebase login
firebase init        # Firestore + Hosting ni tanlang; mavjud loyihani (cs8-foundation) tanlang;
                     # rules fayli: firestore.rules (almashtirmang); public papka: public; single-page app: No
firebase deploy
```
Terminal oxirida sayt manzili chiqadi: `https://<loyiha>.web.app`.

## 6. Tekshirish
1. Saytni oching → "Ro'yxatdan o'tish" → viloyat, tuman, login, parol → kirish.
2. Boshqa brauzerda "Mentor" bo'limidan umumiy parol bilan kiring — o'quvchi ro'yxatda ko'rinishi kerak.
3. Firestore → `students` kolleksiyasida hujjat paydo bo'lganini ko'ring.

## Sozlamalar
- **Mentor parolini almashtirish:** Authentication → Users → `mentor@cs8.uz` → ⋮ → Reset password (yoki foydalanuvchini o'chirib, yangi parol bilan qayta qo'shing).
- **Tumanlarni qo'shish:** `public/index.html` ichidagi `const TUM={...}` ga viloyat bo'yicha ro'yxat qo'shing, masalan `"Andijon":["Asaka","Xonobod"]`. Ro'yxati yo'q viloyatda tuman qo'lda yoziladi (birinchi harf avtomatik katta qilinadi).
- **O'quvchi parolini unutsa:** Authentication → Users → login@cs8.uz → Reset password; yoki o'chirib, qayta ro'yxatdan o'tkazing.
- **Ma'lumotni yuklab olish:** Mentor panelidagi **CSV** tugmasi (Excel'da ochiladi).

## Xavfsizlik haqida
- O'quvchi faqat o'z hujjatini o'qiy va yoza oladi; hamma o'quvchilarni faqat `mentor@cs8.uz` hisobi ko'radi.
- Tuman bo'yicha saralash mentor panelida qulaylik uchun (filtr). Umumiy parolni bilgan har kim hamma tumanlarni ko'ra oladi — shuning uchun parolni faqat mentorlarga bering va vaqti-vaqti bilan almashtiring. Har tuman uchun alohida parol kerak bo'lsa, ayting, sozlab beraman.
- Ballar brauzerdan yuboriladi; texnik bilimli o'quvchi o'z natijasini qo'lda o'zgartira olishi mumkin. Qat'iy nazorat kerak bo'lsa, quiz tekshiruvini Cloud Functions'ga ko'chirish kerak (Blaze rejasi talab qilinadi).
- Firebase bepul (Spark) rejasi o'rta guruhlar uchun yetarli; Console → Usage bo'limidan kuzatib boring.
