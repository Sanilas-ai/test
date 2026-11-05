# test

Публичная песочница Sanilas для экспериментов с
[toolchain-verify](https://github.com/Sanilas-ai/toolchain-verify) и GitHub Actions.
Здесь нет продуктового кода — только манифест, workflow и то, что пробуется.

*Sanilas's public sandbox for trying out [toolchain-verify](https://github.com/Sanilas-ai/toolchain-verify)
and CI experiments. No product code here.*

## Что здесь / What's here

| Файл / File | Зачем / Purpose |
|---|---|
| [`toolchain.toml`](toolchain.toml) | Манифест: go, git, python3 (обязательные), node (optional) для `ubuntu-latest` (`require_container = false`). |
| [`.github/workflows/toolchain.yml`](.github/workflows/toolchain.yml) | Ставит toolchain-verify через `go install`, запускает `check -v` и `pin --dry-run`. |

## Локально / Locally

```bash
go install github.com/Sanilas-ai/toolchain-verify/cmd/toolchain-verify@latest
toolchain-verify check -m toolchain.toml -v        # exit 0 = всё совпало / all good
toolchain-verify pin -m toolchain.toml --dry-run   # что записал бы pin / what pin would record
```

Внутри контейнера (например, OSS-песочницы) поменяйте `require_container` на `true`
или уберите строку — иначе `check` честно упадёт с «manifest requires running on the host».

*Inside a container set `require_container = true` (or drop the line); otherwise `check`
fails by design.*

## Лицензия / License

[Apache-2.0](LICENSE), как и у toolchain-verify.
