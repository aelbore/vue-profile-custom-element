<template>
  <div>
    <md-table>
      <md-table-row>
        <md-table-head md-numeric>ID</md-table-head>
        <md-table-head>Name</md-table-head>
        <md-table-head>Profession</md-table-head>
        <md-table-head>Motto</md-table-head>
        <md-table-head>Actions</md-table-head>
      </md-table-row>

      <md-table-row v-for="(profile, index) in profiles" v-bind:key="index">
        <md-table-cell md-numeric>{{ profile.id }}</md-table-cell>
        <md-table-cell>{{ profile.name }}</md-table-cell>
        <md-table-cell>{{ profile.profession }}</md-table-cell>
        <md-table-cell>{{ profile.motto }}</md-table-cell>
        <md-table-cell>
          <md-button class="md-icon-button md-raised">
            <md-icon>library_books</md-icon>
          </md-button>
        </md-table-cell>
      </md-table-row>
    </md-table>

    <MdTablePagination  mdPageSize="3"/>
  </div>
</template>

<script>
  export default {
    name: 'Search',
    props: ['profiles'],
  }
</script>


<style scoped>
.md-table-row:hover:not(.md-header-row) .md-table-cell{
  background: unset!important;
}
</style>
