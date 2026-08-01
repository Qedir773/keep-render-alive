# 🛠️ cron-job.org Qurma Təlimatı

Bu, Render saytlarını hər 2 dəqiqədən bir oyadacaq **əsas pinger**-dir.

## Addım 1: Qeydiyyat

1. Brauzerdə aç: **https://cron-job.org**
2. **Sign Up** düyməsini bas
3. Qeydiyyat formasını doldur:
   - Username
   - Email
   - Şifrə
4. Email-ə gəlmiş təsdiq linkini bas

## Addım 2: Login

- Email və şifrə ilə daxil ol
- "Cronjobs" tab-ına keç

## Addım 3: Hər URL üçün Cron Job Yarat

Yalnız **1** misal göstərirəm — qalan 2 üçün eyni addımları təkrarla:

### Cron Job #1: qerarlari-avtomatik-yazdirma

1. **"+ Create cronjob"** düyməsini bas
2. Formu doldur:

| Sahə | Dəyər |
|------|-------|
| Title | `render-awake-qerarlari` |
| Address | `https://qerarlari-avtomatik-yazdirma.onrender.com/` |
| Schedule | `*/2 * * * *` (hər 2 dəq) |
| Request method | `GET` |
| Timeout | `30 seconds` |
| Save Responses | ✅ (yoxlamaq üçün) |

3. **Save** bas

### Cron Job #2: sivi-yarat

Eyni addımlarla, fərqi:
- Title: `render-awake-sivi-yarat`
- Address: `https://sivi-yarat.onrender.com/`
- Schedule: `*/2 * * * *`

### Cron Job #3: evtap

Eyni addımlarla, fərqi:
- Title: `render-awake-evtap`
- Address: `https://evtap.onrender.com/`
- Schedule: `*/2 * * * *`

## Addım 4: Test Et

Yeni yaradılmış hər cronjob üçün:
1. **"Run now"** düyməsini bas (sıralama: ən sağda)
2. "History" tab-ına keç
3. Uğurlu tarixçə görünməlidir:
   - **URL:** saytın URL-i
   - **Status code:** `200`
   - **Date:** indiki vaxt

## ✅ Hazırdır!

Hər 2 dəqiqədən bir hər 3 sayta ping gedəcək. Yoxlamaq üçün:
- 5 dəq gözlə
- History tab-ına bax — bir neçə uğurlu qeyd olmalıdır

---

## ❓ Problem yaranarsa

| Problem | Həll |
|---------|------|
| Email təsdiq gəlmir | Spam qovluğunu yoxla |
| "Schedule syntax error" | Cron formatına bax — `*/2 * * * *` |
| Status code 000 | Sayt hələ cold start-dadır, 30-60 san gözlə |
| Cron job işləmir | Free plan limits yoxdur, lakin brauzer sessiyasından asılı ola bilər |

İkinci addım: `SETUP-uptimerobot.md` faylına bax.
