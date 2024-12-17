# Отчет по лабораторной работе: Основы работы с Git
## Цель работы:  
освоить основные команды Git
## Задание 1 - Автоматизация проверки формата файлов при коммите
в директории ``` .git/hooks/ ``` создаю новый файл ``` pre-commit ``` и начинаю его редактирование:

![image](https://github.com/user-attachments/assets/63cf573e-df85-4988-a57d-602b7398b774)

наполняю его следующим кодом:
```bash
#!/bin/bash

# Устанавливаем права на исполнение
chmod +x "$0"

# Проверка, что есть хотя бы один .txt файл в staging area
txt_files=$(git diff --cached --name-only --diff-filter=ACM | grep '\.txt$')
if [ -z "$txt_files" ]; then
  echo "No .txt files found in the commit. Continuing..."
  exit 0 #Выход с кодом 0, т.к. ошибка отсутствия файлов не критична.
fi

# Проверка каждого .txt файла на наличие не-пробельных символов
for file in $txt_files; do
  if ! grep -q '[^[:space:]]' "$file"; then
    echo "Error: File '$file' is empty or contains only whitespace. Commit aborted." >&2
    exit 1
  fi
done

echo "All .txt files are valid. Commit proceeding..."
exit 0
```

пытаюсь создать "плохие" файлы и получаю нужный ответ:

![image](https://github.com/user-attachments/assets/932f15ac-d5b1-43f7-8b15-c5e417d982d5)

очищаю staging area, чтобы Git не выдавал ошибку старых файлов перед коммитом новых и добавляю "правильный" файл:

![image](https://github.com/user-attachments/assets/8cbfca04-3175-4d9d-873f-a12f84fa2f10)

все прошло успешно
