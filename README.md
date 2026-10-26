# ai-expert-agent-skills

Открытые Agent Skills для экспертов [ai-expert.pro](https://ai-expert.pro).

## Установка

```bash
npx -y skills add Evgenydokukin/ai-expert-agent-skills
```

Команда подходит для Codex и Claude Code. Повторный запуск обновляет установленный
навык.

Перед работой подключите MCP кабинета эксперта. Claude Code:

```bash
claude mcp add ai-expert --transport http https://dd-ru.ai-expert.pro/api/mcp/contractor
```

Затем запустите `claude`, введите `/mcp`, выберите `ai-expert` и нажмите Authenticate —
откроется браузер для входа. Codex:

```bash
codex mcp add ai-expert --url https://dd-ru.ai-expert.pro/api/mcp/contractor
codex mcp login ai-expert
```

После входа используйте `create-ai-expert-case`, чтобы создать или улучшить
собственный кейс из явно выбранных локальных материалов. Исходные файлы остаются
локально; в кабинет уходят только итоговый текст кейса и выбранные изображения.
