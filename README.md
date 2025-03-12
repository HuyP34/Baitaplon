<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quản Lý Sinh Viên</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
        th { background-color: #f4f4f4; }
        button { margin: 5px; cursor: pointer; }
    </style>
</head>
<body>
    <h2>Quản Lý Sinh Viên</h2>
    <input type="text" id="name" placeholder="Họ và tên">
    <input type="text" id="id" placeholder="Mã số sinh viên">
    <input type="text" id="class" placeholder="Lớp">
    <button onclick="addStudent()">Thêm Sinh Viên</button>
    
    <table>
        <thead>
            <tr>
                <th>Họ và Tên</th>
                <th>Mã Sinh Viên</th>
                <th>Lớp</th>
                <th>Hành Động</th>
            </tr>
        </thead>
        <tbody id="student-list"></tbody>
    </table>

    <script>
        let students = JSON.parse(localStorage.getItem("students")) || [];

        function renderStudents() {
            let table = document.getElementById("student-list");
            table.innerHTML = "";
            students.forEach((student, index) => {
                let row = `<tr>
                    <td>${student.name}</td>
                    <td>${student.id}</td>
                    <td>${student.class}</td>
                    <td>
                        <button onclick="editStudent(${index})">Sửa</button>
                        <button onclick="deleteStudent(${index})">Xóa</button>
                    </td>
                </tr>`;
                table.innerHTML += row;
            });
            localStorage.setItem("students", JSON.stringify(students));
        }

        function addStudent() {
            let name = document.getElementById("name").value;
            let id = document.getElementById("id").value;
            let className = document.getElementById("class").value;
            
            if (name && id && className) {
                students.push({ name, id, class: className });
                renderStudents();
                document.getElementById("name").value = "";
                document.getElementById("id").value = "";
                document.getElementById("class").value = "";
            }
        }

        function deleteStudent(index) {
            students.splice(index, 1);
            renderStudents();
        }

        function editStudent(index) {
            let student = students[index];
            let newName = prompt("Nhập tên mới", student.name);
            let newId = prompt("Nhập mã số mới", student.id);
            let newClass = prompt("Nhập lớp mới", student.class);
            
            if (newName && newId && newClass) {
students[index] = { name: newName, id: newId, class: newClass };
                renderStudents();
            }
        }

        renderStudents();
    </script>
</body>
</html>
