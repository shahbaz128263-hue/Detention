# Detention Memo App — Android APK (GitHub Actions se auto-build)

Ye repo aapki Detention Memo web app ko Capacitor ke through Android APK me convert karta hai.
GitHub Actions workflow (`.github/workflows/build-apk.yml`) automatically APK bana deta hai jab bhi aap `main`/`master` branch pe push karte ho.

## Setup Steps (ek baar karna hai)

1. **Is poore folder ko apne GitHub repo me upload/push karo:**
   ```bash
   git init
   git add .
   git commit -m "Initial Capacitor Android setup"
   git branch -M main
   git remote add origin https://github.com/<aapka-username>/<repo-name>.git
   git push -u origin main
   ```

2. Push hote hi **GitHub Actions tab** me jaake dekho — "Build Android APK" workflow automatically chalega.

3. Workflow complete hone ke baad:
   - Repo ke **Actions** tab me jao
   - Latest run pe click karo
   - Neeche **Artifacts** section me `detention-memo-app-debug` milega
   - Usse download karo — ye ek `.zip` hoga, andar `app-debug.apk` hai
   - Us APK ko apne Android phone me transfer karke install kar lo (Unknown Sources allow karna padega settings me)

## App me update kaise karein

Jab bhi aapko app ka content/design change karna ho:
1. `www/index.html` file ko edit karo (yehi aapki poori app hai — HTML/CSS/JS sab isi me hai)
2. Commit + push karo
3. GitHub Actions automatically naya APK bana dega

## App ki Details

- **App Name:** Detention Memo
- **App ID:** com.detentionmemo.app
- **Type:** Capacitor-wrapped WebView app (poori app HTML/CSS/JS se bani hai, `www/index.html` me)
- **Data storage:** App ke andar hi `localStorage` me save hota hai (sections, trains, remarks, recent history) — phone pe hi rehta hai, offline bhi kaam karta hai.

## Agar aap khud apne computer pe build karna chahein (optional)

Agar GitHub Actions ke bina bhi local machine pe try karna ho (Android Studio + JDK 17 install hona chahiye):

```bash
npm install
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug
```

APK yahan milega: `android/app/build/outputs/apk/debug/app-debug.apk`

## Release/Signed APK (Play Store ke liye)

Ye workflow **debug APK** banata hai — testing/personal use ke liye theek hai (seedha install ho jayega).
Agar Play Store pe daalna ho ya production-signed APK chahiye, to keystore signing add karni padegi — bata dena, wo workflow bhi bana dunga.
