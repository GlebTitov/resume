<template>
  <div class="resume-container">
    <div class="card">
      <div class="profile-header">
        <div class="cover-photo"></div>
        <div class="profile-photo">АИ</div>
      </div>

      <div class="profile-info">
        <h1 class="profile-name">{{ profileData.name }}</h1>
        <p class="profile-headline">{{ profileData.headline }}</p>
        <p class="profile-location">{{ profileData.location }}</p>
        <p class="profile-contact">{{ profileData.email }} · {{ profileData.phone }}</p>

        <div class="profile-buttons">
          <button class="primary-button" @click="contactMe">Связаться</button>
          <button class="secondary-button" @click="downloadPDF">Скачать PDF</button>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-section">
        <h2 class="section-title">Обо мне</h2>
        <p>{{ profileData.about }}</p>
      </div>
    </div>

    <div class="card">
      <div class="card-section">
        <h2 class="section-title">Опыт работы</h2>

        <div v-for="(job, index) in profileData.experience" :key="'job-' + index" class="experience-item">
          <div class="experience-logo">{{ getInitials(job.company) }}</div>
          <div class="experience-details">
            <h3 class="experience-title">{{ job.title }}</h3>
            <p class="experience-company">{{ job.company }}</p>
            <p class="experience-date">{{ job.period }}</p>
            <p class="experience-description">{{ job.description }}</p>
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-section">
        <h2 class="section-title">Образование</h2>

        <div v-for="(edu, index) in profileData.education" :key="'edu-' + index" class="education-item">
          <div class="education-logo" v-html="edu.logoHtml || getInitials(edu.institution)"></div>
          <div class="education-details">
            <h3 class="education-school">{{ edu.institution }}</h3>
            <p class="education-degree">{{ edu.degree }}</p>
            <p class="education-date">{{ edu.period }}</p>
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-section">
        <h2 class="section-title">Проекты</h2>

        <div v-for="(project, index) in profileData.projects" :key="'project-' + index" class="project-item">
          <h3 class="project-title">{{ project.title }}</h3>
          <p class="project-description">{{ project.description }}</p>
          <div class="project-tech">
            <span v-for="(tech, techIndex) in project.technologies" :key="'tech-' + techIndex" class="tech-chip">
              {{ tech }}
            </span>
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-section">
        <h2 class="section-title">Навыки</h2>

        <div class="skills-list">
          <div
              v-for="(skill, index) in profileData.skills"
              :key="'skill-' + index"
              :class="['skill-tag', { 'vue-tag': skill.includes('Vue') }]"
          >
            {{ skill }}
          </div>
        </div>
      </div>
    </div>

    <p class="connect-footer">
      Открыт к предложениям о работе на позицию Middle Frontend Developer.<br>
      <a href="https://linkedin.com/in/your-linkedin" target="_blank" class="connect-link">Связаться через LinkedIn</a> или
      <a :href="'mailto:' + profileData.email" class="connect-link">написать на почту</a>.
    </p>
  </div>
</template>

