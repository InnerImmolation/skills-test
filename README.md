# bidzaar-marketplace

Внутренний маркетплейс скиллов организации **Bidzaar** для Claude Desktop и Claude Code.

Сотрудники подключают этот репозиторий как marketplace и получают скиллы компании:
бизнес-процессы, онбординг, справочники и (в перспективе) остальные скиллы организации.

## Как устроен репозиторий

Плагины лежат в корне репозитория — по одному каталогу на плагин (формат Anthropic):

```
skills-test/
├── marketplace.json                  <- каталог маркетплейса (реестр плагинов)
├── README.md
└── bidzaar-processy/                 <- плагин «Бизнес-процессы»
    ├── .claude-plugin/plugin.json
    └── skills/
        └── bidzaar-processy/
            ├── SKILL.md              <- сам скилл (инструкции для модели)
            ├── reestr-processov.md
            ├── voprosy-vladelcam.md
            └── references/           <- карточки процессов по департаментам
```

Каждый новый скилл добавляется одним из двух способов:

- **в существующий плагин** — новой папкой в `<имя>/skills/<скилл>/SKILL.md`;
- **новым плагином** — каталог `<имя>/` в корне репо + запись в `marketplace.json`.

## Подключение

**В Claude Desktop:** Settings → Plugins / Integrations → Add marketplace —
указать путь к репозиторию (локальный путь или URL). После добавления в магазине
появятся плагины; плагин нужно установить, и его скиллы станут доступны.

**В Claude Code (CLI):**

```
claude plugin marketplace add git@github.com:<org>/bidzaar-marketplace.git
claude plugin install "bidzaar-processy@bidzaar-marketplace"
```

## Версионирование и обновления

- Версия каждого плагина — в `<имя>/.claude-plugin/plugin.json`.
- Релиз делается git-тегом или merge в защищённую ветку; изменения доезжают до
  пользователей повторным обновлением магазина/плагина в приложении либо командами
  `claude plugin marketplace update` + `claude plugin update` в CLI.

## Безопасность

Скиллы — исполняемые инструкции для агента. Репозиторий должен оставаться приватным,
изменения проходят code review. Не добавляйте сюда плагины из недоверенных источников.

## Ссылки по теме

- Структура маркетплейсов и плагинов: https://code.claude.com/docs/en/marketplaces
- Скиллы: https://code.claude.com/docs/en/skills
