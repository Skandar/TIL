# Commit

При коммите можно указать некоторый свойства предстоящего коммита:

- `--author="..."` - указывает автора коммита.

  ```bash
  git commit --author='Developer <developer@email.com>'
  ```

- `--date="..."` - указать дату коммита.

  ```bash
  git commit --date='20.01.1990'
  ```

- `--all` (`-a`) - закоммитить все изменения, без добавления их в индекс. Игнорируются неотлеживаемые файлы.

  ```bash
  git commit -a
  ```

Если нужно быстро закоммитить 1 или несколько файлов, то иногда быстрее использовать команду `commit` с путями к папкам/файлам, которые нужно закоммитить.

```bash
git commit -m 'Add file' file.txt
```

## Ссылки

- [3.1 Скринкаст по Git – Основы – Создание репозитория, первый коммит](https://youtu.be/KqsWpHq6SPk)
- [3.5 Скринкаст по Git – Основы – Коммиты без git add](https://www.youtube.com/watch?v=_jHQl1ZqXt0&list=PLDyvV36pndZHkDRik6kKF6gSb0N0W995h&index=18)
