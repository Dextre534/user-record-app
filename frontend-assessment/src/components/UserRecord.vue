<template>
    <div class="row p-3 shadow mb-3 bg-white rounded p-4">
        <div class="col-2 text-start text-gray">
            {{ date }}
        </div>

        <div class="col-3 text-start">
            {{ name }}
        </div>

        <div class="col-2 text-start text-gray">
            {{ gender }}
        </div>

        <div class="col-2 text-start">
            {{ country }}
        </div>

        <div class="col-3 text-end text-gray">
            {{ email }}
        </div>
    </div>

  </template>
  
  <script>
  export default {
    name: 'UserRecord',
    props: [
        'date',
        'name',
        'gender',
        'country',
        'email',
    ]
  }
  </script>

  