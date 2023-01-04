<template>
  <div class="max-w-3xl pl-2">
    <div class="mb-3">
      <h1 class="text-4xl text-white">{{ msg }}</h1>
      <h2 class="text-gray-300">
        Software Engineer

        <a
          class="px-1"
          href="https://www.linkedin.com/in/maurilio-atila/"
          target="_blank"
          rel="noopener"
          >Linkedin</a
        >
        <a
          class="px-1"
          href="https://github.com/cabelotaina/"
          target="_blank"
          rel="noopener"
          >Github</a
        >
      </h2>
    </div>
    <div class="lg:flex mb-10">
      <div class="lg:pr-2 text-white lg:text-gray-400">
        <p class="py-2">
          I have over 7 years of experience in the technology industry, with a
          focus on web and mobile development. I have a strong background in
          continuous integration and continuous delivery (CI/CD) and have
          utilized a variety of technologies such as Vue.js, Node.js, and Ionic
          Framework in my projects.
        </p>
        <p class="py-2">
          I have worked on a number of successful initiatives, including
          automating the creation of accounts, improving the UI and UX of
          interfaces for millions of users, and implementing CI/CD algorithms to
          automate the deployment process. I have also made contributions to
          open-source projects, including the Delibera plugin and Rede Livre,
          and have integrated Delibera with the open-source social network,
          Noosfero.
        </p>
      </div>
      <div class="lg:pl-2 text-white lg:text-gray-400">
        <p class="py-2">
          In my most recent role as Co-Owner at BCompliance&Law, I have
          leveraged my expertise in web development and AWS cloud formation to
          create a scalable infrastructure. I have also utilized my skills in
          git, HTML, CSS, and JavaScript to drive real-time improvements through
          a CI/CD process automation using GitHub actions and git flow.
        </p>
        <p class="py-2">
          I am a skilled and motivated professional with a passion for
          technology and a track record of delivering successful projects. I am
          confident in my ability to make a positive impact in any organization
          and am always eager to learn and grow as a full stack engineer.
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    msg: String,
  },
};
</script>
