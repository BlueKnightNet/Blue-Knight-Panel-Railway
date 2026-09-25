# Blue Knight Gate — Railway Edition

پنل Blue Knight آماده‌ی دیپلوی روی Railway از طریق GitHub.
Telegram: https://t.me/BlueKnight_Net · YouTube: https://www.youtube.com/@BlueKnight-Net

## فارسی

### ۱) فورک
روی **Fork** بالای همین صفحه بزن تا یه کپی توی اکانت گیت‌هاب خودت ساخته بشه.

### ۲) دیپلوی روی Railway
1. وارد railway.com شو (Login with GitHub).
2. **New Project** ← **Deploy from GitHub repo** ← ریپوی فورک‌شده.
3. **Variables**:
   - `PORT` = `8080`
   - `BK_DATA_DIR` = `/data`
   - `SETUP_KEY` = یه کلید تصادفی (اختیاری ولی پیشنهادی؛ فقط برای ساخت رمز بار اول لازمه)
4. یه **Volume** با Mount Path `/data` وصل کن (UUID و رمز پنل اینجا ذخیره میشن).
5. **Settings ← Networking ← Generate Domain** با پورت `8080`.
6. صبر کن دیپلوی سبز (Active) بشه.

### ۳) ورود به پنل
1. برو `https://YOUR-DOMAIN.up.railway.app/knight`
2. **بار اول** صفحه‌ی «ساخت رمز پنل» میاد: رمز (حداقل ۸ کاراکتر) و تکرارش رو بزن (و اگه `SETUP_KEY` گذاشتی، اونم وارد کن).
3. دفعه‌های بعد با همون رمز وارد میشی. خروج: `/knight/logout`
4. بعد از دیپلوی سریع رمز بساز؛ تا وقتی رمز ساخته نشده، اولین کسی که آدرس رو باز کنه می‌تونه رمز بسازه (برای همین `SETUP_KEY` پیشنهاد میشه).

### ۴) کانفیگ‌ها
فقط این‌ها روی Railway کار می‌کنن: **VLESS-WS-TLS** و **VMess-WS-TLS**.
لینک‌های ساب داخل پنل خودشون یه `token` مخصوص دارن؛ همونو توی v2rayNG / Hiddify بزن. این لینک رو پخش نکن.

### رمز یادت رفت؟
متغیر `RESET_PANEL_PASSWORD=true` رو بذار، Redeploy کن، رمز جدید بساز، بعد **حتماً این متغیر رو پاک کن**.

### نکته‌ها
- اگه `up.railway.app` باز نشد، **Custom Domain** وصل کن و `DOMAIN` رو هم ست کن.
- Railway پلن رایگان دائمی نداره؛ قیمت‌ها رو از صفحه‌ی Pricing چک کن.
- آپدیت: توی فورکت **Sync fork** بزن؛ Railway خودکار دوباره دیپلوی می‌کنه.

## English

1. **Fork** this repo.
2. Railway: **New Project → Deploy from GitHub repo** → your fork.
3. Variables: `PORT=8080`, `BK_DATA_DIR=/data`, optional `SETUP_KEY` (required only for first password creation).
4. Add a **Volume** at `/data`.
5. **Settings → Networking → Generate Domain**, port `8080`.
6. Open `https://<domain>/knight`. First visit asks you to create a panel password; after that you log in with it. Logout: `/knight/logout`.
7. Use **VLESS-WS-TLS** or **VMess-WS-TLS** links. Subscription URLs in the panel include a private `token`.

Forgot password: set `RESET_PANEL_PASSWORD=true`, redeploy, create a new one, then remove the variable.
Only WebSocket over TLS on port 443 works on Railway. Optional overrides: `DOMAIN`, `FORCE_HOST`, `LINK_PORT`, `PUBLIC_BASE_URL`.