# 🔴 ВАЖНО / IMPORTANT

> **🔴 ВАЖНО**  
> Для корректной работы этого skill рекомендуется использовать аудит-модуль:  
> [`nidox-vpn-detection-defense-skill`](https://github.com/JonesPitkin/nidox-vpn-detection-defense-skill)
>
> Без него проверка конфигураций, маршрутизации, CDN, DNS и VPN-детекта может быть неполной.
>
> **🔴 IMPORTANT**  
> For proper operation of this skill it is strongly recommended to use:  
> [`nidox-vpn-detection-defense-skill`](https://github.com/JonesPitkin/nidox-vpn-detection-defense-skill)
>
> Without it, validation of VPN configurations, routing, CDN, DNS and detection-resistance settings may be incomplete.

# 3X-UI Skills

Набор автономных Skills для Codex по установке, inbounds, маршрутизации, безопасности и интеграции [3X-UI](https://github.com/MHSanaei/3x-ui) с Cloudflare.

Проект не является частью официального 3X-UI. Материалы основаны на официальном репозитории и Wiki 3X-UI, исходном коде панели, документации Xray-core и официальной документации связанных upstream-проектов.

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

Каждый `SKILL.md` ссылается только на собственные references, поэтому Skill можно устанавливать отдельно.

## Проверка

Запускать официальный валидатор `skill-creator` для каждого каталога:

```sh
python3 /path/to/skill-creator/scripts/quick_validate.py 3x-ui-install
python3 /path/to/skill-creator/scripts/quick_validate.py 3x-ui-inbounds
python3 /path/to/skill-creator/scripts/quick_validate.py 3x-ui-routing
python3 /path/to/skill-creator/scripts/quick_validate.py 3x-ui-security
python3 /path/to/skill-creator/scripts/quick_validate.py 3x-ui-cloudflare
```

Перед публикацией также проверить локальные Markdown-ссылки, внешние источники, отсутствие секретов и наличие `SKILL.md`, `agents/openai.yaml`, непустой `references/` в каждом Skill.

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
- выпускать release только после успешной валидации всех пяти Skills.
