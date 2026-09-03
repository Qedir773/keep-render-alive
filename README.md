# Keep Render Alive

Render Free planında yerləşdirilmiş **qerarlari-avtomatik-yazdirma** saytını yuxuya getməyə qoymamaq üçün.

## 🔍 Niyə sayt yenə yuxuya gedirdi?

Render Free planı bir web servisi **15 dəqiqə** heç trafik almasa avtomatik yuxuya keçirir. Bu repodakı `keep-alive.yml` workflow-u hər 5 dəqiqədə bir ping atmalı idi — nəzəri baxımdan kifayət qədər tez-tez olmalıydı.

Problem GitHub Actions-un özündə idi: **planlaşdırılmış (`schedule`) tetikləyicilər dəqiq vaxtında işə düşəcəyinə zəmanət vermir**. GitHub-un rəsmi sənədlərinə görə, xüsusilə "izdihamlı" dəqiqələrdə (hər saatın başlanğıcı, dəqiqə 00, 05, 10 və s.) run-lar gecikə və ya bəzən **ümumiyyətlə buraxıla** bilər. Köhnə cron ifadəsi (`*/5 5-17 * * *`) məhz bu izdihamlı dəqiqələrə düşürdü. Nəticədə arabir 15+ dəqiqəlik boşluqlar yaranıb, Render sayta yenidən yuxuya gedirdi.

## ✅ Nə dəyişdi

`.github/workflows/keep-alive.yml`:

1. **Cron dəqiqələri sürüşdürüldü** — `2-59/5` (dəqiqə 2-dən başlayır), ki GitHub-un ən izdihamlı olduğu tam dəqiqələrə düşməsin.
2. **Hər run daxilində 2 dəfə ping** — birinci dərhal, ikincisi 4 dəqiqə sonra. Beləliklə xarici tetikləyici gecikəndə və ya bir dəfə buraxılanda belə, əvvəlki run-un "quyruğu" boşluğu doldurur və 15 dəqiqəlik yuxu həddinə çatmır.
3. **`concurrency` qrupu** əlavə edildi ki, üst-üstə düşən run-lar yığılıb qalmasın — yeni tetiklənən run köhnəsini əvəz edir.
4. **`retry` əlavə edildi** curl sorğusuna, keçici şəbəkə xətalarına qarşı.

`.github/workflows/repo-heartbeat.yml` (yeni):

- GitHub qaydası: repoda **60 gün** ərzində heç bir push olmasa, bütün scheduled workflow-lar (keep-alive daxil) **avtomatik deaktiv edilir**. Sadəcə workflow-un işləməsi bunu qabaqlamır — əsl commit lazımdır. Bu iş ayda bir dəfə boş commit atıb bu sayğacı sıfırlayır.

## ⚠️ Diqqət: yalnız 1 sayt əhatə olunur

Bu repo hazırda YALNIZ `qerarlari-avtomatik-yazdirma.onrender.com` saytını ping edir (əvvəlki `sivi-yarat` və `evtap` 2026-09-01-də bilərəkdən silinib). Əgər digər saytlar da yuxuya gedirsə, bu workflow onları əhatə etmir.

## 🛡️ Xarici pinger-lər (tövsiyə olunur)

GitHub Actions-un planlaşdırma qeyri-dəqiqliyi səbəbindən, **ən etibarlı həll xarici pinger istifadə etməkdir** (onlar öz infrastrukturunda dəqiq işləyir, GitHub-un növbəsindən asılı deyil):

- **cron-job.org** — bax `SETUP-cron-job.md` (2 dəqiqəlik interval, ən etibarlısı)
- **UptimeRobot** — bax `SETUP-uptimerobot.md` (5 dəqiqə + email alert, sayt düşəndə xəbərdarlıq edir)

Bu GitHub Actions workflow-u yalnız **backup** kimi düşünün. Əgər cron-job.org / UptimeRobot hesablarınızı əvvəllər qurmusunuzsa, onların hələ də aktiv olduğunu yoxlayın (free planlarda bəzən uzun müddət istifadə olunmayan job-lar pauza edilir).

## 📋 Manual test

Actions tab → "Keep Render Services Alive" → "Run workflow" düyməsi ilə əl ilə də işə sala bilərsiniz.
