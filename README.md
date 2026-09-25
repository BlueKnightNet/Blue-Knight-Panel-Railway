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
فقط این‌ها روی Railway کار می‌کنن: **VLESS-WS-TLS**، **VMess-WS-TLS**، **Trojan-WS-TLS** و **VLESS-XHTTP-TLS** (فقط کلاینت‌های Xray) — همه روی پورت 443 با دامنه‌ی Railway.
لینک‌های ساب داخل پنل خودشون یه `token` مخصوص دارن؛ همونو توی v2rayNG / Hiddify بزن. این لینک رو پخش نکن.

### تنظیمات TLS لینک‌ها (اختیاری)
| متغیر | پیش‌فرض | توضیح |
|---|---|---|
| `DOMAIN` / `FORCE_HOST` | دامنه‌ی Railway | آدرس، Host و SNI لینک‌ها. اگه لینک‌ها IP نشون میدن، دامنه‌ت رو اینجا بذار (بدون `https://`). |
| `LINK_FP` | `chrome` | فینگرپرینت uTLS: `chrome` `firefox` `safari` `edge` `ios` `android` `random` `randomized` `360` `qq` یا `none` |
| `LINK_ALPN` | `http/1.1` | برای WebSocket باید `http/1.1` بمونه. `none` = حذف |
| `TLS_CIPHERS` | خالی | لیست cipher با کاما؛ فقط توی ساب sing-box (`tls.cipher_suites`) اعمال میشه. لینک‌های v2ray فیلد استاندارد cipher ندارن. |
| `LINK_SNI` / `LINK_HOST` | همون دامنه | برای CDN/دامنه‌ی سفارشی: SNI و هدر Host جدا. روی خود Railway باید دامنه‌ی Railway یا دامنه‌ی متصل‌شده باشن. |

### VLESS + XHTTP (فقط کلاینت‌های Xray)
پنل موقع اجرا خودش **Xray-core** رو دانلود می‌کنه (آخرین نسخه‌ی پایدار، با چک SHA-256) و یه لینک **VLESS-XHTTP-TLS** هم می‌سازه (پورت 443، TLS روی لبه‌ی Railway).
- کلاینت‌هایی که پشتیبانی می‌کنن: **v2rayNG**، **v2rayN**، **Hiddify** (با هسته‌ی Xray)، Streisand/V2Box با هسته‌ی Xray. کلاینت‌های sing-box و Clash **XHTTP ندارن**، برای همین این لینک فقط توی ساب v2ray (base64) هست، نه توی ساب Clash یا sing-box.
- لینک پیش‌فرض: `type=xhttp&mode=packet-up&alpn=h2`. لبه‌ی Railway روی h2 مذاکره می‌کنه و کلاینت Xray باید با همون ALPN وصل بشه؛ `alpn=http/1.1` با فینگرپرینت uTLS روی Railway کار **نمی‌کنه**.

| متغیر | پیش‌فرض | توضیح |
|---|---|---|
| `ENABLE_XHTTP` | روی Railway `true` | `false` = Xray دانلود/اجرا نمیشه و لینک XHTTP حذف میشه |
| `XRAY_VERSION` | آخرین نسخه | پین کردن نسخه، مثلاً `26.3.27` |
| `XRAY_URL` | خالی | آدرس zip دلخواه برای دانلود Xray |
| `XHTTP_MODE` | `packet-up` | مود داخل لینک: `packet-up` `stream-up` `stream-one` `auto` (سرور همه رو قبول می‌کنه) |
| `XHTTP_ALPN` | `h2` | ALPN داخل لینک XHTTP. `none` = حذف |

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
7. Use **VLESS-WS-TLS**, **VMess-WS-TLS**, **Trojan-WS-TLS** or **VLESS-XHTTP-TLS** (Xray clients) links (port 443, Railway domain). Subscription URLs in the panel include a private `token`.

Forgot password: set `RESET_PANEL_PASSWORD=true`, redeploy, create a new one, then remove the variable.
Only WebSocket / XHTTP over TLS on port 443 works on Railway. Optional overrides: `DOMAIN`, `FORCE_HOST`, `LINK_PORT`, `PUBLIC_BASE_URL`.

### Link TLS options (optional env vars)
| Variable | Default | Meaning |
|---|---|---|
| `DOMAIN` / `FORCE_HOST` | Railway domain (`RAILWAY_PUBLIC_DOMAIN`) | Address, Host and SNI used in links. Set this if links show an IP (bare hostname, no `https://`). |
| `LINK_FP` | `chrome` | uTLS fingerprint in links / Clash (`client-fingerprint`) / sing-box (`utls`): `chrome firefox safari edge ios android random randomized 360 qq`, or `none` to omit |
| `LINK_ALPN` | `http/1.1` | Comma list; keep `http/1.1` for WebSocket. `none` = omit |
| `TLS_CIPHERS` | empty | Comma list (e.g. `TLS_AES_128_GCM_SHA256,TLS_CHACHA20_POLY1305_SHA256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256`). Only applied to the sing-box subscription (`tls.cipher_suites`); v2ray share links have no standard cipher field. Note: Go ignores TLS 1.3 suite choices and uTLS fingerprints use their own suite list. |
| `LINK_SNI` / `LINK_HOST` | same as domain | Separate SNI / WS Host header for CDN fronting or a custom domain. On plain Railway both must be your Railway (or attached custom) domain. |
| `LINK_PORT` / `LINK_TLS` | `443` / auto | Override port shown in links / force TLS links on or off. |

### VLESS + XHTTP (Xray clients only)
At startup the panel downloads **Xray-core** (latest stable, SHA-256 verified against the release `.dgst`, cached in `BK_DATA_DIR/bin`) and serves a **VLESS-XHTTP-TLS** link on port 443 (TLS terminated by Railway's edge; Xray listens on `127.0.0.1` behind the panel's HTTP multiplexer).
- Supported clients: **v2rayNG**, **v2rayN**, **Hiddify** (Xray core), Streisand / V2Box (Xray core). sing-box and Clash/Mihomo clients do **not** support XHTTP, so the link is only in the v2ray (base64) subscription, not in the Clash or sing-box subscriptions.
- Default link: `type=xhttp&mode=packet-up&alpn=h2`. Railway's edge negotiates h2 and Xray's XHTTP client must use the same HTTP version as the edge; `alpn=http/1.1` (with a uTLS fingerprint) fails on Railway.

| Variable | Default | Meaning |
|---|---|---|
| `ENABLE_XHTTP` | `true` on Railway | `false` = don't download/run Xray, hide the XHTTP link |
| `XRAY_VERSION` | latest | Pin a version, e.g. `26.3.27` |
| `XRAY_URL` | empty | Custom Xray zip URL |
| `XHTTP_MODE` | `packet-up` | Mode written in the link: `packet-up`, `stream-up`, `stream-one`, `auto` (server accepts all) |
| `XHTTP_ALPN` | `h2` | ALPN written in the XHTTP link; `none` = omit |
