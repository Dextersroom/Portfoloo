const cursorGlow = document.querySelector('.cursor-glow');
const magneticItems = document.querySelectorAll('.magnetic');
const revealItems = document.querySelectorAll('.reveal');
const navToggle = document.querySelector('.nav-toggle');
const navLinks = document.querySelector('.nav-links');

let cursorX = window.innerWidth / 2;
let cursorY = window.innerHeight / 2;
let glowX = cursorX;
let glowY = cursorY;

window.addEventListener('pointermove', (event) => {
  cursorX = event.clientX;
  cursorY = event.clientY;
});

function animateCursor() {
  glowX += (cursorX - glowX) * 0.12;
  glowY += (cursorY - glowY) * 0.12;
  cursorGlow.style.transform = `translate(${glowX - 110}px, ${glowY - 110}px)`;
  requestAnimationFrame(animateCursor);
}
animateCursor();

magneticItems.forEach((item) => {
  item.addEventListener('pointerenter', () => cursorGlow.classList.add('is-active'));
  item.addEventListener('pointerleave', () => {
    cursorGlow.classList.remove('is-active');
    item.style.transform = '';
  });
  item.addEventListener('pointermove', (event) => {
    const rect = item.getBoundingClientRect();
    const moveX = (event.clientX - rect.left - rect.width / 2) * 0.18;
    const moveY = (event.clientY - rect.top - rect.height / 2) * 0.18;
    item.style.transform = `translate(${moveX}px, ${moveY}px)`;
  });
});

const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      entry.target.classList.add('is-visible');
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.18 });

revealItems.forEach((item, index) => {
  item.style.transitionDelay = `${Math.min(index * 70, 280)}ms`;
  observer.observe(item);
});

navToggle.addEventListener('click', () => {
  const isOpen = navLinks.classList.toggle('is-open');
  navToggle.setAttribute('aria-expanded', String(isOpen));
});

navLinks.querySelectorAll('a').forEach((link) => {
  link.addEventListener('click', () => {
    navLinks.classList.remove('is-open');
    navToggle.setAttribute('aria-expanded', 'false');
  });
});