<script>
export default {
  name: 'LinkedInResume',
  data() {
    return {
      profileData: {
        name: 'Александр Иванов',
        headline: 'Middle Frontend Developer (Vue.js) | Разработка CRM-систем',
        location: 'Москва, Россия',
        email: 'alexander@example.com',
        phone: '+7 (977) 330-66-54',
        about: 'Frontend-разработчик с опытом создания веб-приложений на Vue.js. Специализируюсь на разработке CRM-систем для сферы услуг, подобных YClients. Создаю удобные и эффективные пользовательские интерфейсы, решающие бизнес-задачи. Учусь на 3 курсе университета, постоянно совершенствую навыки и изучаю новые технологии.',

        experience: [
          {
            title: 'Middle Frontend Developer',
            company: 'ООО "DigitalCRM"',
            period: 'Июнь 2023 — Настоящее время · 1 год 10 мес',
            description: 'Разработка интерфейса CRM-системы для сферы услуг (аналог YClients) на Vue.js. Создание модуля онлайн-записи, панели аналитики с интерактивными графиками, интеграция с платежными системами и оптимизация производительности.'
          },
          {
            title: 'Junior Frontend Developer',
            company: 'IT-студия "WebDev"',
            period: 'Январь 2022 — Май 2023 · 1 год 5 мес',
            description: 'Разработка пользовательских интерфейсов на Vue.js. Создание адаптивных веб-страниц, верстка и стилизация компонентов, работа с REST API и интеграция с бэкендом.'
          }
        ],

        education: [
          {
            institution: 'Московский Государственный Технический Университет',
            degree: 'Бакалавр, Информационные технологии и системы',
            period: '2021 — настоящее время (3 курс)',
            logoHtml: 'МГ<br>ТУ'
          },
          {
            institution: 'Онлайн-курс "Vue.js с нуля до профессионала"',
            degree: 'Сертификат о прохождении',
            period: '2022',
            logoHtml: '<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M19 16.9A5 5 0 0 0 18 7h-1.26a8 8 0 1 0-11.62 9"/><polyline points="13 11 9 17 15 17 11 23"/></svg>'
          }
        ],

        projects: [
          {
            title: 'Модуль онлайн-записи CRM',
            description: 'Интерактивный календарь с возможностью бронирования услуг. Реализован планировщик с drag-and-drop и автоматическим расчетом продолжительности.',
            technologies: ['Vue.js', 'Vuex', 'Vue Draggable', 'FullCalendar']
          },
          {
            title: 'Аналитическая панель',
            description: 'Дашборд для визуализации бизнес-метрик с интерактивными графиками и возможностью фильтрации по различным параметрам.',
            technologies: ['Vue.js', 'Chart.js', 'Pinia', 'REST API']
          }
        ],

        skills: [
          'Vue.js', 'Vuex', 'Vue Router', 'Pinia',
          'JavaScript', 'TypeScript', 'HTML5', 'CSS3/SCSS',
          'REST API', 'Git', 'Webpack/Vite', 'Адаптивная верстка',
          'Компонентный подход', 'CRM-системы', 'Jest'
        ]
      }
    }
  },
  methods: {
    getInitials(name) {
      return name
          .split(' ')
          .map(word => word[0])
          .join('')
          .substring(0, 2)
          .toUpperCase();
    },
    contactMe() {
      // Открываем приложение для звонка с вашим номером
      window.location.href = `tel:${this.profileData.phone}`;
    },
    async downloadPDF() {
      try {
        // Импортируем библиотеку html2pdf для конвертации HTML в PDF
        const html2pdf = await import('html2pdf.js');

        // Создаем клон контейнера, чтобы не затронуть оригинальный DOM
        const element = this.$el.cloneNode(true);

        // Находим и удаляем кнопки из клонированного элемента
        const buttons = element.querySelectorAll('.profile-buttons');
        buttons.forEach(button => button.remove());

        // Настройки PDF
        const options = {
          margin: 10,
          filename: `${this.profileData.name.replace(' ', '_')}_резюме.pdf`,
          image: { type: 'jpeg', quality: 0.98 },
          html2canvas: { scale: 2, useCORS: true },
          jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
        };

        // Генерируем PDF
        html2pdf.default(element, options);
      } catch (error) {
        console.error('Ошибка при создании PDF:', error);
        alert('Для генерации PDF требуется библиотека html2pdf.js. Пожалуйста, установите ее в вашем проекте.');
      }
    }
  }
}
</script>

<style scoped>
:root {
  --primary-color: #0a66c2;
  --secondary-color: #5e5e5e;
  --background-color: #f3f2ef;
  --card-bg: #ffffff;
  --border-color: #e0e0e0;
  --text-color: #333333;
  --accent-color: #42b883; /* Vue.js green */
}

