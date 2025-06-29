<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Gros Magazin</title>
<style>
  /* Reset & Basis */
  * {
    margin: 0; padding: 0; box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  body {
    background: #fafafa;
    color: #222;
    line-height: 1.5;
  }
  a {
    color: #d40000;
    text-decoration: none;
  }
  a:hover {
    text-decoration: underline;
  }

  /* Header-Leiste */
  header {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 50px;
    background: white;
    border-bottom: 1px solid #ddd;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 1rem;
    z-index: 1000;
    transition: top 0.3s ease;
  }

  /* Logo in der Mitte */
  #logo {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    font-weight: 700;
    font-size: 1.4rem;
    color: #d40000;
    cursor: default;
    user-select: none;
    transition: opacity 0.3s ease;
  }

  /* Link-Leiste links */
  nav#sidebar {
    position: fixed;
    top: 50px;
    left: 0;
    width: 200px;
    bottom: 0;
    background: white;
    border-right: 1px solid #ddd;
    padding-top: 1rem;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }
  nav#sidebar button {
    background: none;
    border: none;
    font-size: 1rem;
    padding: 0.75rem 1rem;
    text-align: left;
    cursor: pointer;
    color: #555;
    transition: background 0.2s, color 0.2s;
  }
  nav#sidebar button:hover,
  nav#sidebar button.active {
    background: #d40000;
    color: white;
  }

  /* Hauptinhalt */
  main {
    margin-left: 210px;
    padding: 60px 20px 20px 20px;
    max-width: 900px;
  }

  /* Suchbereich */
  #search-bar {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(255,255,255,0.95);
    display: none;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    z-index: 2000;
  }
  #search-bar.active {
    display: flex;
  }
  #search-bar input {
    width: 300px;
    font-size: 1.5rem;
    border: none;
    border-bottom: 2px solid #d40000;
    outline: none;
    padding: 0.25rem 0;
    margin-left: 0.5rem;
  }
  #search-bar label {
    font-size: 1.5rem;
    color: #d40000;
    display: flex;
    align-items: center;
  }
  #search-bar .suggestions {
    margin-top: 1rem;
    width: 320px;
    max-height: 200px;
    overflow-y: auto;
    border: 1px solid #d40000;
    border-radius: 4px;
    background: white;
  }
  #search-bar .suggestions div {
    padding: 0.5rem 1rem;
    cursor: pointer;
  }
  #search-bar .suggestions div:hover {
    background: #f9d6d6;
  }

  /* Beiträge */
  section#articles .featured {
    border: 2px solid #d40000;
    padding: 1rem;
    margin-bottom: 1rem;
    background: #fff0f0;
  }
  article {
    border-bottom: 1px solid #ddd;
    padding: 1rem 0;
    cursor: pointer;
  }
  article:hover {
    background: #f9f0f0;
  }
  article h3 {
    margin-bottom: 0.25rem;
    color: #d40000;
  }
  article .meta {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    font-size: 0.85rem;
    color: #666;
  }
  article .meta img {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    object-fit: cover;
  }

  /* Team */
  section#team {
    display: none;
    max-width: 900px;
  }
  #team-list {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
  }
  .team-member {
    background: white;
    border: 1px solid #ddd;
    padding: 1rem;
    width: 200px;
    cursor: pointer;
    text-align: center;
    border-radius: 6px;
    transition: box-shadow 0.3s;
  }
  .team-member:hover {
    box-shadow: 0 0 8px rgba(212,0,0,0.5);
  }
  .team-member img {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    object-fit: cover;
    margin-bottom: 0.5rem;
  }
  .team-member h4 {
    margin-bottom: 0.25rem;
    color: #d40000;
  }
  .team-member .role {
    font-size: 0.85rem;
    color: #555;
  }

  /* Team Detail */
  #team-detail {
    display: none;
    background: white;
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 6px;
    margin-top: 1rem;
  }
  #team-detail img {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    object-fit: cover;
    float: left;
    margin-right: 1rem;
  }
  #team-detail h3 {
    margin-bottom: 0.5rem;
    color: #d40000;
  }
  #team-detail p {
    margin-top: 0.5rem;
  }

  /* Links-Seite */
  section#links {
    display: none;
    max-width: 900px;
  }
  section#links ul {
    list-style: none;
    padding-left: 0;
  }
  section#links li {
    margin-bottom: 1rem;
  }
  section#links a {
    font-weight: bold;
  }

  /* Such-Button oben links */
  #search-btn {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 1.2rem;
    color: #d40000;
  }

  /* Scrollbar in Vorschlägen */
  #search-bar .suggestions::-webkit-scrollbar {
    width: 6px;
  }
  #search-bar .suggestions::-webkit-scrollbar-thumb {
    background: #d40000;
    border-radius: 3px;
  }

  /* Responsive */
  @media (max-width: 700px) {
    nav#sidebar {
      position: static;
      width: 100%;
      height: auto;
      flex-direction: row;
      border-right: none;
      border-bottom: 1px solid #ddd;
      padding: 0.5rem 0;
    }
    nav#sidebar button {
      flex: 1;
      text-align: center;
      padding: 0.5rem;
    }
    main {
      margin: 0;
      padding: 70px 10px 10px 10px;
    }
  }
