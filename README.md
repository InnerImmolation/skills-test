# bidzaar-marketplace

Внутренний маркетплейс скиллов Claude Code для организации **Bidzaar**.

Сотрудники подключают этот репозиторий как marketplace и получают скиллы компании:
бизнес-процессы, онбординг, справочники и (в перспективе) остальные скиллы организации.

## Как устроен репозиторий

```
bidzaar-marketplace/
├── marketplace.json                  <- каталог маркетплейса (реестр плагинов)
├── plugins/
│   └── bidzaar-processy/             <- плагин «Бизнес-процессы»
│       ├── .claude-plugin/plugin.json
│       └── skills/
│           └── bidzaar-processy/
│               ├── SKILL.md          <- сам скилл (инструкции для модели)
│               ├── reestr-processov.md
│               ├── voprosy-vladelcam.md
│               └── references/       <- карточки процессов по департаментам
```

Каждый новый скилл добавляется одним из двух способов:

- **в существующий плагин** — новой папкой в `plugins/<имя>/skills/<скилл>/SKILL.md`;
- **новым плагином** — папка `plugins/<имя>/` + запись в `marketplace.json`.

## Подключение сотрудником

```
claude plugin marketplace add git@github.com:<org>/bidzaar-marketplace.git
claude plugin install "bidzaar-processy@bidzaar-marketplace"
```

Для автораздачи всем сотрудникам маркетплейс и плагин указываются в
`managed-settings.json` (см. документацию managed-settings), тогда руками ничего
вводить не нужно.

## Версионирование и обновления

- Версия каждого плагина — в `plugins/<имя>/.claude-plugin/plugin.json`.
- Релиз делается git-тегом или mergem в защищённую ветку; изменения доезжают до
  сотрудников командой `claude plugin marketplace update` + `claude plugin update`.
- На каждый релиз полезно заводить запись в `CHANGELOG.md` (пока не создан).

## Безопасность

Скиллы — исполняемые инструкции для агента. Репозиторий должен оставаться
приватным, изменения проходят code review, а permissions скиллов ограничиваются
в managed-settings. Не добавляйте сюда плагины из недоверенных источников.

## Ссылки по теме

- Структура маркетплейса и плагинов: https://code.claude.com/docs/en/marketplaces
- Скиллы: https://code.claude.com/docs/en/skills
- Автораздача через managed settings: https://code.claude.com/docs/en/managed-settings
# skills-test
