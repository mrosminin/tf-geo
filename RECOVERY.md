# Восстановление tf-geo v1.0.5

Этот `dev` основан на GitHub `mrosminin/tf-geo` `master` (`231aee6d5ca2b4463e18407bbbc2f60c917ed93b`) и локально восстановлен из Go module proxy архива версии `v1.0.5`. Источник архива сообщает GitLab tag commit `abccaf824c565868a532da63d378691778604c14`, ref `refs/tags/v1.0.5`, время `2026-03-26T08:58:12Z`.

Архив: `cloud-dev-recovery/dependencies/go-proxy/git.transflow.ru/go-libs/tf-geo/@v/v1.0.5.zip`; SHA-256 `1bb063b0c9a2f1136b731094df44c356d298b1e3c0e0a031b0ee8a331492ed11`; Go module checksum `h1:OxkqBbOe1KZH18SYt8KgSUz9cbDZY/FiOYZJUaMyPSw=`. Все 151 файлов версии `v1.0.5` сохранены, включая LICENSE, README и тесты. Module path оставлен `git.transflow.ru/go-libs/tf-geo`, как ожидает backend.

Сравнение с GitHub tag `v1.0.4` (`231aee6d5ca2b4463e18407bbbc2f60c917ed93b`): 82 Go-файла отличаются только заменой import path с `github.com/mrosminin/tf-geo` на `git.transflow.ru/go-libs/tf-geo`; прочие Go-исходники совпадают. В `go.mod` удалена зависимость `golang.org/x/exp`; runtime пакет не имеет внешних зависимостей.

Аудит архива не обнаружил private-key markers, URL credentials, `.env`/`.npmrc`; один keyword match в `s2/cellid_test.go` — обычный тестовый fixture. Публичные ссылки относятся к S2 документации, upstream и лицензии.

Тесты запускаются отдельно, но не являются обязательной CI-проверкой этой миграции: полный `go test -p 1 ./...` сообщил `s2/TestSliceDivided` (`s2/chain_interpolation_query_test.go:833`) и `s2/TestCellDistanceToEdge` (`s2/cell_test.go:676`). На публичном baseline `v1.0.4` также падал `TestSliceDivided`; `TestCellDistanceToEdge`, повторённый отдельно пять раз для обеих версий, прошёл. Ошибки не исправлялись, тесты не исключались. `go build -mod=readonly -p 1 ./...` прошёл; полный тестовый baseline требует отдельного решения.
