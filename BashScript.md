## Основы Bash CLI
**bash** - командная строка, консоль. Ещё **Bash**- это скриптовый ЯП

#!/bin/bash
# Спрашиваем имя и здороваемся
# read
# echo
echo "Как вас зовут?"
read name
echo "Привет, $name!"

#!/bin/bash
# Сумма двух чисел
# Арифметика в Bash
read -p "Введите первое число: " a
read -p "Введите второе число: " b
sum=$((a + b))
echo "Сумма: $sum"

#!/bin/bash
# Проверка числа на чётность
# test
read -p "Введите число: " num

if [ $((num % 2)) -eq 0 ]; then
    echo "Число $num чётное"
else
    echo "Число $num нечётное"
fi

#!/bin/bash
# Создаём папки для веб-проекта
# mkdir
# touch
# ls
mkdir -p myproject/css
mkdir -p myproject/js
mkdir -p myproject/img
touch myproject/index.html
echo "Структура проекта создана:"
ls -R myproject

#!/bin/bash
# Считаем строки в файле
# wc
read -p "Введите имя файла: " filename

if [ -f "$filename" ]; then
    lines=$(wc -l < "$filename")
    echo "В файле '$filename' строк: $lines"
else
    echo "Файл '$filename' не найден"
fi

#!/bin/bash
# Генератор пароля из 8 символов
# tr           html
# head
# /dev/urandom
password=$(tr -dc 'A-Za-z0-9' < /dev/urandom | head -c 8)
echo "Ваш пароль: $password"

#!/bin/bash
# Поиск файлов по расширению в текущей папке
# Glob / Wildcards
read -p "Введите расширение (например txt): " ext

echo "Найденные файлы:"
ls *.$ext 2>/dev/null

if [ $? -ne 0 ]; then
    echo "Файлов с расширением .$ext нет"
fi


#!/bin/bash
# Статистика репозитория GitHub (нужен curl)
# Запуск: bash 8.sh tensorflow/tensorflow
# curl
# grep
# GitHub API

repo=$1

if [ -z "$repo" ]; then
    echo "Укажите репозиторий, например: bash 8.sh torvalds/linux"
    exit 1
fi

data=$

if [ -z "$data" ]; then
    echo "Нет интернета"
    exit 1
fi

if echo "$data" | grep -q '"message": "Not Found"'; then
    echo "Репозиторий $repo не найден"
    exit 1
fi

if echo "$data" | grep -q "rate limit"; then
    echo "Превышен лимит запросов, попробуйте позже"
    exit 1
fi

stars=$(echo "$data" | grep -m1 '"stargazers_count"' | tr -dc '0-9')
forks=$(echo "$data" | grep -m1 '"forks_count"' | tr -dc '0-9')
issues=$(echo "$data" | grep -m1 '"open_issues_count"' | tr -dc '0-9')

YELLOW='\033[33m'
GREEN='\033[32m'
RED='\033[31m'
NC='\033[0m'

echo "Репозиторий: $repo"
echo -e "Звёзды: ${YELLOW}$stars${NC}"
echo -e "Форки: ${GREEN}$forks${NC}"

if [ "$issues" -gt 100 ]; then
    echo -e "Issues: ${RED}$issues${NC}"
else
    echo -e "Issues: ${YELLOW}$issues${NC}"
fi




