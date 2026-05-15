<template>
  <div class="min-h-screen font-sans bg-black text-zinc-200">

    <!-- SKELETON OVERLAY -->
    <transition name="fade">
      <div v-if="loading" class="fixed inset-0 bg-black z-[100] px-8 pt-40 pb-28">
        <div class="max-w-6xl mx-auto">
          <div class="flex flex-col md:flex-row md:items-end gap-12">
            <div class="flex-1 space-y-6">
              <div class="skeleton h-3 w-48 rounded"></div>
              <div class="space-y-4">
                <div class="skeleton h-16 w-64 rounded"></div>
                <div class="skeleton h-16 w-80 rounded"></div>
                <div class="skeleton h-16 w-56 rounded"></div>
              </div>
              <div class="space-y-2">
                <div class="skeleton h-4 w-96 rounded"></div>
                <div class="skeleton h-4 w-72 rounded"></div>
              </div>
            </div>
            <div class="flex flex-col items-end gap-6">
              <div class="skeleton w-28 h-28 rounded-2xl"></div>
              <div class="skeleton h-3 w-32 rounded"></div>
            </div>
          </div>
        </div>
      </div>
    </transition>

    <!-- NAV -->
    <nav class="fixed top-0 w-full z-50 bg-black/98 backdrop-blur-sm border-b border-zinc-900">
      <div class="max-w-6xl mx-auto px-8 py-5 flex justify-between items-center">
        <span class="text-sm font-semibold tracking-widest uppercase text-zinc-400">Maurilio Atila</span>
        <!-- Desktop menu -->
        <div class="hidden md:flex gap-8 text-sm text-zinc-500">
          <a href="#about" class="hover:text-white transition-colors">{{ m.nav.about }}</a>
          <a href="#experience" class="hover:text-white transition-colors">{{ m.nav.experience }}</a>
          <a href="#skills" class="hover:text-white transition-colors">{{ m.nav.skills }}</a>
          <a href="#contact" class="hover:text-white transition-colors">{{ m.nav.contact }}</a>
        </div>
        <!-- Lang selector -->
        <div class="flex items-center gap-1 text-xs font-bold">
          <button v-for="lang in ['en', 'es', 'pt']" :key="lang" @click="setLocale(lang)"
            :class="locale === lang ? 'text-orange-400' : 'text-zinc-600 hover:text-zinc-400'"
            class="uppercase tracking-widest transition-colors px-1">{{ lang }}</button>
        </div>
        <!-- Mobile hamburger -->
        <button @click="mobileMenuOpen = !mobileMenuOpen" class="md:hidden text-zinc-400 hover:text-white transition-colors p-1" aria-label="Menu">
          <i v-if="!mobileMenuOpen" class="fas fa-bars text-lg"></i>
          <i v-else class="fas fa-xmark text-lg"></i>
        </button>
      </div>
      <!-- Mobile dropdown -->
      <transition name="mobile-menu">
        <div v-if="mobileMenuOpen" class="md:hidden bg-black border-t border-zinc-900 px-8 py-4 flex flex-col gap-4 text-sm text-zinc-400">
          <a href="#about" @click="mobileMenuOpen = false" class="hover:text-white transition-colors py-1">{{ m.nav.about }}</a>
          <a href="#experience" @click="mobileMenuOpen = false" class="hover:text-white transition-colors py-1">{{ m.nav.experience }}</a>
          <a href="#skills" @click="mobileMenuOpen = false" class="hover:text-white transition-colors py-1">{{ m.nav.skills }}</a>
          <a href="#contact" @click="mobileMenuOpen = false" class="hover:text-white transition-colors py-1">{{ m.nav.contact }}</a>
          <a href="/maurilio-atila-cv.pdf" download class="inline-flex items-center gap-2 text-orange-400 hover:text-orange-300 transition-colors py-1"><i class="fas fa-download text-xs"></i> {{ m.nav.downloadCV }}</a>
          <div class="flex gap-2 pt-1">
            <button v-for="lang in ['en', 'es', 'pt']" :key="lang" @click="setLocale(lang)"
              :class="locale === lang ? 'text-orange-400' : 'text-zinc-600'"
              class="text-xs font-bold uppercase tracking-widest transition-colors">{{ lang }}</button>
          </div>
        </div>
      </transition>
    </nav>

    <!-- HERO -->
    <section class="max-w-6xl mx-auto px-8 pt-40 pb-28">
      <div class="flex flex-col md:flex-row md:items-end gap-12">
        <div class="flex-1">
          <p class="text-xs font-bold uppercase tracking-[0.25em] text-orange-400 mb-6">{{ m.hero.badge }}</p>
          <h1 class="text-7xl md:text-8xl font-black leading-none tracking-tight mb-8">
            {{ m.hero.pre }}<br/>
            <span v-if="wordLoading" class="word-skeleton inline-block rounded"></span>
            <span v-else class="gradient-text word-reveal">{{ currentWord }}</span><br/>
            {{ m.hero.post }}
          </h1>
          <p class="text-zinc-400 text-xl max-w-md leading-relaxed">
            {{ m.hero.tagline }}
          </p>
        </div>
        <div class="flex flex-col items-start md:items-end gap-6 md:pb-2">
          <img @click="showEmailModal = true" src="./assets/logo.png" alt="Maurilio Atila" class="w-28 h-28 rounded-2xl grayscale hover:grayscale-0 transition-all duration-500 shadow-xl cursor-pointer hover:ring-2 hover:ring-orange-500" title="Send me an email" />
          <div class="flex gap-3">
            <a href="https://github.com/cabelotaina" target="_blank" rel="noopener" class="text-zinc-400 hover:text-white transition-colors text-xl" aria-label="GitHub"><i class="fab fa-github"></i></a>
            <a href="https://www.linkedin.com/in/maurilio-atila/" target="_blank" rel="noopener" class="text-zinc-400 hover:text-white transition-colors text-xl" aria-label="LinkedIn"><i class="fab fa-linkedin"></i></a>
            <a href="https://www.malt.es/profile/mauriliosantana1" target="_blank" rel="noopener" class="text-zinc-400 hover:text-white transition-colors text-sm font-bold tracking-wide" aria-label="Malt">Malt</a>
          </div>
        </div>
      </div>
    </section>

    <!-- DIVIDER with tags -->
    <div class="border-t border-zinc-800 py-5">
      <div class="max-w-6xl mx-auto px-8 flex flex-wrap gap-4 text-xs text-zinc-500 uppercase tracking-widest">
        <span><i class="fas fa-location-dot mr-1.5"></i>Madrid, Spain</span>
        <span class="text-zinc-700">—</span>
        <span><i class="far fa-clock mr-1.5"></i>{{ m.tags.partTime }}</span>
        <span class="text-zinc-700">—</span>
        <span><i class="fas fa-earth-americas mr-1.5"></i>PT · EN B2 · ES C2</span>
        <span class="text-zinc-700">—</span>
        <span><i class="fas fa-wifi mr-1.5"></i>{{ m.tags.remote }}</span>
      </div>
    </div>

    <!-- ABOUT -->
    <section id="about" class="max-w-6xl mx-auto px-8 py-24">
      <div class="grid md:grid-cols-12 gap-8 items-start">
        <div class="md:col-span-3">
          <p class="text-xs font-bold uppercase tracking-[0.2em] text-zinc-500 mt-1">{{ m.about.label }}</p>
        </div>
        <div class="md:col-span-9 grid md:grid-cols-2 gap-8 text-zinc-400 text-lg leading-relaxed">
          <p>{{ m.about.p1 }}</p>
          <p v-html="m.about.p2"></p>
        </div>
      </div>
    </section>

    <!-- EXPERIENCE -->
    <section id="experience" class="border-t border-zinc-800 py-24">
      <div class="max-w-6xl mx-auto px-8">

        <!-- Photo banner -->
        <div class="mb-16 rounded-2xl overflow-hidden">
          <img src="./assets/hero.png" alt="Maurilio Atila" class="w-full block" />
        </div>
        <div class="grid md:grid-cols-12 gap-8 mb-16">
          <div class="md:col-span-3">
            <p class="text-xs font-bold uppercase tracking-[0.2em] text-zinc-500">{{ m.experience.label }}</p>
          </div>
        </div>

        <div v-for="(job, i) in m.jobs" :key="i" class="grid md:grid-cols-12 gap-8 py-10 border-t border-zinc-800 group">
          <div class="md:col-span-3">
            <p class="text-xs text-zinc-600 font-mono mt-1">{{ job.period }}</p>
          </div>
          <div class="md:col-span-9">
            <div class="flex flex-col md:flex-row md:items-baseline md:justify-between gap-1 mb-3">
              <h3 class="text-xl font-bold text-zinc-100">{{ job.title }}</h3>
              <span class="text-orange-400 text-sm font-semibold">{{ job.company }}</span>
            </div>
            <p class="text-zinc-400 leading-relaxed mb-4 max-w-2xl">{{ job.description }}</p>
            <ul v-if="job.bullets" class="text-zinc-500 text-sm space-y-1 mb-4 list-none">
              <li v-for="b in job.bullets" :key="b" class="flex gap-2"><span class="text-orange-400 flex-shrink-0">→</span>{{ b }}</li>
            </ul>
            <div class="flex flex-wrap gap-2">
              <span v-for="t in job.tech" :key="t" class="text-xs font-mono bg-zinc-900 border border-zinc-800 text-zinc-400 px-3 py-1 rounded-full group-hover:border-zinc-700 transition-colors">{{ t }}</span>
            </div>
          </div>
        </div>

      </div>
    </section>

    <!-- SKILLS -->
    <section id="skills" class="border-t border-zinc-800 py-24">
      <div class="max-w-6xl mx-auto px-8">
        <div class="grid md:grid-cols-12 gap-8 mb-16">
          <div class="md:col-span-3">
            <p class="text-xs font-bold uppercase tracking-[0.2em] text-zinc-500">{{ m.skillsSection.label }}</p>
          </div>
        </div>
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-px bg-zinc-800">
          <div v-for="group in m.skills" :key="group.label" class="bg-black p-8">
            <p class="text-xs font-bold uppercase tracking-[0.2em] text-orange-400 mb-5">{{ group.label }}</p>
            <div class="flex flex-wrap gap-2">
              <span v-for="s in group.items" :key="s" class="text-sm text-zinc-400 hover:text-white transition-colors cursor-default">{{ s }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CONTACT -->
    <section id="contact" class="border-t border-zinc-800 py-24">
      <div class="max-w-6xl mx-auto px-8 grid md:grid-cols-12 gap-8 items-center">
        <div class="md:col-span-3">
          <p class="text-xs font-bold uppercase tracking-[0.2em] text-zinc-500">{{ m.contact.label }}</p>
        </div>
        <div class="md:col-span-9">
          <h2 class="text-5xl font-black mb-6 leading-tight">
            {{ m.contact.h2a }}<br/><span class="gradient-text">{{ m.contact.h2b }}</span>
          </h2>
          <p class="text-zinc-400 mb-8 text-lg">{{ m.contact.sub }}</p>
          <div class="flex flex-wrap gap-4">
            <button @click="showEmailModal = true; $gtag('email_button_click')" class="inline-flex items-center gap-2 bg-orange-500 text-white font-bold px-6 py-3 rounded-full text-sm hover:bg-orange-400 transition-colors"><i class="fas fa-envelope"></i> {{ m.contact.emailBtn }}</button>
            <a href="/maurilio-atila-cv.pdf" download="maurilio-atila-cv.pdf" class="inline-flex items-center gap-2 border border-zinc-700 text-zinc-400 font-semibold px-6 py-3 rounded-full text-sm hover:border-zinc-500 hover:text-zinc-200 transition-colors"><i class="fas fa-download"></i> {{ m.contact.cvBtn }}</a>
            <a href="https://www.linkedin.com/in/maurilio-atila/" target="_blank" rel="noopener" @click="$gtag('linkedin_click')" class="inline-flex items-center gap-2 border border-zinc-700 text-zinc-400 font-semibold px-6 py-3 rounded-full text-sm hover:border-zinc-500 hover:text-zinc-200 transition-colors"><i class="fab fa-linkedin"></i> LinkedIn</a>
          </div>
        </div>
      </div>
    </section>

    <!-- EMAIL MODAL -->
    <transition name="modal-fade">
      <div v-if="showEmailModal" class="fixed inset-0 z-[200] flex items-end sm:items-center justify-center p-4" @click.self="showEmailModal = false">
        <div class="absolute inset-0 bg-black/70 backdrop-blur-sm"></div>
        <div class="relative bg-zinc-900 border border-zinc-700 rounded-2xl p-8 w-full max-w-md shadow-2xl">
          <button @click="showEmailModal = false" class="absolute top-4 right-4 text-zinc-500 hover:text-zinc-200 text-xl leading-none">✕</button>
          <div class="flex items-center gap-3 mb-6">
            <div class="w-10 h-10 bg-orange-500 rounded-full flex items-center justify-center flex-shrink-0">
              <i class="fas fa-envelope text-white text-lg"></i>
            </div>
            <div>
              <p class="font-bold text-white text-sm">{{ m.emailModal.title }}</p>
              <p class="text-zinc-500 text-xs">{{ m.emailModal.sub }}</p>
            </div>
          </div>
          <form @submit.prevent="submitEmail" class="space-y-4">
            <div>
              <label class="text-xs text-zinc-400 uppercase tracking-widest block mb-1">{{ m.emailModal.name }}</label>
              <input v-model="emailLeadName" type="text" required :placeholder="m.emailModal.pName" class="w-full bg-zinc-800 border border-zinc-700 rounded-lg px-4 py-3 text-white placeholder-zinc-600 text-sm focus:border-orange-500 focus:outline-none transition-colors" />
            </div>
            <div>
              <label class="text-xs text-zinc-400 uppercase tracking-widest block mb-1">{{ m.emailModal.email }}</label>
              <input v-model="emailLeadEmail" type="email" required :placeholder="m.emailModal.pEmail" class="w-full bg-zinc-800 border border-zinc-700 rounded-lg px-4 py-3 text-white placeholder-zinc-600 text-sm focus:border-orange-500 focus:outline-none transition-colors" />
            </div>
            <div>
              <label class="text-xs text-zinc-400 uppercase tracking-widest block mb-1">{{ m.emailModal.message }}</label>
              <textarea v-model="emailLeadMessage" rows="3" required :placeholder="m.emailModal.pMessage" class="w-full bg-zinc-800 border border-zinc-700 rounded-lg px-4 py-3 text-white placeholder-zinc-600 text-sm focus:border-orange-500 focus:outline-none transition-colors resize-none"></textarea>
            </div>
            <button type="submit" :disabled="emailSending" class="w-full bg-orange-500 hover:bg-orange-400 disabled:opacity-50 disabled:cursor-wait text-white font-bold py-3 rounded-full text-sm transition-colors flex items-center justify-center gap-2">
              <span v-if="emailSending">{{ m.emailModal.sending }}</span>
              <span v-else>{{ m.emailModal.send }}</span>
            </button>
            <p v-if="emailSuccess" class="text-green-400 text-xs text-center"><i class="fas fa-check mr-1"></i>{{ m.emailModal.success }}</p>
            <p v-if="emailError" class="text-red-400 text-xs text-center">{{ emailError }}</p>
          </form>
        </div>
      </div>
    </transition>

    <!-- WHATSAPP LEAD MODAL -->
    <transition name="modal-fade">
      <div v-if="showWaModal" class="fixed inset-0 z-[200] flex items-end sm:items-center justify-center p-4" @click.self="showWaModal = false">
        <div class="absolute inset-0 bg-black/70 backdrop-blur-sm"></div>
        <div class="relative bg-zinc-900 border border-zinc-700 rounded-2xl p-8 w-full max-w-md shadow-2xl">
          <button @click="showWaModal = false" class="absolute top-4 right-4 text-zinc-500 hover:text-zinc-200 text-xl leading-none">✕</button>
          <div class="flex items-center gap-3 mb-6">
            <div class="w-10 h-10 bg-green-500 rounded-full flex items-center justify-center flex-shrink-0">
              <i class="fab fa-whatsapp text-white text-2xl"></i>
            </div>
            <div>
              <p class="font-bold text-white text-sm">{{ m.waModal.title }}</p>
              <p class="text-zinc-500 text-xs">{{ m.waModal.sub }}</p>
            </div>
          </div>
          <form @submit.prevent="submitLead" class="space-y-4">
            <div>
              <label class="text-xs text-zinc-400 uppercase tracking-widest block mb-1">{{ m.waModal.name }}</label>
              <input v-model="leadName" type="text" required :placeholder="m.waModal.pName" class="w-full bg-zinc-800 border border-zinc-700 rounded-lg px-4 py-3 text-white placeholder-zinc-600 text-sm focus:border-orange-500 focus:outline-none transition-colors" />
            </div>
            <div>
              <label class="text-xs text-zinc-400 uppercase tracking-widest block mb-1">{{ m.waModal.contact }}</label>
              <input v-model="leadContact" type="text" required :placeholder="m.waModal.pContact" class="w-full bg-zinc-800 border border-zinc-700 rounded-lg px-4 py-3 text-white placeholder-zinc-600 text-sm focus:border-orange-500 focus:outline-none transition-colors" />
            </div>
            <div>
              <label class="text-xs text-zinc-400 uppercase tracking-widest block mb-1">{{ m.waModal.message }}</label>
              <textarea v-model="leadMessage" rows="2" :placeholder="m.waModal.pMessage" class="w-full bg-zinc-800 border border-zinc-700 rounded-lg px-4 py-3 text-white placeholder-zinc-600 text-sm focus:border-orange-500 focus:outline-none transition-colors resize-none"></textarea>
            </div>
            <button type="submit" :disabled="leadSending" class="w-full bg-green-500 hover:bg-green-400 disabled:opacity-50 disabled:cursor-wait text-white font-bold py-3 rounded-full text-sm transition-colors flex items-center justify-center gap-2">
              <span v-if="leadSending">{{ m.waModal.sending }}</span>
              <span v-else>{{ m.waModal.send }}</span>
            </button>
            <p v-if="leadError" class="text-red-400 text-xs text-center">{{ leadError }}</p>
          </form>
        </div>
      </div>
    </transition>

    <!-- WHATSAPP FLOATING BUTTON -->
    <button @click="showWaModal = true; $gtag('whatsapp_button_click')" class="fixed bottom-6 right-6 z-[150] w-14 h-14 bg-green-500 hover:bg-green-400 rounded-full shadow-2xl flex items-center justify-center transition-all hover:scale-110 group" aria-label="WhatsApp">
      <i class="fab fa-whatsapp text-white text-3xl"></i>
      <span class="absolute right-16 bg-zinc-900 border border-zinc-700 text-white text-xs font-semibold px-3 py-1.5 rounded-full whitespace-nowrap opacity-0 group-hover:opacity-100 transition-opacity shadow-lg">{{ m.floatingBtn }}</span>
    </button>

    <footer class="border-t border-zinc-800 py-8">
      <div class="max-w-6xl mx-auto px-8 flex justify-between items-center text-xs text-zinc-700 uppercase tracking-widest">
        <span>Maurilio Atila</span>
        <span>© 2026</span>
      </div>
    </footer>

  </div>
</template>

<script>
import emailjs from '@emailjs/browser';

const MESSAGES = {
  en: {
    nav: { about: 'About', experience: 'Experience', skills: 'Skills', contact: 'Contact', downloadCV: 'Download CV' },
    hero: {
      badge: 'Full Stack Developer & Tech Lead',
      pre: 'Building',
      post: 'that scale.',
      tagline: '12+ years in web, mobile and cloud. Madrid-based. Available part-time — 4h/day.',
      words: ["plans", "projects", "environments", "machines", "products", "a future", "solutions", "experiences", "ideas"],
    },
    tags: { partTime: 'Part-time · 4h/day', remote: 'Remote' },
    about: {
      label: '01 — About',
      p1: 'Brazilian developer based in Madrid with 12+ years across the full stack — Vue.js, React, Node.js, AWS, and native mobile apps (Android & iOS). Three Spanish companies in my track record.',
      p2: 'Recently led two international products for <strong class="text-zinc-100 font-semibold">Hoffmann-La Roche</strong> across 26 countries at Madrid-based AMURA IT — introduced AI-assisted development and unblocked a project delayed by over a year.',
    },
    experience: { label: '02 — Experience' },
    skillsSection: { label: '03 — Skills' },
    contact: {
      label: '04 — Contact',
      h2a: "Let's work",
      h2b: 'together.',
      sub: 'Part-time freelance · up to 4h/day · Remote or Madrid on-site.',
      emailBtn: 'Send me an email',
      cvBtn: 'Download CV',
    },
    emailModal: {
      title: 'Send me an email',
      sub: "I'll reply within 24h",
      name: 'Name *', email: 'Your email *', message: 'Message *',
      pName: 'Your name', pEmail: 'your@email.com', pMessage: 'Tell me about your project...',
      sending: 'Sending...', send: 'Send message →',
      success: "Message sent! I'll be in touch soon.",
      error: 'Failed to send. Please try LinkedIn instead.',
    },
    waModal: {
      title: 'Chat with me on WhatsApp',
      sub: "I'll reply within 24h",
      name: 'Name *', contact: 'Email or phone *', message: 'Message (optional)',
      pName: 'Your name', pContact: 'email@example.com or +34 600 000 000', pMessage: "What's the project about?",
      sending: 'Sending...', send: 'Continue on WhatsApp →',
    },
    floatingBtn: "Let's talk!",
    skills: [
      { label: 'Frontend', items: ['Vue.js 2/3', 'React', 'Angular', 'Nuxt', 'Tailwind CSS', 'HTML5', 'SASS'] },
      { label: 'Backend', items: ['Node.js', 'Express', 'REST APIs', 'AWS Lambda', 'Ruby on Rails', 'PHP', 'Python'] },
      { label: 'Mobile', items: ['Android (Kotlin/Java)', 'iOS', 'Ionic', 'Cordova', 'React Native'] },
      { label: 'Cloud & DevOps', items: ['AWS ECS', 'Lambda', 'S3', 'Cognito', 'CloudFormation', 'Docker', 'GitHub Actions'] },
      { label: 'Databases', items: ['MongoDB', 'PostgreSQL', 'MySQL'] },
      { label: 'Leadership', items: ['Tech Lead', 'AI Training', 'Agile/Jira', 'Code Review', 'Remote Teams'] },
    ],
    jobs: [
      {
        period: "Dec 2024 – May 2026",
        title: "Project Development Manager & Tech Lead",
        company: "AMURA IT · Madrid 🇪🇸",
        description: "Spanish consultancy. Led Focusme and Med Wallet for Hoffmann-La Roche across 26 countries. Sole tech architect for a team of 6 developers.",
        bullets: [
          "Unblocked a 1-year-delayed project: Ionic app + AWS ECS API + React frontend + Cognito 2FA",
          "Introduced AI-assisted development — trained 3 devs, significantly reduced bug rate",
          "Led 2 major version migrations on Focusme (iOS & Android)",
        ],
        tech: ["React", "Ionic", "Android", "iOS", "Node.js", "Java", "Spring Boot", "AWS ECS", "Cognito", "TypeScript", "Salesforce"],
      },
      {
        period: "Jan 2021 – Present",
        title: "Co-Owner & Full Stack Developer",
        company: "BCompliance&Law · São Paulo (Remote)",
        description: "Built a full SaaS compliance suite from scratch: institutional site, client portal, backoffice, and complaint channel. Payment integration (Vindi) and CI/CD via GitHub Actions + AWS CloudFormation.",
        bullets: null,
        tech: ["Vue.js 3", "Node.js", "MongoDB", "PostgreSQL", "Tailwind", "AWS", "GitHub Actions"],
      },
      {
        period: "Dec 2023 – Nov 2024",
        title: "Android Developer",
        company: "Winche · Barcelona 🇪🇸",
        description: "Spanish SaaS company. Lead developer of WincheCloud, a data collection and management platform. Focused on UX improvements and test automation.",
        bullets: null,
        tech: ["Kotlin", "Java", "Python", "Node.js", "MySQL"],
      },
      {
        period: "May 2019 – Oct 2022",
        title: "Mobile Developer",
        company: "Estapar · Remote",
        description: "Optimized Google Maps API usage saving ~R$40k/month. Delivered Ecovagas and Estapar Reserva — apps used by millions of users. Implemented CI/CD pipelines.",
        bullets: null,
        tech: ["Ionic", "Cordova", "CI/CD"],
      },
    ],
  },
  es: {
    nav: { about: 'Sobre mí', experience: 'Experiencia', skills: 'Habilidades', contact: 'Contacto', downloadCV: 'Descargar CV' },
    hero: {
      badge: 'Full Stack Developer & Tech Lead',
      pre: 'Construyendo',
      post: 'que escalan.',
      tagline: '12+ años en web, móvil y cloud. Afincado en Madrid. Disponible a tiempo parcial — 4h/día.',
      words: ["planes", "proyectos", "entornos", "sistemas", "productos", "el futuro", "soluciones", "experiencias", "ideas"],
    },
    tags: { partTime: 'Tiempo parcial · 4h/día', remote: 'Remoto' },
    about: {
      label: '01 — Sobre mí',
      p1: 'Desarrollador brasileño afincado en Madrid con más de 12 años en el stack completo — Vue.js, React, Node.js, AWS y apps móviles nativas (Android e iOS). Tres empresas españolas en mi historial.',
      p2: 'Lideré recientemente dos productos internacionales para <strong class="text-zinc-100 font-semibold">Hoffmann-La Roche</strong> en 26 países en AMURA IT (Madrid) — introduje desarrollo asistido por IA y desbloqueé un proyecto retrasado más de un año.',
    },
    experience: { label: '02 — Experiencia' },
    skillsSection: { label: '03 — Habilidades' },
    contact: {
      label: '04 — Contacto',
      h2a: 'Trabajemos',
      h2b: 'juntos.',
      sub: 'Freelance a tiempo parcial · hasta 4h/día · Remoto o presencial en Madrid.',
      emailBtn: 'Envíame un email',
      cvBtn: 'Descargar CV',
    },
    emailModal: {
      title: 'Envíame un email',
      sub: 'Respondo en menos de 24h',
      name: 'Nombre *', email: 'Tu email *', message: 'Mensaje *',
      pName: 'Tu nombre', pEmail: 'tu@email.com', pMessage: 'Cuéntame sobre tu proyecto...',
      sending: 'Enviando...', send: 'Enviar mensaje →',
      success: '¡Mensaje enviado! Me pondré en contacto pronto.',
      error: 'Error al enviar. Prueba por LinkedIn.',
    },
    waModal: {
      title: 'Escríbeme por WhatsApp',
      sub: 'Respondo en menos de 24h',
      name: 'Nombre *', contact: 'Email o teléfono *', message: 'Mensaje (opcional)',
      pName: 'Tu nombre', pContact: 'email@ejemplo.com o +34 600 000 000', pMessage: '¿De qué trata el proyecto?',
      sending: 'Enviando...', send: 'Continuar en WhatsApp →',
    },
    floatingBtn: '¡Hablemos!',
    skills: [
      { label: 'Frontend', items: ['Vue.js 2/3', 'React', 'Angular', 'Nuxt', 'Tailwind CSS', 'HTML5', 'SASS'] },
      { label: 'Backend', items: ['Node.js', 'Express', 'REST APIs', 'AWS Lambda', 'Ruby on Rails', 'PHP', 'Python'] },
      { label: 'Móvil', items: ['Android (Kotlin/Java)', 'iOS', 'Ionic', 'Cordova', 'React Native'] },
      { label: 'Cloud & DevOps', items: ['AWS ECS', 'Lambda', 'S3', 'Cognito', 'CloudFormation', 'Docker', 'GitHub Actions'] },
      { label: 'Bases de datos', items: ['MongoDB', 'PostgreSQL', 'MySQL'] },
      { label: 'Liderazgo', items: ['Tech Lead', 'IA aplicada', 'Agile/Jira', 'Code Review', 'Equipos remotos'] },
    ],
    jobs: [
      {
        period: "Dic 2024 – May 2026",
        title: "Project Development Manager & Tech Lead",
        company: "AMURA IT · Madrid 🇪🇸",
        description: "Consultora española. Lideré Focusme y Med Wallet para Hoffmann-La Roche en 26 países. Único arquitecto técnico de un equipo de 6 desarrolladores.",
        bullets: [
          "Desbloqueé un proyecto retrasado 1 año: app Ionic + API en AWS ECS + frontend React + Cognito 2FA",
          "Introduje desarrollo asistido por IA — formé a 3 devs, reducción significativa de bugs",
          "Lideré 2 migraciones de versiones mayores en Focusme (iOS y Android)",
        ],
        tech: ["React", "Ionic", "Android", "iOS", "Node.js", "Java", "Spring Boot", "AWS ECS", "Cognito", "TypeScript", "Salesforce"],
      },
      {
        period: "Ene 2021 – Presente",
        title: "Co-Fundador & Full Stack Developer",
        company: "BCompliance&Law · São Paulo (Remoto)",
        description: "Construí desde cero una suite SaaS de cumplimiento normativo: web institucional, portal de clientes, backoffice y canal de denuncias. Integración de pagos (Vindi) y CI/CD con GitHub Actions + AWS CloudFormation.",
        bullets: null,
        tech: ["Vue.js 3", "Node.js", "MongoDB", "PostgreSQL", "Tailwind", "AWS", "GitHub Actions"],
      },
      {
        period: "Dic 2023 – Nov 2024",
        title: "Desarrollador Android",
        company: "Winche · Barcelona 🇪🇸",
        description: "Empresa SaaS española. Desarrollador líder de WincheCloud, plataforma de recogida y gestión de datos. Mejoras de UX y automatización de pruebas.",
        bullets: null,
        tech: ["Kotlin", "Java", "Python", "Node.js", "MySQL"],
      },
      {
        period: "May 2019 – Oct 2022",
        title: "Desarrollador Mobile",
        company: "Estapar · Remoto",
        description: "Optimicé el uso de la API de Google Maps ahorrando ~R$40k/mes. Entregué Ecovagas y Estapar Reserva — apps usadas por millones de usuarios. Implementé pipelines CI/CD.",
        bullets: null,
        tech: ["Ionic", "Cordova", "CI/CD"],
      },
    ],
  },
  pt: {
    nav: { about: 'Sobre', experience: 'Experiência', skills: 'Habilidades', contact: 'Contato', downloadCV: 'Baixar CV' },
    hero: {
      badge: 'Full Stack Developer & Tech Lead',
      pre: 'Construindo',
      post: 'que escalam.',
      tagline: '12+ anos em web, mobile e cloud. Baseado em Madrid. Disponível meio período — 4h/dia.',
      words: ["planos", "projetos", "ambientes", "sistemas", "produtos", "o futuro", "soluções", "experiências", "ideias"],
    },
    tags: { partTime: 'Meio período · 4h/dia', remote: 'Remoto' },
    about: {
      label: '01 — Sobre',
      p1: 'Desenvolvedor brasileiro radicado em Madrid com 12+ anos no stack completo — Vue.js, React, Node.js, AWS e apps mobile nativos (Android e iOS). Três empresas espanholas no histórico.',
      p2: 'Recentemente liderou dois produtos internacionais para a <strong class="text-zinc-100 font-semibold">Hoffmann-La Roche</strong> em 26 países na AMURA IT (Madrid) — introduziu desenvolvimento assistido por IA e desbloqueou um projeto atrasado por mais de um ano.',
    },
    experience: { label: '02 — Experiência' },
    skillsSection: { label: '03 — Habilidades' },
    contact: {
      label: '04 — Contato',
      h2a: 'Vamos trabalhar',
      h2b: 'juntos.',
      sub: 'Freelance meio período · até 4h/dia · Remoto ou presencial em Madrid.',
      emailBtn: 'Enviar email',
      cvBtn: 'Baixar CV',
    },
    emailModal: {
      title: 'Enviar email',
      sub: 'Respondo em até 24h',
      name: 'Nome *', email: 'Seu email *', message: 'Mensagem *',
      pName: 'Seu nome', pEmail: 'seu@email.com', pMessage: 'Me fale sobre o projeto...',
      sending: 'Enviando...', send: 'Enviar mensagem →',
      success: 'Mensagem enviada! Entro em contato em breve.',
      error: 'Erro ao enviar. Tente pelo LinkedIn.',
    },
    waModal: {
      title: 'Fale comigo pelo WhatsApp',
      sub: 'Respondo em até 24h',
      name: 'Nome *', contact: 'Email ou telefone *', message: 'Mensagem (opcional)',
      pName: 'Seu nome', pContact: 'email@exemplo.com ou +34 600 000 000', pMessage: 'Sobre o que é o projeto?',
      sending: 'Enviando...', send: 'Continuar no WhatsApp →',
    },
    floatingBtn: 'Vamos conversar!',
    skills: [
      { label: 'Frontend', items: ['Vue.js 2/3', 'React', 'Angular', 'Nuxt', 'Tailwind CSS', 'HTML5', 'SASS'] },
      { label: 'Backend', items: ['Node.js', 'Express', 'REST APIs', 'AWS Lambda', 'Ruby on Rails', 'PHP', 'Python'] },
      { label: 'Mobile', items: ['Android (Kotlin/Java)', 'iOS', 'Ionic', 'Cordova', 'React Native'] },
      { label: 'Cloud & DevOps', items: ['AWS ECS', 'Lambda', 'S3', 'Cognito', 'CloudFormation', 'Docker', 'GitHub Actions'] },
      { label: 'Bancos de dados', items: ['MongoDB', 'PostgreSQL', 'MySQL'] },
      { label: 'Liderança', items: ['Tech Lead', 'IA aplicada', 'Agile/Jira', 'Code Review', 'Times remotos'] },
    ],
    jobs: [
      {
        period: "Dez 2024 – Mai 2026",
        title: "Project Development Manager & Tech Lead",
        company: "AMURA IT · Madrid 🇪🇸",
        description: "Consultoria espanhola. Liderou Focusme e Med Wallet para a Hoffmann-La Roche em 26 países. Único arquiteto técnico de uma equipe de 6 desenvolvedores.",
        bullets: [
          "Desbloqueou projeto atrasado por 1 ano: app Ionic + API no AWS ECS + frontend React + Cognito 2FA",
          "Introduziu desenvolvimento assistido por IA — treinou 3 devs, redução significativa de bugs",
          "Liderou 2 migrações de versões maiores no Focusme (iOS e Android)",
        ],
        tech: ["React", "Ionic", "Android", "iOS", "Node.js", "Java", "Spring Boot", "AWS ECS", "Cognito", "TypeScript", "Salesforce"],
      },
      {
        period: "Jan 2021 – Presente",
        title: "Co-Fundador & Full Stack Developer",
        company: "BCompliance&Law · São Paulo (Remoto)",
        description: "Construiu do zero uma suite SaaS de compliance: site institucional, portal do cliente, backoffice e canal de denúncias. Integração de pagamentos (Vindi) e CI/CD com GitHub Actions + AWS CloudFormation.",
        bullets: null,
        tech: ["Vue.js 3", "Node.js", "MongoDB", "PostgreSQL", "Tailwind", "AWS", "GitHub Actions"],
      },
      {
        period: "Dez 2023 – Nov 2024",
        title: "Desenvolvedor Android",
        company: "Winche · Barcelona 🇪🇸",
        description: "Empresa SaaS espanhola. Desenvolvedor líder do WincheCloud, plataforma de coleta e gestão de dados. Foco em melhorias de UX e automação de testes.",
        bullets: null,
        tech: ["Kotlin", "Java", "Python", "Node.js", "MySQL"],
      },
      {
        period: "Mai 2019 – Out 2022",
        title: "Desenvolvedor Mobile",
        company: "Estapar · Remoto",
        description: "Otimizou o uso da API do Google Maps economizando ~R$40k/mês. Entregou Ecovagas e Estapar Reserva — apps usados por milhões de usuários. Implementou pipelines CI/CD.",
        bullets: null,
        tech: ["Ionic", "Cordova", "CI/CD"],
      },
    ],
  },
};

export default {
  name: "App",
  data() {
    return {
      locale: 'en',
      wordIndex: 0,
      currentWord: "plans",
      wordLoading: false,
      wordTimer: null,
      loading: true,
      mobileMenuOpen: false,
      showWaModal: false,
      leadName: '',
      leadContact: '',
      leadMessage: '',
      leadSending: false,
      leadError: '',
      showEmailModal: false,
      emailLeadName: '',
      emailLeadEmail: '',
      emailLeadMessage: '',
      emailSending: false,
      emailSuccess: false,
      emailError: '',
    }
  },
  computed: {
    m() { return MESSAGES[this.locale]; },
  },
  watch: {
    locale(newLocale) {
      this.wordIndex = 0;
      this.currentWord = MESSAGES[newLocale].hero.words[0];
    },
  },
  mounted() {
    setTimeout(() => {
      this.loading = false;
    }, 1400);

    this.wordTimer = setInterval(() => {
      this.wordLoading = true;
      setTimeout(() => {
        this.wordIndex = (this.wordIndex + 1) % this.m.hero.words.length;
        this.currentWord = this.m.hero.words[this.wordIndex];
        this.wordLoading = false;
      }, 700);
    }, 4000);
  },
  beforeUnmount() {
    clearInterval(this.wordTimer);
  },
  methods: {
    setLocale(lang) {
      this.locale = lang;
      this.mobileMenuOpen = false;
    },
    $gtag(eventName, params = {}) {
      if (window.gtag) window.gtag('event', eventName, params);
    },
    async submitEmail() {
      this.emailSending = true;
      this.emailError = '';
      this.emailSuccess = false;
      try {
        await emailjs.send(
          'service_uy5yk0s',
          'template_f9w0v48',
          {
            name: this.emailLeadName,
            email: this.emailLeadEmail,
            time: new Date().toLocaleString('pt-BR', { timeZone: 'Europe/Madrid' }),
            message: this.emailLeadMessage,
          },
          'DI5beBFZHP3rS6nGZ'
        );
        this.emailSuccess = true;
        this.$gtag('email_form_submitted', { name: this.emailLeadName });
        this.emailLeadName = '';
        this.emailLeadEmail = '';
        this.emailLeadMessage = '';
        setTimeout(() => { this.showEmailModal = false; this.emailSuccess = false; }, 2500);
      } catch (e) {
        this.emailError = this.m.emailModal.error;
      }
      this.emailSending = false;
    },
    async submitLead() {
      this.leadSending = true;
      this.leadError = '';
      const waText = encodeURIComponent(
        `Hi Maurilio! I'm ${this.leadName} (${this.leadContact}).${this.leadMessage ? ' ' + this.leadMessage : ''}`
      );
      try {
        await emailjs.send(
          'service_uy5yk0s',
          'template_f9w0v48',
          {
            name: this.leadName,
            email: this.leadContact,
            time: new Date().toLocaleString('pt-BR', { timeZone: 'Europe/Madrid' }),
            message: this.leadMessage || '(sem mensagem)',
          },
          'DI5beBFZHP3rS6nGZ'
        );
      } catch (e) {
        // Abre o WhatsApp mesmo se o email falhar — o lead pode voltar
        console.warn('EmailJS error:', e);
      }
      this.showWaModal = false;
      this.leadName = '';
      this.leadContact = '';
      this.leadMessage = '';
      this.leadSending = false;
      this.$gtag('whatsapp_form_submitted');
      window.open(`https://wa.me/34685684314?text=${waText}`, '_blank');
    }
  }
};
</script>

<style>
* { scroll-behavior: smooth; }
body { margin: 0; background: #000; }

.skeleton {
  background: linear-gradient(90deg, #1a1a1a 25%, #2a2a2a 50%, #1a1a1a 75%);
  background-size: 200% 100%;
  animation: shimmer 1.4s infinite;
}

@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}

.modal-fade-enter-active, .modal-fade-leave-active {
  transition: opacity 0.25s ease;
}
.modal-fade-enter-from, .modal-fade-leave-to {
  opacity: 0;
}

.fade-leave-active {
  transition: opacity 0.6s ease;
}
.fade-leave-to {
  opacity: 0;
}

.gradient-text {
  background: linear-gradient(90deg, #f97316, #a855f7, #3b82f6);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.word-skeleton {
  background: linear-gradient(90deg, #2a1a00 25%, #4a2f00 50%, #2a1a00 75%);
  background-size: 200% 100%;
  animation: shimmer 0.8s infinite;
  height: 0.85em;
  width: 7ch;
  vertical-align: middle;
  display: inline-block;
}

.word-reveal {
  animation: wordFadeIn 0.4s ease forwards;
}

@keyframes wordFadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}
</style>
