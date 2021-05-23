<template>
 
  <form>
    <table>
      <tr>
        <th colspan="2">description</th>
      </tr>
      <tr>
        <td colspan="2">
          <textarea class="form-control" id="exampleFormControlTextarea1" placeholder="Descriptions"></textarea>
        </td>
      </tr>
      <tr>
        <th>Age</th>
        <th>Group</th>
      </tr>
      <tr>
        <td>
          <input type="text" id="example1" class="form-control">
        </td>
        <td>
          <select class="browser-default custom-select">
            <option selected>Group</option>
            <option value="1">Group 1</option>
            <option value="2">Group 2</option>
            <option value="3">Group 3</option>
          </select>
        </td>
      </tr>
      <tr>
        <th>Services</th>
        <th>Gender</th>
      </tr>
      <tr>
        <td>
            <select class="browser-default custom-select">
              <option selected>Services</option>
              <option value="1">One</option>
              <option value="2">Two</option>
              <option value="3">Three</option>
            </select>
        </td>
        <td>
            <select class="browser-default custom-select">
              <option selected>Gender</option>
              <option value="1">One</option>
              <option value="2">Two</option>
              <option value="3">Three</option>
            </select>
        </td>
      </tr>
      <tr>
        <th>Fee</th>
      </tr>
      <tr>
        <td>
            <input type="text" id="example1" class="form-control">
        </td>
      </tr>
    </table>
  </form>
  
</template>
<style>
*{
  margin: 0;
  padding: 0;
}
form{
  background-color:rgb(241, 236, 236);
  padding: 5%;
  box-shadow: 1px 1px 2px;
}
table{
  width: 100%;
}
</style>