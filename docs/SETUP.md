# การตั้งค่า Nong Khai Trip

## สิ่งที่ต้องมี

- Node.js 22.13 ขึ้นไปและ npm
- Expo Go ที่รองรับ SDK 57 หรือ Development Build ของโปรเจกต์
- มือถือหรือ Emulator สำหรับทดสอบ
- มือถือและคอมพิวเตอร์อยู่ในเครือข่ายเดียวกันเมื่อใช้ LAN

## ติดตั้งโปรเจกต์

```bash
git clone https://github.com/jutatipp/appNong-Khai-Trip_Assignment11.git "AppNong Khai Trip_Hybrid_Mobile"
cd "AppNong Khai Trip_Hybrid_Mobile"
npm ci
```

## เปิด API และแอป

เปิดสอง Terminal ในโฟลเดอร์โปรเจกต์

Terminal 1:

```bash
npm run server
```

Terminal 2:

```bash
npm start -- --lan
```

สแกน QR ล่าสุดจาก Terminal ที่เปิด Expo หาก Expo ขอเข้าสู่ระบบ ให้ใช้ `npx expo login` และตรวจบัญชีด้วย `npx expo whoami`

## บัญชีสาธิต

| ข้อมูล   | ค่า                 |
| -------- | ------------------- |
| อีเมล    | `jutatip@gmail.com` |
| รหัสผ่าน | `123456`            |

Remember Me เก็บ Session ใน SecureStore หาก API รีสตาร์ต Session เดิมจะใช้ไม่ได้และต้องเข้าสู่ระบบใหม่

## ตั้งค่า API

แอปใช้ Host ของ Expo เป็นที่อยู่ API อัตโนมัติ หากต้องกำหนดเอง ให้คัดลอก `.env.example` เป็น `.env` แล้วใส่:

```dotenv
EXPO_PUBLIC_API_URL=http://<LAN-IP-คอมพิวเตอร์>:3001
```

หลังแก้ `.env` ให้หยุด Expo แล้วเปิดใหม่ด้วย:

```bash
npm start -- --clear
```

| อุปกรณ์          | API URL                            |
| ---------------- | ---------------------------------- |
| iOS Simulator    | `http://localhost:3001`            |
| Android Emulator | `http://10.0.2.2:3001`             |
| มือถือจริง       | `http://<LAN-IP-คอมพิวเตอร์>:3001` |

ตรวจ API บนคอมพิวเตอร์ที่ `http://localhost:3001/health` ซึ่งควรแสดง `{"ok":true}` บนมือถือ `localhost` หมายถึงมือถือเอง จึงต้องใช้ LAN IP ของคอมพิวเตอร์

## แก้ปัญหาเชื่อมต่อ

- ตรวจว่า `npm run server` และ Expo ยังทำงานอยู่
- เปิด Health check จากมือถือโดยใช้ LAN IP ของคอมพิวเตอร์
- ตรวจว่ามือถือกับคอมพิวเตอร์อยู่ Wi-Fi เดียวกัน
- หากเปลี่ยน Wi-Fi ให้ตรวจ IP และสแกน QR ใหม่
- หลังเปลี่ยนโค้ด Server ให้หยุดและเปิด `npm run server` ใหม่
- หาก API รีสตาร์ต ให้เข้าสู่ระบบใหม่
- Expo Tunnel ส่งต่อ Metro แต่ไม่ส่งต่อ API ที่ Port 3001

## Development Build

```bash
npx expo run:android
# หรือบน macOS ที่ติดตั้ง Xcode และยอมรับ License แล้ว
npx expo run:ios
npm run dev-client
```

Android Production Build ต้องกำหนด `GOOGLE_MAPS_ANDROID_API_KEY` และจำกัด Key ตาม Package กับ Signing certificate ส่วน iOS ใช้ Apple Maps เป็นค่าเริ่มต้น เมื่อเปลี่ยน Native module หรือ Config plugin ต้องสร้าง Build ใหม่

## ตรวจโปรเจกต์

```bash
npm run typecheck
npm test
npm run format:check
npx expo-doctor
npx expo export --platform ios --platform android --output-dir /tmp/nongkhai-export
```

การ Export ตรวจ JavaScript และ Assets แต่ไม่แทนการทดสอบกล้อง แผนที่ Permission และ Notification บนมือถือจริง ดูรายการที่ยังต้องทดสอบใน [TESTING.md](TESTING.md)