.resume-container {
  max-width: 1200px;
  margin: 0 auto;
  background-color: var(--background-color, #f3f2ef);
  color: var(--text-color, #333333);
  line-height: 1.5;
  padding: 20px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.card {
  background-color: var(--card-bg, #ffffff);
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  margin-bottom: 20px;
}

.profile-header {
  position: relative;
  height: 200px;
}

.cover-photo {
  width: 100%;
  height: 134px;
  background: linear-gradient(120deg, var(--accent-color, #42b883), var(--primary-color, #0a66c2));
  position: absolute;
  top: 0;
  left: 0;
}

.profile-photo {
  width: 152px;
  height: 152px;
  border-radius: 50%;
  border: 4px solid var(--card-bg, #ffffff);
  background-color: #f0f0f0;
  position: absolute;
  top: 70px;
  left: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 48px;
  color: var(--secondary-color, #5e5e5e);
}

.profile-info {
  padding: 84px 24px 24px;
}

.profile-name {
  font-size: 24px;
  font-weight: 600;
  margin-bottom: 4px;
}

.profile-headline {
  font-size: 16px;
  color: var(--secondary-color, #5e5e5e);
  margin-bottom: 8px;
}

.profile-location {
  font-size: 14px;
  color: var(--secondary-color, #5e5e5e);
  margin-bottom: 16px;
}

.profile-contact {
  font-size: 14px;
  color: var(--secondary-color, #5e5e5e);
  margin-bottom: 16px;
}

.profile-buttons {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
}

.primary-button {
  background-color: var(--primary-color, #0a66c2);
  color: white;
  border: none;
  border-radius: 16px;
  padding: 6px 16px;
  font-weight: 600;
  font-size: 16px;
  cursor: pointer;
}

.secondary-button {
  background-color: transparent;
  color: var(--primary-color, #0a66c2);
  border: 1px solid var(--primary-color, #0a66c2);
  border-radius: 16px;
  padding: 6px 16px;
  font-weight: 600;
  font-size: 16px;
  cursor: pointer;
}

.card-section {
  padding: 24px;
  border-bottom: 1px solid var(--border-color, #e0e0e0);
}

.card-section:last-child {
  border-bottom: none;
}

.section-title {
  font-size: 20px;
  font-weight: 600;
  margin-bottom: 16px;
}

.experience-item {
  display: flex;
  margin-bottom: 16px;
}

.experience-logo {
  width: 48px;
  height: 48px;
  background-color: var(--accent-color, #42b883);
  margin-right: 12px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
}

.experience-details {
  flex: 1;
}

.experience-title {
  font-weight: 600;
  margin-bottom: 4px;
}

.experience-company {
  margin-bottom: 4px;
}

.experience-date {
  font-size: 14px;
  color: var(--secondary-color, #5e5e5e);
  margin-bottom: 8px;
}

.experience-description {
  font-size: 14px;
}

.skills-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.skill-tag {
  background-color: rgba(10, 102, 194, 0.1);
  color: var(--primary-color, #0a66c2);
  padding: 4px 12px;
  border-radius: 4px;
  font-size: 14px;
  transition: all 0.2s;
}

.skill-tag:hover {
  background-color: rgba(10, 102, 194, 0.2);
}

.vue-tag {
  background-color: rgba(66, 184, 131, 0.1);
  color: var(--accent-color, #42b883);
}

.vue-tag:hover {
  background-color: rgba(66, 184, 131, 0.2);
}

.education-item {
  display: flex;
  margin-bottom: 16px;
}

.education-logo {
  width: 48px;
  height: 48px;
  background-color: #5e5e5e;
  margin-right: 12px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 20px;
  text-align: center;
}

.education-details {
  flex: 1;
}

.education-school {
  font-weight: 600;
  margin-bottom: 4px;
}

.education-degree {
  margin-bottom: 4px;
}

.education-date {
  font-size: 14px;
  color: var(--secondary-color, #5e5e5e);
}

.project-item {
  border: 1px solid var(--border-color, #e0e0e0);
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 16px;
}

.project-title {
  font-weight: 600;
  margin-bottom: 8px;
  color: var(--primary-color, #0a66c2);
}

.project-description {
  font-size: 14px;
  margin-bottom: 12px;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.tech-chip {
  background-color: #f3f2ef;
  padding: 3px 8px;
  border-radius: 4px;
  font-size: 12px;
  color: var(--secondary-color, #5e5e5e);
}

.connect-footer {
  text-align: center;
  margin-top: 16px;
  font-size: 14px;
  color: var(--secondary-color, #5e5e5e);
}

.connect-link {
  color: var(--primary-color, #0a66c2);
  text-decoration: none;
  font-weight: 600;
}

.connect-link:hover {
  text-decoration: underline;
}

@media (max-width: 600px) {
  .profile-header {
    height: 170px;
  }

  .profile-photo {
    width: 120px;
    height: 120px;
    top: 80px;
    left: 16px;
    font-size: 36px;
  }

  .profile-info {
    padding: 60px 16px 16px;
  }

  .card-section {
    padding: 16px;
  }
}
</style>