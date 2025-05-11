<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Привет отметься здесь</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #ccc;
            padding: 10px;
            text-align: center;
        }
        th {
            background-color: #f2f2f2;
        }
        h1 {
            text-align: center; /* Центрирование заголовка */
        }
        .clear-button, .share-button {
            display: block;
            margin: 20px auto; /* Центрирование кнопок */
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>

<h1>Привет отметься здесь.</h1>

<table id="attendanceTable">
    <thead>
        <tr>
            <th>День недели</th>
            <th>Дата</th>
            <th>Отметка</th>
        </tr>
    </thead>
    <tbody>
        <!-- Дни будут добавлены через JavaScript -->
    </tbody>
</table>

<button class="clear-button" id="clearButton">Очистить</button>
<button class="share-button" id="shareButton">Поделиться</button>

<script>
// Функция для добавления дней недели в таблицу
function populateTable() {
    const tableBody = document.getElementById('attendanceTable').getElementsByTagName('tbody')[0];
    
    const daysOfWeek = [
        'Понедельник',
        'Вторник',
        'Среда',
        'Четверг',
        'Пятница',
        'Суббота',
        'Воскресенье'
    ];

    // Очищаем тело таблицы перед добавлением новых строк
    tableBody.innerHTML = '';

    daysOfWeek.forEach(day => {
        const row = tableBody.insertRow();
        
        const cellDay = row.insertCell(0);
        cellDay.textContent = day;

        const cellDate = row.insertCell(1);
        const dateInput = document.createElement('input');
        dateInput.type = 'date';
        
        // Восстановление даты из localStorage
        dateInput.value = localStorage.getItem(day + '_date') || '';
        
        dateInput.addEventListener('change', function() {
            localStorage.setItem(day + '_date', this.value);
        });

        cellDate.appendChild(dateInput);

        const cellCheckbox = row.insertCell(2);
        const checkbox = document.createElement('input');
        checkbox.type = 'checkbox';
        
        // Сохранение состояния чекбокса в localStorage
        checkbox.checked = localStorage.getItem(day + '_checked') === 'true';
        
        checkbox.addEventListener('change', function() {
            localStorage.setItem(day + '_checked', this.checked);
        });

        cellCheckbox.appendChild(checkbox);
    });
}

// Функция для очистки данных и перезаполнения таблицы
function clearData() {
    const daysOfWeek = [
        'Понедельник',
        'Вторник',
        'Среда',
        'Четверг',
        'Пятница',
        'Суббота',
        'Воскресенье'
    ];

    daysOfWeek.forEach(day => {
       localStorage.removeItem(day + '_date');
       localStorage.removeItem(day + '_checked');
    });

    // Перезаполнение таблицы с пустыми значениями
    populateTable();
}

// Функция для получения данных таблицы в виде строки
function getDataString() {
    const tableBody = document.getElementById('attendanceTable').getElementsByTagName('tbody')[0];
    
    let dataToShare = "Данные о посещаемости:\n\n";
    
    for (let row of tableBody.rows) {
      const day = row.cells[0].textContent;
      const date = row.cells[1].querySelector('input').value || "Не указано";
      const checked = row.cells[2].querySelector('input').checked ? "Отметка поставлена" : "Отметка не поставлена";
      
      dataToShare += `${day}: ${date} - ${checked}\n`;
    }

    return dataToShare;
}

// Функция для создания текстового файла и его отправки
async function shareData() {
    const dataToShare = getDataString();
    
    // Создаем Blob из данных
    const blob = new Blob([dataToShare], { type: 'text/plain' });
    
    // Создаем ссылку на файл
    const fileHandle = new File([blob], "attendance.txt", { type: "text/plain" });

   // Используем Web Share API для отправки файла через приложения
   if (navigator.share) {
       try {
           await navigator.share({
               title: 'Данные о посещаемости',
               files: [fileHandle],
           });
           console.log('Успешно поделились!');
       } catch (error) {
           console.error('Ошибка при попытке поделиться:', error);
       }
   } else {
       alert("Ваш браузер не поддерживает функцию обмена.");
       prompt("Скопируйте данные ниже:", dataToShare);
   }
}

// Заполнение таблицы при загрузке страницы
window.onload = populateTable;

// Обработчик события для кнопки "Очистить"
document.getElementById('clearButton').addEventListener('click', clearData);

// Обработчик события для кнопки "Поделиться"
document.getElementById('shareButton').addEventListener('click', shareData);
</script>

</body>
</html>
