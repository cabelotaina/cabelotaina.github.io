<template>
  <div class="max-w-lg">
    <h1 class="text-4xl">{{ msg }}</h1>
    <p class="py-2">
      My Name is Maurílio Atila, I'm computer scientist, I work mainly with JS.
      I like to build web applications with NodeJS, VueJS and MongoDB.
      I'm working also with React Native, Android and iOS to build mobile apps.
      I know how to build API's with Node and Express, but I can manage to build with Rails and Python too.
      I have strong habilities with AWS services.
    </p>
    <h3 class="text-lg">Follow me</h3>
    <ul>
      <li><a href="https://www.linkedin.com/in/maurilio-atila/" target="_blank" rel="noopener">Linkedin</a></li>
      <li><a href="https://github.com/cabelotaina/" target="_blank" rel="noopener">Github</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>
