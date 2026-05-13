<template>
  <div class="min-h-screen text-white font-sans">
    <!-- NAV -->
    <nav class="fixed top-0 w-full bg-black/30 backdrop-blur z-50">
      <div class="max-w-5xl mx-auto px-6 py-4 flex justify-between items-center">
        <img src="./assets/logo.png" alt="Maurilio Atila" class="w-10 h-10 rounded-full" />
        <div class="flex gap-6 text-sm text-white/80">
          <a href="#about" class="hover:text-white transition">About</a>
          <a href="#experience" class="hover:text-white transition">Experience</a>
          <a href="#skills" class="hover:text-white transition">Skills</a>
          <a href="#contact" class="hover:text-white transition">Contact</a>
        </div>
      </div>
    </nav>

    <!-- HERO -->
    <section class="max-w-5xl mx-auto px-6 pt-36 pb-20 flex flex-col md:flex-row items-center gap-10">
      <img src="./assets/logo.png" alt="Maurilio Atila" class="w-36 h-36 rounded-full shadow-2xl border-4 border-white/20 flex-shrink-0" />
      <div>
        <p class="text-yellow-300 text-sm font-semibold uppercase tracking-widest mb-3">Full Stack Developer & Tech Lead</p>
        <h1 class="text-5xl font-bold leading-tight mb-4">
          Building products<br/>that scale.
        </h1>
        <p class="text-white/70 text-lg max-w-xl mb-8">
          12+ years delivering web, mobile and cloud solutions. Currently based in Madrid.
          Available part-time (4h/day) for freelance projects.
        </p>
        <div class="flex gap-4 flex-wrap">
          <a href="#contact" class="bg-white text-purple-700 font-semibold px-5 py-2.5 rounded-lg text-sm transition hover:bg-yellow-300">Get in touch</a>
          <a href="https://github.com/cabelotaina" target="_blank" rel="noopener" class="border border-white/40 hover:border-white text-white px-5 py-2.5 rounded-lg text-sm font-medium transition">GitHub</a>
          <a href="https://www.linkedin.com/in/maurilio-atila/" target="_blank" rel="noopener" class="border border-white/40 hover:border-white text-white px-5 py-2.5 rounded-lg text-sm font-medium transition">LinkedIn</a>
        </div>
      </div>
    </section>

    <!-- ABOUT -->
    <section id="about" class="max-w-5xl mx-auto px-6 py-16 border-t border-white/10">
      <h2 class="text-2xl font-bold mb-6">About</h2>
      <div class="grid md:grid-cols-2 gap-8 text-white/70 leading-relaxed">
        <p>
          I'm a Brazilian developer living in Madrid with over 12 years of experience across the full stack — from Vue.js and React frontends to Node.js APIs, AWS infrastructure, and native mobile apps.
        </p>
        <p>
          I recently led two international projects for <strong class="text-white">Hoffmann-La Roche</strong> across 26 countries, introduced AI-assisted development to my team, and unblocked a project that had been delayed for over a year. I work best in environments that value autonomy, quality, and delivery.
        </p>
      </div>
      <div class="mt-8 flex flex-wrap gap-3 text-sm">
        <span class="bg-white/10 text-white px-3 py-1 rounded-full">📍 Madrid, Spain</span>
        <span class="bg-white/10 text-white px-3 py-1 rounded-full">🕓 Part-time · 4h/day</span>
        <span class="bg-white/10 text-white px-3 py-1 rounded-full">🌍 PT · EN · ES</span>
        <span class="bg-white/10 text-white px-3 py-1 rounded-full">🔓 Open to remote</span>
      </div>
    </section>

    <!-- EXPERIENCE -->
    <section id="experience" class="max-w-5xl mx-auto px-6 py-16 border-t border-white/10">
      <h2 class="text-2xl font-bold mb-10">Experience</h2>
      <div class="space-y-10">

        <div class="grid md:grid-cols-4 gap-4">
          <div class="text-white/40 text-sm pt-1">Dec 2024 – May 2026</div>
          <div class="md:col-span-3">
            <h3 class="font-semibold text-white text-lg">Project Development Manager & Tech Lead</h3>
            <p class="text-yellow-300 text-sm mb-2">AMURA IT · Madrid, Spain</p>
            <p class="text-white/60 text-sm leading-relaxed mb-3">
              Led delivery of <strong class="text-white">Focusme</strong> and <strong class="text-white">Med Wallet</strong> for Hoffmann-La Roche across 26 countries. Sole tech architect for a team of 6.
            </p>
            <ul class="text-white/60 text-sm space-y-1 list-disc list-inside">
              <li>Unblocked 1-year-delayed Brazil project: Ionic app + AWS ECS API + React frontend + Cognito 2FA</li>
              <li>Introduced AI-assisted development — trained 3 devs, significantly reduced bug rate</li>
              <li>Led 2 major version migrations on Focusme (iOS & Android)</li>
            </ul>
            <div class="flex flex-wrap gap-2 mt-3">
              <span v-for="t in ['React', 'Ionic', 'Android', 'iOS', 'Node.js', 'AWS ECS', 'Cognito', 'TypeScript', 'Salesforce']" :key="t" class="bg-white/10 text-white text-xs px-2 py-0.5 rounded">{{ t }}</span>
            </div>
          </div>
        </div>

        <div class="grid md:grid-cols-4 gap-4">
          <div class="text-white/40 text-sm pt-1">Jan 2021 – Present</div>
          <div class="md:col-span-3">
            <h3 class="font-semibold text-white text-lg">Co-Owner & Full Stack Developer</h3>
            <p class="text-yellow-300 text-sm mb-2">BCompliance&Law · São Paulo, Brazil (Remote)</p>
            <p class="text-white/60 text-sm leading-relaxed">
              Built the entire SaaS suite from scratch: institutional site, client portal, backoffice, and complaint channel. Payment integration (Vindi), CI/CD via GitHub Actions + AWS CloudFormation.
            </p>
            <div class="flex flex-wrap gap-2 mt-3">
              <span v-for="t in ['Vue.js 3', 'Node.js', 'MongoDB', 'PostgreSQL', 'Tailwind', 'AWS', 'GitHub Actions']" :key="t" class="bg-white/10 text-white text-xs px-2 py-0.5 rounded">{{ t }}</span>
            </div>
          </div>
        </div>

        <div class="grid md:grid-cols-4 gap-4">
          <div class="text-white/40 text-sm pt-1">Dec 2023 – Nov 2024</div>
          <div class="md:col-span-3">
            <h3 class="font-semibold text-white text-lg">Android Developer</h3>
            <p class="text-yellow-300 text-sm mb-2">Winche Redes Comerciales · Barcelona, Spain (Remote)</p>
            <p class="text-white/60 text-sm">Lead developer of WincheCloud data platform. UX improvements and test automation.</p>
            <div class="flex flex-wrap gap-2 mt-3">
              <span v-for="t in ['Kotlin', 'Java', 'Python', 'Node.js', 'MySQL']" :key="t" class="bg-white/10 text-white text-xs px-2 py-0.5 rounded">{{ t }}</span>
            </div>
          </div>
        </div>

        <div class="grid md:grid-cols-4 gap-4">
          <div class="text-white/40 text-sm pt-1">May 2019 – Oct 2022</div>
          <div class="md:col-span-3">
            <h3 class="font-semibold text-white text-lg">Mobile Developer</h3>
            <p class="text-yellow-300 text-sm mb-2">Estapar · Remote</p>
            <p class="text-white/60 text-sm">Optimized Google Maps API usage saving ~R$40k/month. Delivered Ecovagas and Estapar Reserva used by millions of users.</p>
            <div class="flex flex-wrap gap-2 mt-3">
              <span v-for="t in ['Ionic', 'Cordova', 'CI/CD']" :key="t" class="bg-white/10 text-white text-xs px-2 py-0.5 rounded">{{ t }}</span>
            </div>
          </div>
        </div>

      </div>
    </section>

    <!-- SKILLS -->
    <section id="skills" class="max-w-5xl mx-auto px-6 py-16 border-t border-white/10">
      <h2 class="text-2xl font-bold mb-8">Skills</h2>
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div v-for="group in skills" :key="group.label" class="bg-white/10 rounded-xl p-5">
          <p class="text-yellow-300 text-xs font-semibold uppercase tracking-wider mb-3">{{ group.label }}</p>
          <div class="flex flex-wrap gap-2">
            <span v-for="s in group.items" :key="s" class="bg-white/10 text-white text-sm px-2.5 py-1 rounded-lg">{{ s }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- CONTACT -->
    <section id="contact" class="max-w-5xl mx-auto px-6 py-16 border-t border-white/10">
      <h2 class="text-2xl font-bold mb-4">Get in touch</h2>
      <p class="text-white/60 mb-8 max-w-lg">Available for part-time freelance projects (up to 4h/day). Remote or Madrid on-site.</p>
      <div class="flex flex-wrap gap-4">
        <a href="mailto:cabelotaina@gmail.com" class="bg-white text-purple-700 font-semibold px-5 py-2.5 rounded-lg text-sm transition hover:bg-yellow-300">cabelotaina@gmail.com</a>
        <a href="https://www.linkedin.com/in/maurilio-atila/" target="_blank" rel="noopener" class="border border-white/40 hover:border-white text-white px-5 py-2.5 rounded-lg text-sm font-medium transition">LinkedIn</a>
        <a href="https://github.com/cabelotaina" target="_blank" rel="noopener" class="border border-white/40 hover:border-white text-white px-5 py-2.5 rounded-lg text-sm font-medium transition">GitHub</a>
      </div>
    </section>

    <footer class="border-t border-white/10 text-center text-white/30 text-sm py-8">
      © 2026 Maurilio Atila
    </footer>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      skills: [
        { label: "Frontend", items: ["Vue.js 2/3", "React", "Angular", "Nuxt", "Tailwind CSS", "HTML5", "SASS"] },
        { label: "Backend", items: ["Node.js", "Express", "REST APIs", "AWS Lambda", "Ruby on Rails", "PHP", "Python"] },
        { label: "Mobile", items: ["Android (Kotlin/Java)", "iOS", "Ionic", "Cordova", "React Native"] },
        { label: "Cloud & DevOps", items: ["AWS ECS", "AWS Lambda", "S3", "Cognito", "CloudFormation", "Docker", "GitHub Actions"] },
        { label: "Databases", items: ["MongoDB", "PostgreSQL", "MySQL"] },
        { label: "Leadership", items: ["Tech Lead", "AI Training", "Agile/Jira", "Code Review", "Remote Teams"] },
      ]
    }
  }
};
</script>

<style>
* { scroll-behavior: smooth; }
body {
  margin: 0;
  background: rgb(3, 128, 57);
  background-image: linear-gradient(135deg, indigo, purple, orange);
  background-attachment: fixed;
}
</style>