</style>
</head>
<body>

<header>
  <button id="search-btn" aria-label="Suche öffnen">🔍</button>
  <div id="logo">Gros Magazin</div>
  <div style="width: 40px;"></div>
</header>

<nav id="sidebar">
  <button data-section="articles" class="active">Aktuell</button>
  <button data-section="all-news">Alle News</button>
  <button data-section="team">Team</button>
  <button data-section="links">Links</button>
</nav>

<div id="search-bar" aria-label="Suchfunktion">
  <label for="search-input">Suchen 🔍</label>
  <input type="text" id="search-input" autocomplete="off" />
  <div class="suggestions" role="listbox"></div>
</div>

<main>
  <!-- Aktuelle Beiträge -->
  <section id="articles" aria-label="Aktuelle Beiträge">
    <article class="featured" data-link="https://example.com/beitrag1" tabindex="0">
      <div class="meta">
        <img src="https://i.pravatar.cc/40?img=12" alt="Autor Bild" />
        <div>
          <strong>Jonathan</strong><br />
          <small>Meinung</small>
        </div>
      </div>
      <h3>Das meistgelikete Thema</h3>
      <p>Hier steht eine kurze Zusammenfassung des meistgeliketen Beitrags.</p>
    </article>
    <article data-link="https://example.com/beitrag2" tabindex="0">
      <div class="meta">
        <img src="https://i.pravatar.cc/40?img=5" alt="Autor Bild" />
        <div>
          <strong>Anna</strong><br />
          <small>Reporterin</small>
        </div>
      </div>
      <h3>Weitere News zum Thema</h3>
      <p>Kurze Beschreibung des Beitrags.</p>
    </article>
    <article data-link="https://example.com/beitrag3" tabindex="0">
      <div class="meta">
        <img src="https://i.pravatar.cc/40?img=7" alt="Autor Bild" />
        <div>
          <strong>Max</strong><br />
          <small>Redakteur</small>
        </div>
      </div>
      <h3>Noch mehr News</h3>
      <p>Kurzer Einblick in den Artikel.</p>
    </article>
  </section>

  <!-- Alle News -->
  <section id="all-news" aria-label="Alle News" style="display:none;">
    <article data-link="https://example.com/news1" tabindex="0">
      <h3>News 1</h3>
      <p>Details zum Artikel 1.</p>
    </article>
    <article data-link="https://example.com/news2" tabindex="0">
      <h3>News 2</h3>
      <p>Details zum Artikel 2.</p>
    </article>
  </section>

  <!-- Team -->
  <section id="team" aria-label="Team" style="display:none;">
    <div id="team-list">
      <div class="team-member" tabindex="0" data-id="1">
        <img src="https://i.pravatar.cc/100?img=3" alt="Jonathan Bild" />
        <h4>Jonathan</h4>
        <div class="role">Chefredakteur</div>
      </div>
      <div class="team-member" tabindex="0" data-id="2">
        <img src="https://i.pravatar.cc/100?img=8" alt="Anna Bild" />
        <h4>Anna</h4>
        <div class="role">Reporterin</div>
      </div>
      <div class="team-member" tabindex="0" data-id="3">
        <img src="https://i.pravatar.cc/100?img=15" alt="Max Bild" />
        <h4>Max</h4>
        <div class="role">Redakteur</div>
      </div>
    </div>
    <div id="team-detail" tabindex="0" style="display:none;">
      <!-- Details per JS -->
    </div>
  </section>

  <!-- Links -->
  <section id="links" aria-label="Links" style="display:none;">
    <ul>
      <li><a href="https://www.tiktok.com/@deintiktok" target="_blank" rel="noopener noreferrer">TikTok</a></li>
      <li><a href="https://www.instagram.com/deininsta" target="_blank" rel="noopener noreferrer">Instagram</a></li>
      <li><a href="https://www.facebook.com/deinfacebook" target="_blank" rel="noopener noreferrer">Facebook</a></li>
    </ul>
  </section>
</main>

