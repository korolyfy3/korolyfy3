<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Онлайн-журнал студентів</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin: 20px; }
        table { width: 100%; border-collapse: collapse; margin-top: 20px; }
        th, td { border: 1px solid #ddd; padding: 10px; text-align: center; }
        th { background-color: #007bff; color: white; }
        input { padding: 5px; }
        button { margin-top: 10px; padding: 8px 12px; }
    </style>
</head>
<body>
    <h1>Онлайн-журнал студентів</h1>
    <input type="text" id="studentName" placeholder="Ім'я студента">
    <button onclick="addStudent()">Додати студента</button>
    <table>
        <thead>
            <tr>
                <th>Студент</th>
                <th>Оцінка</th>
                <th>Дія</th>
            </tr>
        </thead>
        <tbody id="studentTable"></tbody>
    </table>
    <script>
        let students = JSON.parse(localStorage.getItem("students")) || [];
        function renderTable() {
            let table = document.getElementById("studentTable");
            table.innerHTML = "";
            students.forEach((student, index) => {
                table.innerHTML += `<tr>
                    <td>${student.name}</td>
                    <td><input type="number" min="0" max="100" value="${student.grade}" onchange="updateGrade(${index}, this.value)"></td>
                    <td><button onclick="removeStudent(${index})">Видалити</button></td>
                </tr>`;
            });
            localStorage.setItem("students", JSON.stringify(students));
        }
        function addStudent() {
            let name = document.getElementById("studentName").value;
            if (name.trim() !== "") {
                students.push({ name, grade: "" });
                document.getElementById("studentName").value = "";
                renderTable();
            }
        }
        function updateGrade(index, grade) {
            students[index].grade = grade;
            renderTable();
        }
        function removeStudent(index) {
            students.splice(index, 1);
            renderTable();
        }
        renderTable();
    </script>
</body>
</html>
