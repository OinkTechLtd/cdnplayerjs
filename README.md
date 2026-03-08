# CDNPlayerJS

Статический плеер на базе `Playerjs` с поддержкой:

- прямых потоков (`.m3u8`, `.mp4`, и т.д.);
- удалённых плейлистов `.m3u` и `.txt`;
- шифрованных ссылок (AES-GCM) для шаринга потока.

## Как запустить локально

```bash
python3 -m http.server 8080
```

Открой: `http://localhost:8080`

## Как передать поток

### Вариант 1: через UI
1. Вставь ссылку в поле **"Ссылка на поток или плейлист"**.
2. Нажми **"Запустить"**.

### Вариант 2: через URL
- `?src=https://example.com/live.m3u8`
- `?file=https://example.com/live.m3u8`
- `?stream=https://example.com/live.m3u8`

Пример:

```text
https://your-domain.com/?src=https%3A%2F%2Fexample.com%2Flive.m3u8
```

## Плейлисты `.m3u` и `.txt`

Для `.m3u` поддерживаются строки `#EXTINF` + URL.

Для `.txt` поддерживаются форматы:
- `https://example.com/stream.m3u8`
- `Название|https://example.com/stream.m3u8`
- `Название,https://example.com/stream.m3u8`

После загрузки список собирается в внутренний playlist PlayerJS и каналы можно переключать прямо в плеере.

## Шифрованные ссылки

1. Введи ссылку на поток.
2. Укажи ключ.
3. Нажми **"Сгенерировать ссылку"**.
4. Получишь ссылку вида: `#enc=...&k=...`.

> Важно: если ключ передаётся в URL (`k`), это обфускация, а не полноценная защита от целевого взлома.

## Деплой

### Netlify
Проект уже содержит `netlify.toml`.

- Build command: не нужен
- Publish directory: `.`

### Vercel
Проект уже содержит `vercel.json`.

- Framework preset: `Other`
- Build command: не нужен
- Output directory: `.`
