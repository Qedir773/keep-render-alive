# Keep Render Services Alive

Bu repo Render platformasında yerləşdirilmiş 3 veb-saytı oyaq saxlamaq üçündür.

## 🛡️ Üçqat Müdafiə

| Servis | Interval | Funksiya |
|--------|----------|----------|
| cron-job.org | 2 dəq | Əsas pinger |
| GitHub Actions (bu repo) | 10 dəq | Backup pinger |
| UptimeRobot | 5 dəq | Monitorinq + alert |

## 🌐 İzlənən Saytlar

- https://qerarlari-avtomatik-yazdirma.onrender.com/
- https://sivi-yarat.onrender.com/
- https://evtap.onrender.com/

## 🔧 Qurulma

1. **cron-job.org** — 3 cron job yaradın (hər 2 dəqiqə)
2. **Bu repo** — workflow faylı hər 10 dəqiqə ping atır
3. **UptimeRobot** — 3 monitor yaradın (hər 5 dəqiqə) + email alert

## 📋 Workflow Haqqında

- **Tetik:** Hər 10 dəqiqədən bir (`*/10 * * * *`)
- **Manual tetik:** Actions tab → "Run workflow"
- **Log:** Hər URL üçün HTTP status kodu
