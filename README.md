import React, { useState } from "react";

export default function EmployeeTable() {
  const [employees, setEmployees] = useState([
    { name: "Alice", department: "HR", salary: 50000 },
    { name: "Bob", department: "Engineering", salary: 75000 },
    { name: "Charlie", department: "Marketing", salary: 60000 },
    { name: "David", department: "Finance", salary: 65000 },
    { name: "Eve", department: "Engineering", salary: 72000 },
  ]);

  const [sortConfig, setSortConfig] = useState({ key: null, direction: "asc" });

  const sortData = (key) => {
    let direction = "asc";
    if (sortConfig.key === key && sortConfig.direction === "asc") {
      direction = "desc";
    }
    const sorted = [...employees].sort((a, b) => {
      if (a[key] < b[key]) return direction === "asc" ? -1 : 1;
      if (a[key] > b[key]) return direction === "asc" ? 1 : -1;
      return 0;
    });
    setEmployees(sorted);
    setSortConfig({ key, direction });
  };

  return (
    <div style={{ padding: "20px" }}>
      <h2>Employee Data</h2>
      <table style={{ borderCollapse: "collapse", width: "100%" }}>
        <thead>
          <tr>
            <th onClick={() => sortData("name")} style={styles.header}>
              Name {sortConfig.key === "name" ? (sortConfig.direction === "asc" ? "▲" : "▼") : ""}
            </th>
            <th onClick={() => sortData("department")} style={styles.header}>
              Department {sortConfig.key === "department" ? (sortConfig.direction === "asc" ? "▲" : "▼") : ""}
            </th>
            <th onClick={() => sortData("salary")} style={styles.header}>
              Salary {sortConfig.key === "salary" ? (sortConfig.direction === "asc" ? "▲" : "▼") : ""}
            </th>
          </tr>
        </thead>
        <tbody>
          {employees.map((emp, index) => (
            <tr
              key={index}
              style={{
                backgroundColor: index % 2 === 0 ? "#f9f9f9" : "#ffffff",
                cursor: "pointer",
              }}
            >
              <td style={styles.cell}>{emp.name}</td>
              <td style={styles.cell}>{emp.department}</td>
              <td style={styles.cell}>{emp.salary}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}

const styles = {
  header: {
    border: "1px solid #ddd",
    padding: "10px",
    backgroundColor: "#f2f2f2",
    cursor: "pointer",
    userSelect: "none",
  },
  cell: {
    border: "1px solid #ddd",
    padding: "10px",
  },
};
