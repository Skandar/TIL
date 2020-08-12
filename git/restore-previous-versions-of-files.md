# Восстановление предыдущих версий файлов

Во время работы может возникнуть ситуация когда ошибка замечается только через несколько коммитов, после того как она была совершена. В такой ситуации нужно восстановить предыдущие версии файлов в которых были сделаны ошибки не трогая другие файлы и не переключаясь на другие ветки. Этого можно достичь используя команду `checkout` с указанием коммита с которого нужно восстановиться и название одного или нескольких файлов/папок, которые нужно восстановить.

```bash
git checkout 3da1f2 index.html
```

Предыдущие версии файлов окажутся в рабочей директории и сразу попадут в индекс.

Для того чтобы отменить восстановление нужно выполнить команду `checkout` с хешем текущего коммита (или HEAD).

```bash
# Восстановит файлы до версии текущего коммита
git checkout HEAD index.html

# Восстанавливает файлы из индекса
# Подходит в том случае если изменения не были индексированы
git checkout index.html
```

## Ссылки

- [4.6 Скринкаст по Git – Ветки – Восстановление предыдущих версий файлов](https://www.youtube.com/watch?v=_O23vcT7Fno)