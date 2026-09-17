## ИСХОДНЫЙ КОД ПРОГРАММ

### 1. Программа генерации таблицы дней года:

```javascript
function daysInMonth(month) {
    return 32 - new Date(2023, month, 32).getDate();
}

function generateTable() {
    const months = [31, 28, 31, 30, 31, 30, 
                    31, 31, 30, 31, 30, 31];
    const monthNames = ['Янв', 'Фев', 'Мар', 'Апр', 
                        'Май', 'Июн', 'Июл', 'Авг', 
                        'Сен', 'Окт', 'Ноя', 'Дек'];
    const cumulativeDays = [0, 31, 59, 90, 120, 151, 
                            181, 212, 243, 273, 304, 334];
    
    let table = '<table><thead><tr><th>№</th>';
    monthNames.forEach(name => {
        table += '<th>' + name + '</th>';
    });
    table += '</tr></thead><tbody>';
    
    for (let day = 1; day <= 31; day++) {
        table += '<tr><td>' + day + '</td>';
        for (let month = 0; month < 12; month++) {
            if (day <= months[month]) {
                const dayNumber = cumulativeDays[month] + day;
                table += '<td>' + dayNumber + '</td>';
            } else {
                table += '<td>—</td>';
            }
        }
        table += '</tr>';
    }
    
    table += '</tbody></table>';
    document.getElementById('tableContainer').innerHTML = table;
}
```

---

### 2. Программа расчёта кредита:

```javascript
function calculateCredit() {
    const P = parseFloat(document.getElementById('calc-p').value);
    const i = parseFloat(document.getElementById('calc-i').value) / 100;
    const days = parseInt(document.getElementById('calc-days').value);
    const practice = document.getElementById('calc-practice').value;
    const type = document.getElementById('calc-type').value;
    
    if (isNaN(P) || isNaN(i) || isNaN(days) || 
        P < 0 || i < 0 || days < 30) {
        document.getElementById('calc-result').innerHTML = 
            '<span style="color:#ff6b6b;">Ошибка!</span>';
        return;
    }
    
    let n;
    if (practice === 'german' || practice === 'french') {
        n = days / 360;
    } else {
        n = days / 365;
    }
    
    let S;
    if (type === 'simple') {
        S = P * (1 + n * i);
    } else {
        S = P * Math.pow((1 + i), n);
    }
    
    document.getElementById('calc-result').innerHTML = 
        'S = ' + S.toFixed(2) + ' руб.';
}
```