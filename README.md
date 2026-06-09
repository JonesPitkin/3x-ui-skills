# 3x-ui-skills

`3x-ui-skills` — самостоятельный репозиторий Codex skills для установки, настройки, маршрутизации, безопасности и Cloudflare-интеграции `3x-ui`.

Этот репозиторий может использоваться отдельно, без обязательной привязки к мета-репозиторию `nidox-vpn-skills`.

## Статус репозитория

Репозиторий остаётся самостоятельным набором skills. Он не требует обязательного аудита через `nidox-vpn-detection-defense-skill`, если используется сам по себе.

Обязательный аудит нужен только в одном сценарии: если конкретный skill из этого репозитория копируется, включается или используется внутри `nidox-vpn-skills`, где действует отдельная политика аудита.

## Skills

| Skill | Назначение |
|---|---|
| [`3x-ui-install`](3x-ui-install/SKILL.md) | Ubuntu/Debian, VPS/LXC, Docker/systemd, обновление, миграция, backup и диагностика |
| [`3x-ui-inbounds`](3x-ui-inbounds/SKILL.md) | Inbounds, transports, REALITY/Vision/Hysteria2 и совместимость клиентов |
| [`3x-ui-routing`](3x-ui-routing/SKILL.md) | Xray routing/DNS, geosite/geoip, direct/proxy/block, split tunneling и balancers |
| [`3x-ui-security`](3x-ui-security/SKILL.md) | Panel hardening, credentials/2FA, TLS, firewall, Fail2Ban, SSH и защита backups |
| [`3x-ui-cloudflare`](3x-ui-cloudflare/SKILL.md) | Cloudflare DNS/Proxy/CDN, TLS modes, WS/gRPC, Origin Rules, certificates и Tunnel |

## Структура

```text
3x-ui-skills/
├── README.md
├── 3x-ui-install/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
├── 3x-ui-inbounds/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
├── 3x-ui-routing/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
├── 3x-ui-security/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
└── 3x-ui-cloudflare/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
```

## Карта знаний

### `3x-ui-install`

`install.md`, `update.md`, `backup.md`, `security.md`, `troubleshooting.md`.

### `3x-ui-inbounds`

- Protocols: VLESS, VMess, Trojan, Shadowsocks, Hysteria2.
- Other inbounds: WireGuard, HTTP/Mixed, Tunnel, TUN.
- Security/transports: REALITY, Vision, TCP, mKCP, WS, gRPC, HTTPUpgrade, XHTTP/SplitHTTP.
- Выбор и совместимость: `comparison.md`, `clients.md`, `troubleshooting.md`.

### `3x-ui-routing`

- `routing.md`, `rules.md` — модель Xray, `domainStrategy`, порядок и поля rules.
- `dns.md` — Xray DNS, fallback/cache и граница с DNS Podkop.
- `geosite.md`, `geoip.md` — встроенные и дополнительные `.dat`.
- `direct-proxy-block.md` — server-side split tunneling.
- `balancer.md`, `troubleshooting.md` — стратегии и диагностика.

### `3x-ui-security`

- `panel-security.md`, `credentials.md`, `tls.md`.
- `firewall.md`, `fail2ban.md`, `ssh-hardening.md`.
- `backups-security.md`, `troubleshooting.md`.

### `3x-ui-cloudflare`

- Архитектура/DNS/CDN: `overview.md`, `dns.md`, `proxy-cdn.md`.
- TLS/origin: `tls-modes.md`, `certificates.md`, `origin-rules.md`.
- Transports/access: `websockets.md`, `grpc.md`, `tunnel.md`.
- Ошибки 522/525/526: `troubleshooting.md`.

## Границы ответственности

- `3x-ui-install` отвечает за жизненный цикл deployment; углубленный hardening находится в `3x-ui-security`.
- `3x-ui-inbounds` отвечает за protocol/transport; Cloudflare-specific edge/origin настройки находятся в `3x-ui-cloudflare`.
- `3x-ui-routing` описывает server-side Xray policy. Client-side sing-box/Podkop routing настраивается отдельно.
- `3x-ui-cloudflare` не рассматривает standard CDN как arbitrary TCP/UDP proxy: REALITY/raw TCP/Hysteria2 требуют DNS-only/direct либо отдельного поддерживаемого продукта.

Каждый `SKILL.md` ссылается только на собственные references, поэтому skill можно устанавливать отдельно.

## Связь с nidox-vpn-skills

Если материалы из `3x-ui-skills` используются внутри `nidox-vpn-skills`, они попадают под политику обязательного аудита, описанную в мета-репозитории. Вне этого сценария репозиторий остаётся автономным.

## Проверка

Запускать официальный валидатор `skill-creator` для каждого каталога:

```sh
python3 /path/to/skill-creator/scripts/quick_validate.py 3x-ui-install
python3 /path/to/skill-creator/scripts/quick_validate.py 3x-ui-inbounds
python3 /path/to/skill-creator/scripts/quick_validate.py 3x-ui-routing
python3 /path/to/skill-creator/scripts/quick_validate.py 3x-ui-security
python3 /path/to/skill-creator/scripts/quick_validate.py 3x-ui-cloudflare
```

Перед публикацией также проверить локальные Markdown-ссылки, внешние источники, отсутствие секретов и наличие `SKILL.md`, `agents/openai.yaml`, непустой `references/` в каждом skill.

## Актуальность

Последний аудит выполнен 7 июня 2026 года:

- 3X-UI release `v3.2.8` от 5 июня 2026 года;
- repository commit `483952cfa0333a051f78c3aedf37f4c25945042a` от 6 июня 2026 года;
- Wiki commit `264a7b202aacc0036a1fbb95a285d3e2981a3578` от 3 июня 2026 года;
- bundled Xray-core commit `94ffd50060f1`.

## Перед первой публикацией

- выбрать лицензию;
- повторно проверить изменяемые Cloudflare/Xray limits;
- проверить историю Git на отсутствие секретов после инициализации;
- выпускать release только после успешной валидации всех пяти skills.
