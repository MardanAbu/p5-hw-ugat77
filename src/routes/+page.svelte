<script>
  let employees = [
    { id: 1, name: "Jack", gender: "Male", salary: 50000 },
    { id: 2, name: "Rose", gender: "Female", salary: 60000 },
  ];

  let newName = "";
  let newGender = "";
  let newSalary = "";

  function addEmployee() {
    if (!newName || !newGender || !newSalary || isNaN(newSalary) || newSalary.length > 6) {
      alert("Please enter valid information.");
      return;
    }

    const salary = parseFloat(newSalary);
    const newEmployee = { id: employees.length + 1, name: newName, gender: newGender, salary };
    employees = [...employees, newEmployee];

    //clear feilds
    newName = "";
    newGender = "";
    newSalary = "";
  }

  function removeEmployee(id) {
    employees = employees.filter((employee) => employee.id !== id);
  }
</script>

<style>
  
</style>

<main>
  <h1>Employee Management System</h1>

  <h2>Employee List</h2>
  <table>
    <thead>
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Gender</th>
        <th>Salary</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody>
      {#each employees as { id, name, gender, salary }}
        <tr>
          <td>{id}</td>
          <td>{name}</td>
          <td>{gender}</td>
          <td>${salary.toFixed(2)}</td>
          <td><button on:click={() => removeEmployee(id)}>Remove</button></td>
        </tr>
      {/each}
    </tbody>
  </table>

  <h2>Add Employee</h2>
  <form on:submit|preventDefault={addEmployee}>
    <label for="name">Name:</label>
    <input type="text" id="name" bind:value={newName} required>

    <label for="gender">Gender:</label>
    <select id="gender" bind:value={newGender} required>
      <option value="">Select gender</option>
      <option value="Male">Male</option>
      <option value="Female">Female</option>
    </select>

    <label for="salary">Salary:</label>
    <input type="text" id="salary" bind:value={newSalary} pattern="\d+(\.\d{1,2})?" required>
    
    <button type="submit">Add Employee</button>
  </form>
</main>