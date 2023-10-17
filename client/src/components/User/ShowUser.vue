<template> 
  <div> 
  <h1>Show User</h1> 
  <p>id: {{ user.id }}</p> 
  <p>ชือ-นามสกุล: {{ user.name }} - {{ user.lastname }}</p> 
  <p>email: {{ user.email }}</p> 
  <p>password: {{ user.password }}</p>   
  </div> 
</template> 
<script> 
import UsersService from '@/services/UsersService' 
 
export default { 
  data () { 
    return { 
      user:  []  
    } 
  }, 
  async created () { 
    let userId = this.$route.params.userId 
    this.user = (await UsersService.show(userId)).data 
  } 
} 
</script> 
<style scoped> 
</style> 