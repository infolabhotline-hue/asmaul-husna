# আসমাউল হুসনা – ৯৯ নাম মুখস্থ (অফলাইন অ্যাপ)

আল্লাহর ৯৯ নাম মুখস্থ করার অ্যাপ: তালিকা, ফ্ল্যাশকার্ড, কুইজ ও গজল (অটো স্ক্রল)।
পুরোটাই HTML/JS, কোনো ইন্টারনেট বা সার্ভার লাগে না। Capacitor দিয়ে Android APK বানানো যায়।

## ফোল্ডার
```
www/                 অ্যাপের সব কোড (index.html), গজল অডিও (audio/gojol.mp3), PWA ফাইল
capacitor.config.json  অ্যাপের নাম ও আইডি
.github/workflows/   GitHub Actions: স্বয়ংক্রিয় APK বিল্ড
```

## ১) GitHub দিয়ে APK বিল্ড (সবচেয়ে সহজ)
```bash
git init && git add . && git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/<আপনার-ইউজার>/asmaul-husna.git
git push -u origin main
```
পুশ করলে GitHub → **Actions → Build APK** চলবে। শেষ হলে রান পেজের নিচে **Artifacts** থেকে
`asmaul-husna-apk` নামিয়ে ফোনে `app-debug.apk` ইনস্টল করুন
(ফোনে "Install unknown apps" অনুমতি লাগবে)।

## ২) নিজের কম্পিউটারে বিল্ড
দরকার: Node 20+, JDK 21, Android SDK (Android Studio)।
```bash
npm install
npx cap add android
npx cap sync android
cd android && ./gradlew assembleDebug
# APK: android/app/build/outputs/apk/debug/app-debug.apk
```
Android Studio-তে খুলতে: `npx cap open android`

## ৩) ব্রাউজারে টেস্ট
```bash
npm run serve    # http://localhost:8080
```

## ফোনে (PWA) ইনস্টল
`www/` ফোল্ডারটি কোনো HTTPS হোস্টে (GitHub Pages ইত্যাদি) রাখলে ব্রাউজার থেকে
"Add to Home screen" করা যায়; এরপর অফলাইনে চলে।

## পরিবর্তন করতে
- নাম/অর্থ/আরবি: `www/index.html`-এর `const D=` অংশ।
- গজল: `www/audio/gojol.mp3` বদলান। নামের সময় `www/index.html`-এ `G.s`/`G.e` (শুরু/শেষ সেকেন্ড) ঠিক করুন।
- অ্যাপ আইডি/নাম: `capacitor.config.json` (প্রকাশের আগে `appId` বদলান)।

## জানা সীমাবদ্ধতা
- অ্যাপে (APK) নাম পড়ে শোনানো হয় Android-এর নিজস্ব Text-to-speech দিয়ে (`@capacitor-community/text-to-speech`)।
  ফোনের Settings → Text-to-speech-এ আরবি ও বাংলা ভাষা/ভয়েস ইনস্টল থাকতে হবে, নইলে অ্যাপ লাল বার্তা দেখাবে।
- গজলটি ডিস্ট্রিবিউট করার আগে অডিওর কপিরাইট/অনুমতি নিশ্চিত করুন।
- APK ডিবাগ-সাইনড; Play Store-এর জন্য রিলিজ কিস্ট্যোর দিয়ে সাইন করতে হবে।
