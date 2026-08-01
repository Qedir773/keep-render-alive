# 📊 UptimeRobot Qurma Təlimatı

Bu, Render saytları 5 dəqiqəlik intervalla yoxlayacaq və **email alert** göndərəcək (sayt dayananda).

## Addım 1: Qeydiyyat

1. Brauzerdə aç: **https://uptimerobot.com**
2. **Register for FREE** düyməsini bas
3. Formu doldur:
   - Email
   - Şifrə
   - Şifrə təkrar
4. Email-ə gəlmiş təsdiq linkini bas

## Addım 2: Login və Dashboard

- Daxil olduqda səni Dashboard-a yönləndirəcək
- Yuxarı sağda **"+ Add New Monitor"** düyməsini görəcəksən

## Addım 3: Hər URL üçün Monitor Yarat

### Monitor #1: qerarlari-avtomatik-yazdirma

1. **"+ Add New Monitor"** bas
2. Formu doldur:

| Sahə | Dəyər |
|------|-------|
| Monitor Type | `HTTP(s)` |
| Friendly Name | `qerarlari-avtomatik-yazdirma` |
| URL (or IP) | `https://qerarlari-avtomatik-yazdirma.onrender.com/` |
| Monitoring Interval | `5 minutes` (Free tier minimum) |
| Monitor Timeout | `30 seconds` |
| Check `*` Alert Contact | Email-in (avtomatik əlavə olunur) |

3. **Create Monitor** bas

### Monitor #2: sivi-yarat

Eyni addımlarla:
- Friendly Name: `sivi-yarat`
- URL: `https://sivi-yarat.onrender.com/`
- Interval: `5 minutes`

### Monitor #3: evtap

Eyni addımlarla:
- Friendly Name: `evtap`
- URL: `https://evtap.onrender.com/`
- Interval: `5 minutes`

## Addım 4: Dashboard Yoxlaması

1-2 dəqiqədən sonra dashboard-da:
- Bütün 3 monitor görünməlidir
- Status **"Up"** (yaşıl) olmalıdır
- "Uptime" göstəricisi 99.9%+ göstərməlidir

## Addım 5: Email Alert Test (Vacib!)

1. **evtap** monitoruna kliklə
2. **Edit** düyməsini bas
3. URL-i dəyişdir: `https://evtap.onrender.com/error` (qəsdən yanlış)
4. **Save** bas
5. 10 dəqiqə gözlə — email-ə **"Monitor is Down"** mesajı gəlməlidir
6. URL-i geri **düzəlt**: `https://evtap.onrender.com/`
7. 5 dəqiqə sonra email-ə **"Monitor is Back Up"** mesajı gəlməlidir

**⚠️ Əgər email gəlməsə:** Spam qovluğunu yoxla, həmçinin UptimeRobot-da "My Settings → Alert Contacts" bölməsindən email-i təsdiqlə.

## ✅ Hazırdır!

İndi var:
- **cron-job.org**: hər 2 dəq ping (əsas)
- **GitHub Actions**: hər 10 dəq ping (backup)
- **UptimeRobot**: hər 5 dəq yoxlama + email alert

Saytlarınız indi daim oyaq qalacaq! 🎉

---

## 📧 Bonus: Email Ayarları

**Birdən çox email əlavə etmək:**
- My Settings → Alert Contacts → "Add Alert Contact"
- E-poçt ünvanı əlavə et
- Təsdiq email al, linki bas

**Birdən çox email alert saytı:**
- Hər monitor üçün ayrı "Alert Contact" seçə bilərsən
- Və ya hamısına eyni kontakt siyahısını bağlaya bilərsən

## ❓ Problem yaranarsa

| Problem | Həll |
|---------|------|
| Email gəlmir | Spam qovlağını yoxla, "Alert Contacts" siyahısında email-in olduğunu yoxla |
| 5 dəq interval seçə bilmirəm | Bu Free tier minimum, dəyişdirilə bilməz |
| Status "Down" göstərir, amma sayt işləyir | Cold start ola bilər — 1-2 dəq gözlə, monitor yenidən yoxlayacaq |
| Çoxlu yanlış alert | UptimeRobot "consecutive failures" sayını artırmaq olmaz (free tier) |
