# ai-expert-agent-skills

Открытые Agent Skills для подрядчиков [ai-expert.pro](https://ai-expert.pro).

## Установка

```bash
npx -y skills add Evgenydokukin/ai-expert-agent-skills
```

Команда подходит для Codex и Claude Code. Повторный запуск обновляет установленный
скилл.

Перед работой подключите contractor MCP:

```bash
claude mcp add ai-expert --transport http https://dd.ai-expert.pro/api/mcp/contractor
```

После OAuth-авторизации используйте `create-ai-expert-case`, чтобы создать или улучшить
собственный кейс из явно выбранных локальных материалов. Исходные файлы остаются
локально; в GD отправляется только итоговая карточка и выбранные изображения.