<script>
  // Navigation zwischen Bereichen
  const navButtons = document.querySelectorAll('nav#sidebar button');
  const sections = ['articles', 'all-news', 'team', 'links'];
  navButtons.forEach(btn => {
    btn.addEventListener('click', () => {
      navButtons.forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      sections.forEach(sec => {
        document.getElementById(sec).style.display = (sec === btn.dataset.section) ? 'block' : 'none';
      });
      if(btn.dataset.section !== 'team') {
        document.getElementById('team-detail').style.display = 'none';
      }
      // Logo wieder einblenden, falls versteckt
      logo.style.opacity = '1';
    });
  });

  // Artikel klickbar & Link öffnen in neuem Tab
  document.querySelectorAll('article[data-link]').forEach(article => {
    article.addEventListener('click', () => {
      window.open(article.dataset.link, '_blank');
      logo.style.opacity = '0'; // Logo verschwindet wenn Artikel geklickt
    });
    article.addEventListener('keydown', e => {
      if(e.key === 'Enter' || e.key === ' ') {
        window.open(article.dataset.link, '_blank');
        logo.style.opacity = '0';
      }
    });
  });

  // Logo
  const logo = document.getElementById('logo');

  // Scroll-Verhalten: Header + Logo verschwinden beim Scrollen nach unten
  let lastScrollTop = 0;
  window.addEventListener('scroll', () => {
    let st = window.pageYOffset || document.documentElement.scrollTop;
    const header = document.querySelector('header');
    if(st > lastScrollTop && st > 50) {
      // Scroll down
      header.style.top = '-60px';
      logo.style.opacity = '0';
    } else {
      // Scroll up
      header.style.top = '0';
      logo.style.opacity = '1';
    }
    lastScrollTop = st <= 0 ? 0 : st;
  });

  // Suchfunktion ein/aus
  const searchBtn = document.getElementById('search-btn');
  const searchBar = document.getElementById('search-bar');
  const searchInput = document.getElementById('search-input');
  const suggestionsBox = document.querySelector('#search-bar .suggestions');

  searchBtn.addEventListener('click', () => {
    searchBar.classList.add('active');
    searchInput.focus();
  });

  // Vorschläge (basierend auf Artikeltiteln)
  const articlesData = [
    { title: "Das meistgelikete Thema", link: "https://example.com/beitrag1" },
    { title: "Weitere News zum Thema", link: "https://example.com/beitrag2" },
    { title: "Noch mehr News", link: "https://example.com/beitrag3" },
    { title: "News 1", link: "https://example.com/news1" },
    { title: "News 2", link: "https://example.com/news2" },
  ];

  // Eingabe: Suche & Vorschläge anzeigen
  searchInput.addEventListener('input', () => {
    const val = searchInput.value.toLowerCase().trim();
    suggestionsBox.innerHTML = '';
    if(val.length === 0) return;
    const matches = articlesData.filter(a => a.title.toLowerCase().includes(val));
    matches.forEach(m => {
      const div = document.createElement('div');
      div.textContent = m.title;
      div.tabIndex = 0;
      div.addEventListener('click', () => {
        window.open(m.link, '_blank');
        searchBar.classList.remove('active');
        searchInput.value = '';
        suggestionsBox.innerHTML = '';
      });
      div.addEventListener('keydown', e => {
        if(e.key === 'Enter' || e.key === ' ') {
          window.open(m.link, '_blank');
          searchBar.classList.remove('active');
          searchInput.value = '';
          suggestionsBox.innerHTML = '';
        }
      });
      suggestionsBox.appendChild(div);
    });
  });

  // Suchbar schließen mit Escape
  window.addEventListener('keydown', e => {
    if(e.key === 'Escape' && searchBar.classList.contains('active')) {
      searchBar.classList.remove('active');
      searchInput.value = '';
      suggestionsBox.innerHTML = '';
    }
  });

  // Teammitglied Details
  const teamList = document.getElementById('team-list');
  const teamDetail = document.getElementById('team-detail');

  const teamMembers = {
    1: {
      name: 'Jonathan',
      role: 'Chefredakteur',
      img: 'https://i.pravatar.cc/150?img=3',
      description: 'Jonathan leitet das Magazin und sorgt für die Redaktion.'
    },
    2: {
      name: 'Anna',
      role: 'Reporterin',
      img: 'https://i.pravatar.cc/150?img=8',
      description: 'Anna berichtet über aktuelle Themen und recherchiert sorgfältig.'
    },
    3: {
      name: 'Max',
      role: 'Redakteur',
      img: 'https://i.pravatar.cc/150?img=15',
      description: 'Max kümmert sich um das Lektorat und die Veröffentlichung.'
    }
  };

  teamList.addEventListener('click', e => {
    const memberDiv = e.target.closest('.team-member');
    if (!memberDiv) return;
    const
