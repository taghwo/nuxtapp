<template>
<div>

  <table class="table-condensed">
    <tbody>
      <tr>
      <th>sn</th>
      <th>topic</th>
      <th>client number</th>
      <th>client email</th>
      <th>Date Of Delivery</th>
      <th>Delivery Type</th>
    </tr>
    <tr>
      <td>{{id}}</td>
      <td>{{topic}}</td>
      <td>{{client_phone_number}}</td>
      <td>{{client_email}}</td>
      <td>{{date_of_delivery}}</td>
      <td>{{time_of_delivery}}</td>
    </tr>
    </tbody>
    <tfoot>
    </tfoot>
    
  </table>
</div>
</template>

<script>
export default {
name: "allurgentorder",
props:['id','topic','client_phone_number','client_email','date_of_delivery','time_of_delivery']
}
</script>

<style>

</style>
