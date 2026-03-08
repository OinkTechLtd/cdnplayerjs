# CDNPlayerJS

Статический плеер на базе `Playerjs` с поддержкой:

- прямых потоков (`.m3u8`, `.mp4`, и т.д.);
- удалённых плейлистов `.m3u` и `.txt`;
- шифрованных ссылок (AES-GCM) с TTL 24 часа.

## Как запустить локально

```bash
python3 -m http.server 8080
```

Открой: `http://localhost:8080`

## Как передать поток

Только через адресную строку:

- `?src=https://example.com/live.m3u8`
- `?file=https://example.com/live.m3u8`
- `?stream=https://example.com/live.m3u8`

Пример:

```text
https://your-domain.com/?src=https%3A%2F%2Fexample.com%2Flive.m3u8
```

Если открыть страницу с `src/file/stream`, приложение автоматически:

1. запускает поток;
2. шифрует ссылку;
3. заменяет URL в адресной строке на `?enc=...`.

Шифрованная ссылка активна 24 часа, после чего становится невалидной для всех.

## Плейлисты `.m3u` и `.txt`

Для `.m3u` поддерживаются строки `#EXTINF` + URL.

Для `.txt` поддерживаются форматы:
- `https://example.com/stream.m3u8`
- `Название|https://example.com/stream.m3u8`
- `Название,https://example.com/stream.m3u8`

После загрузки список собирается во внутренний playlist PlayerJS, каналы можно переключать в плеере.

## Шифрованные ссылки

- Формат: `?enc=...` (опционально `&k=...` для кастомного ключа).
- Алгоритм: AES-GCM.
- Срок жизни токена: 24 часа.

> Важно: ключ в URL (`k`) — это обфускация, а не абсолютная криптографическая защита от целевого взлома.

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
