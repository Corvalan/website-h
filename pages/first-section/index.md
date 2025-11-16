[Home](https://Corvalan.github.io/website-h/) | [First Section](https://Corvalan.github.io/website-h/pages/first-section/) | [Second Section](https://Corvalan.github.io/website-h/pages/second-section/)

<div class="section-two-panel">

<div class="section-two-panel__sidebar" markdown="block">

## First Section

This is the body text of the Section. Lorem Psum asdfasdf

### Pages

- [Page A in first section](./Page-A-in-first-sect.html)
- [Page B in first section](./Page-B-in-first-sect.html)

</div>

<div class="section-two-panel__content">
  <iframe
    id="section-page-frame"
    class="section-two-panel__frame"
    src=""
    loading="lazy"
  ></iframe>
</div>

</div>

<style>
  .section-two-panel {
    display: flex;
    align-items: stretch;
    justify-content: space-between;
    min-height: 100vh; /* full viewport height */
    gap: 0;
  }

  .section-two-panel__sidebar,
  .section-two-panel__content {
    flex: 0 0 50%;
    max-width: 50%;
    box-sizing: border-box;
    padding-right: 1.5rem;
  }

  .section-two-panel__content {
    padding-right: 0;
    padding-left: 1.5rem;
    border-left: 1px solid #e0e0e0;
  }

  .section-two-panel__sidebar {
    font-size: 0.95rem;
    overflow-y: auto;
  }

  .section-two-panel__sidebar ul {
    list-style: none;
    padding-left: 0;
    margin-top: 0.5rem;
  }

  .section-two-panel__sidebar li {
    margin: 0.15rem 0;
  }

  .section-two-panel__sidebar a {
    text-decoration: none;
    display: block;
    padding: 0.15rem 0.25rem;
    border-radius: 4px;
  }

  .section-two-panel__sidebar a:hover {
    text-decoration: underline;
  }

  .section-two-panel__sidebar a.is-active {
    font-weight: 600;
  }

  .section-two-panel__frame {
    display: block;
    width: 100%;
    height: 100vh;        /* full viewport height */
    border: none;
    border-radius: 0;
  }

  @media (max-width: 900px) {
    .section-two-panel {
      flex-direction: column;
      min-height: auto;
    }

    .section-two-panel__sidebar,
    .section-two-panel__content {
      max-width: 100%;
      flex: 1 1 auto;
      padding: 0;
      border-left: none;
    }

    .section-two-panel__content {
      margin-top: 1rem;
    }

    .section-two-panel__frame {
      height: 60vh;
    }
  }
</style>

<script>
document.addEventListener('DOMContentLoaded', function () {
  var sidebar = document.querySelector('.section-two-panel__sidebar');
  if (!sidebar) return;

  var allLinks = Array.prototype.slice.call(
    sidebar.querySelectorAll('a[href]')
  );

  var links = allLinks.filter(function (a) {
    var href = a.getAttribute('href') || '';
    return !href.startsWith('http') && href.endsWith('.html');
  });

  if (!links.length) return;

  var frame = document.getElementById('section-page-frame');
  if (!frame) return;

  function openLink(link, pushHistory) {
    var href = link.getAttribute('href');
    if (!href) return;

    frame.setAttribute('src', href);

    links.forEach((a) => a.classList.remove('is-active'));
    link.classList.add('is-active');

    if (pushHistory && history.pushState) {
      var u = new URL(window.location.href);
      u.searchParams.set('page', href);
      history.pushState({ page: href }, '', u.toString());
    }
  }

  links.forEach((l) =>
    l.addEventListener('click', (e) => {
      e.preventDefault();
      openLink(l, true);
    })
  );

  var initial = null;
  try {
    var params = new URLSearchParams(window.location.search || '');
    var ph = params.get('page');
    if (ph) {
      initial = links.find((l) => l.getAttribute('href') === ph) || null;
    }
  } catch (e) {}

  if (!initial) initial = links[0];
  if (initial) openLink(initial, false);

  window.addEventListener('popstate', (ev) => {
    var href = ev.state && ev.state.page;
    if (!href) return;
    var link = links.find((l) => l.getAttribute('href') === href) || null;
    if (link) openLink(link, false);
  });
});
</script>

<style>
/* Global site tweaks */

body {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  line-height: 1.5;
}

/* Navigation bar (if you wrap nav_menu in a <p> or container) */
a {
  color: #0366d6;
}
a:hover {
  text-decoration: underline;
  color: red;
}

/* Active link style used in your section/page lists */
.section-two-panel__sidebar a.is-active {
  font-weight: 600;
  outline: none;
  border: none;
}

/* Optional: make inline "Home | Section" nav a bit nicer */
p:first-of-type a {
  margin-right: 0.25rem;
}
</style>
