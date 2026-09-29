# ประยุกต์ Assignment Week 1–12 เป็น Nong Khai Trip

ขอบเขตที่ผู้ใช้เลือก: แอปแพลนทริปเที่ยวหนองคาย ใช้ธีมล่าสุด เพิ่มสถานที่เข้าทริป และเก็บภาพความทรงจำในแต่ละทริป กล้องใช้โค้ด Photo_camera-_expo ของผู้ใช้

บทเรียนต้นฉบับใช้ Campus Events; ตารางนี้อธิบายการประยุกต์เป็น Trip ไม่ได้อ้างว่าโครงสร้างธุรกิจเหมือน Lab ตรงตัว หรือผู้สอนรับรองการเปลี่ยนแล้ว

| Week / บทเรียน                                           | เรียนอะไร                                                       | ใช้ในระบบนี้                                                                                                                 | ไฟล์หลัก                                                                                 |
| -------------------------------------------------------- | --------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| [1](https://tanapattara.github.io/react_native/week-01)  | React Native, Expo, TypeScript, setup และ Profile               | โปรเจกต์มือถือ หน้าโปรไฟล์ และ README วิธีติดตั้ง                                                                            | `package.json`, `app/(tabs)/profile.tsx`                                                 |
| [2](https://tanapattara.github.io/react_native/week-02)  | Components, Props, State และ callback                           | การ์ดสถานที่ หัวใจ ปุ่มเพิ่มทริป และ UI ที่ใช้ซ้ำ                                                                            | `src/components/PlaceCard.tsx`, `src/components/ui.tsx`                                  |
| [3](https://tanapattara.github.io/react_native/week-03)  | Styling, responsive, FlatList, Safe Area, Loading/Empty/Error   | รายการสถานที่และทริป ธีมเดียวกันและสถานะข้อมูล                                                                               | `src/components/PlaceList.tsx`, `app/(tabs)/trips.tsx`, `src/theme`                      |
| [4](https://tanapattara.github.io/react_native/week-04)  | Expo Router, Tabs/Stack, dynamic ID และ deep link               | สำรวจ → เลือกทริป/สร้าง → รายละเอียดทริป และเปิดจากแจ้งเตือน                                                                 | `app/_layout.tsx`, `app/trips`, `app/places/[id].tsx`                                    |
| [5](https://tanapattara.github.io/react_native/week-05)  | Search, form validation, state ownership, keyboard และกันส่งซ้ำ | ฟอร์มชื่อ/เวลาเดินทาง เลือกสถานที่และจัดลำดับ ใช้แทน Registration form ของ Lab                                               | `app/trips/edit.tsx`, `src/utils/tripDate.ts`, `src/context/TripContext.tsx`             |
| [6](https://tanapattara.github.io/react_native/week-06)  | REST API, GET/POST, validation, errors และ retry                | อ่านสถานที่/ทริป สร้าง/แก้ไข/ลบทริป และเพิ่มรูปด้วย ID เดิมเพื่อ retry ไม่ซ้ำ                                                | `src/services/api.ts`, `src/services/trips.ts`, `server/index.mjs`                       |
| [7](https://tanapattara.github.io/react_native/week-07)  | AsyncStorage, SQLite, cache และ offline                         | เก็บ Favorite, cache สถานที่/ทริป และภาพรอส่งใน SQLite                                                                       | `src/services/storage.ts`, `src/services/tripStorage.ts`                                 |
| [8](https://tanapattara.github.io/react_native/week-08)  | Login, SecureStore, protected route/API, restore/logout/expiry  | ต้อง Login เพื่อจัดการทริป; API ตรวจเจ้าของทริป แทน protected registration                                                   | `src/context/AuthContext.tsx`, `app/login.tsx`, `server/index.mjs`                       |
| [9](https://tanapattara.github.io/react_native/week-09)  | Camera, Image Picker, permission, preview และ upload            | ถ่าย/เพิ่มรูปความทรงจำของแต่ละทริป เลือกโทนจากโค้ดผู้ใช้ บันทึกในทริปและลงคลังมือถือ                                         | `src/components/TripCamera.tsx`, `src/components/camera`, `src/services/memoryPhotos.ts` |
| [10](https://tanapattara.github.io/react_native/week-10) | Location, Maps, marker และ permission                           | หมุดสถานที่ตามลำดับในทริป ตำแหน่งปัจจุบัน และยังเก็บฟอร์มเลือกหมุดสถานที่เดิม                                                | `src/components/TripMap.tsx`, `app/(tabs)/map.tsx`, `app/create.tsx`                     |
| [11](https://tanapattara.github.io/react_native/week-11) | Notifications, channel, schedule/cancel และ app lifecycle       | เตือนเมื่อถึงเวลาเที่ยวแต่ละสถานที่ แตะเปิดทริป และตั้งใหม่เมื่อแก้เวลา                                                      | `src/services/notifications.ts`, `src/components/NotificationObserver.tsx`               |
| [12](https://tanapattara.github.io/react_native/week-12) | Architecture, Performance และ Accessibility                     | แยกหน้าจอ/Context/Services ใช้ FlatList, cache, ลดขนาดภาพ และ Accessibility props; ยังต้องเก็บหลักฐาน Profiler และทดสอบ 200% | `docs/ARCHITECTURE.md`, `src/components/PlaceList.tsx`, `app/trips/[id].tsx`             |

## สถานะ Week 12

มีในโค้ดแล้ว:

- แยกหน้าจอและ routing ไว้ใน `app/`, ส่วน UI ร่วมใน `src/components/`, state ร่วมใน `src/context/` และ API/storage/device logic ใน `src/services/`
- ระบุ source of truth และการไหลของข้อมูลไว้ใน `docs/ARCHITECTURE.md`
- ใช้ `FlatList` กับ stable ID ในรายการสถานที่ ทริป แผนที่ และคลังภาพ
- อ่าน cache ก่อนขอข้อมูลใหม่ และลดด้านยาวของภาพไม่เกิน 1,600 px ก่อนบันทึก
- ใส่ `accessibilityLabel`, `accessibilityRole`, `accessibilityState` และ `accessibilityHint` ใน flow หลักหลายจุด

หลักฐานที่ยังต้องทำบนอุปกรณ์จริง:

- วัดด้วย React DevTools/Profiler และแก้ bottleneck ที่พิสูจน์ได้อย่างน้อย 1 จุด พร้อมผลก่อน–หลัง
- ทดสอบด้วย VoiceOver หรือ TalkBack และตัวอักษรขนาด 200%
- บันทึก Accessibility issues อย่างน้อย 5 จุด พร้อมภาพหรือผลก่อน–หลัง

## สิ่งที่นำมาประยุกต์

- ฟอร์มลงทะเบียนกิจกรรม → ฟอร์มสร้างและจัดการทริป
- Event API → Place/Trip API พร้อมตรวจเจ้าของและบันทึกภาพ
- ภาพกิจกรรม → อัลบั้มความทรงจำภายในแต่ละทริป ไม่บังคับภาพปกก่อนสร้าง
- เตือนก่อนกิจกรรม → เตือนเมื่อถึงเวลาเที่ยวแต่ละสถานที่
- UI ภาพอ้างอิงใช้เป็นแนวทางภาพ/การ์ด/สี ไม่เพิ่มโรงแรม เที่ยวบิน ชำระเงิน หรือบริการจอง

## หลักฐานก่อนส่ง

- [ ] ชื่อและรหัสผู้จัดทำจริง
- [ ] Clone/install/run จาก commit ที่ส่งจริง
- [ ] ภาพสองขนาดจอและ font scale 150%
- [ ] วิดีโอเพิ่มสถานที่ → สร้าง/เลือกทริป → เรียงสถานที่ → ดูแผนที่
- [ ] วิดีโอ Login/Logout/restore/expiry และการป้องกันทริป
- [ ] วิดีโอ offline/restart และ Favorite/Trip/ภาพรอส่งยังอยู่
- [ ] วิดีโอกล้อง/คลังภาพ/เปลี่ยนโทน/บันทึก ทั้งอนุญาต ปฏิเสธ และยกเลิก
- [ ] วิดีโอแจ้งเตือน foreground/background/cold start และ ID ไม่ถูกต้อง
- [ ] เปิด Development Build ตาม Lab 8 บนอุปกรณ์จริง
- [ ] Profiler trace และผลก่อน–หลังของจุดที่ปรับประสิทธิภาพตาม Lab 12
- [ ] วิดีโอ VoiceOver/TalkBack และตัวอักษร 200% พร้อม Accessibility fixes อย่างน้อย 5 จุด

มีโค้ดครอบคลุมหัวข้อไม่เท่ากับผ่านการทดสอบบนมือถือครบ ดูสถานะใน TESTING.md
