<script>
  import '../app.css';
  import { onMount } from 'svelte';
  import { page } from '$app/stores';
  import { fade, slide } from 'svelte/transition';

  let menuOpen = false;
  let scrolled = false;

  onMount(() => {
    // Detectar scroll para cambiar el estilo del navbar
    window.addEventListener('scroll', () => {
      scrolled = window.scrollY > 20;
    });
  });

  // Función para cerrar el menú al hacer clic en un enlace
  function closeMenu() {
    menuOpen = false;
  }
</script>

<div class="min-h-screen flex flex-col">
  <header class="bg-white shadow-md fixed w-full top-0 z-50 transition-all duration-300 {scrolled ? 'py-2' : 'py-3'}">
    <nav class="container mx-auto px-4 flex justify-between items-center">
      <div class="logo">
        <a href="/" class="flex items-center">
          <img src="/img/logo_titulo.PNG" alt="Wawi Spot Logo" class="h-10 md:h-16 transition-transform duration-300 hover:scale-105">
        </a>
      </div>
      <button 
        class="menu-toggle md:hidden flex flex-col justify-center items-center w-10 h-10 space-y-1.5 cursor-pointer z-50 bg-primary/10 rounded-full p-2" 
        aria-label={menuOpen ? 'Cerrar menú' : 'Abrir menú'}
        aria-expanded={menuOpen}
        on:click={() => menuOpen = !menuOpen}
      >
        <span class="block w-6 h-0.5 bg-primary transition-all duration-300 {menuOpen ? 'rotate-45 translate-y-2' : ''}"></span>
        <span class="block w-6 h-0.5 bg-primary transition-all duration-300 {menuOpen ? 'opacity-0' : ''}"></span>
        <span class="block w-6 h-0.5 bg-primary transition-all duration-300 {menuOpen ? '-rotate-45 -translate-y-2' : ''}"></span>
      </button>
      <ul class="nav-links hidden md:flex space-x-6 font-medium">
        <li>
          <a href="/" class="flex items-center gap-2 text-dark hover:text-primary transition-colors duration-300 {$page.url.pathname === '/' ? 'text-primary font-bold' : ''}">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path>
            </svg>
            Inicio
          </a>
        </li>
        <li>
          <a href="/producto" class="flex items-center gap-2 text-dark hover:text-primary transition-colors duration-300 {$page.url.pathname === '/producto' ? 'text-primary font-bold' : ''}">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"></path>
            </svg>
            Producto
          </a>
        </li>
        <li>
          <a href="/beneficios" class="flex items-center gap-2 text-dark hover:text-primary transition-colors duration-300 {$page.url.pathname === '/beneficios' ? 'text-primary font-bold' : ''}">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
            </svg>
            Beneficios
          </a>
        </li>
        <li>
          <a href="/preguntas-frecuentes" class="flex items-center gap-2 text-dark hover:text-primary transition-colors duration-300 {$page.url.pathname === '/preguntas-frecuentes' ? 'text-primary font-bold' : ''}">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
            </svg>
            FAQ
          </a>
        </li>
        <li>
          <a href="/contacto" class="flex items-center gap-2 text-dark hover:text-primary transition-colors duration-300 {$page.url.pathname === '/contacto' ? 'text-primary font-bold' : ''}">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path>
            </svg>
            Contacto
          </a>
        </li>
      </ul>
    </nav>
    
    <!-- Menú móvil (desplegable hacia abajo) -->
    {#if menuOpen}
      <div 
        transition:fade={{ duration: 200 }}
        class="fixed inset-0 bg-black bg-opacity-50 z-40"
        on:click={closeMenu}
      ></div>
      
      <div 
        transition:slide={{ duration: 300, axis: 'y' }}
        class="absolute top-full left-0 right-0 bg-white shadow-lg z-40 md:hidden"
      >
        <div class="py-4 px-6">
          <ul class="space-y-0">
            <li class="border-b">
              <a href="/" class="flex items-center gap-3 py-3 {$page.url.pathname === '/' ? 'text-primary font-bold' : ''}" on:click={closeMenu}>
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path>
                </svg>
                Inicio
              </a>
            </li>
            <li class="border-b">
              <a href="/producto" class="flex items-center gap-3 py-3 {$page.url.pathname === '/producto' ? 'text-primary font-bold' : ''}" on:click={closeMenu}>
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"></path>
                </svg>
                Producto
              </a>
            </li>
            <li class="border-b">
              <a href="/beneficios" class="flex items-center gap-3 py-3 {$page.url.pathname === '/beneficios' ? 'text-primary font-bold' : ''}" on:click={closeMenu}>
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                </svg>
                Beneficios
              </a>
            </li>
            <li class="border-b">
              <a href="/preguntas-frecuentes" class="flex items-center gap-3 py-3 {$page.url.pathname === '/preguntas-frecuentes' ? 'text-primary font-bold' : ''}" on:click={closeMenu}>
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                </svg>
                FAQ
              </a>
            </li>
            <li>
              <a href="/contacto" class="flex items-center gap-3 py-3 {$page.url.pathname === '/contacto' ? 'text-primary font-bold' : ''}" on:click={closeMenu}>
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path>
                </svg>
                Contacto
              </a>
            </li>
          </ul>
        </div>
      </div>
    {/if}
  </header>

  <main class="flex-grow pt-20">
    <slot />
  </main>

  <footer class="bg-dark text-white py-8">
    <div class="container mx-auto px-4">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <div>
          <h3 class="text-xl font-semibold mb-4">Wawi Spot</h3>
          <p class="mb-4">Bandeja sanitaria con pasto natural para tu mascota. La solución ecológica y saludable.</p>
          <div class="flex space-x-4">
            <a href="#" class="text-white hover:text-accent transition-colors duration-300">
              <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                <path fill-rule="evenodd" d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z" clip-rule="evenodd"></path>
              </svg>
            </a>
            <a href="#" class="text-white hover:text-accent transition-colors duration-300">
              <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                <path fill-rule="evenodd" d="M12.315 2c2.43 0 2.784.013 3.808.06 1.064.049 1.791.218 2.427.465a4.902 4.902 0 011.772 1.153 4.902 4.902 0 011.153 1.772c.247.636.416 1.363.465 2.427.048 1.067.06 1.407.06 4.123v.08c0 2.643-.012 2.987-.06 4.043-.049 1.064-.218 1.791-.465 2.427a4.902 4.902 0 01-1.153 1.772 4.902 4.902 0 01-1.772 1.153c-.636.247-1.363.416-2.427.465-1.067.048-1.407.06-4.123.06h-.08c-2.643 0-2.987-.012-4.043-.06-1.064-.049-1.791-.218-2.427-.465a4.902 4.902 0 01-1.772-1.153 4.902 4.902 0 01-1.153-1.772c-.247-.636-.416-1.363-.465-2.427-.047-1.024-.06-1.379-.06-3.808v-.63c0-2.43.013-2.784.06-3.808.049-1.064.218-1.791.465-2.427a4.902 4.902 0 011.153-1.772A4.902 4.902 0 015.45 2.525c.636-.247 1.363-.416 2.427-.465C8.901 2.013 9.256 2 11.685 2h.63zm-.081 1.802h-.468c-2.456 0-2.784.011-3.807.058-.975.045-1.504.207-1.857.344-.467.182-.8.398-1.15.748-.35.35-.566.683-.748 1.15-.137.353-.3.882-.344 1.857-.047 1.023-.058 1.351-.058 3.807v.468c0 2.456.011 2.784.058 3.807.045.975.207 1.504.344 1.857.182.466.399.8.748 1.15.35.35.683.566 1.15.748.353.137.882.3 1.857.344 1.054.048 1.37.058 4.041.058h.08c2.597 0 2.917-.01 3.96-.058.976-.045 1.505-.207 1.858-.344.466-.182.8-.398 1.15-.748.35-.35.566-.683.748-1.15.137-.353.3-.882.344-1.857.048-1.055.058-1.37.058-4.041v-.08c0-2.597-.01-2.917-.058-3.96-.045-.976-.207-1.505-.344-1.858a3.097 3.097 0 00-.748-1.15 3.098 3.098 0 00-1.15-.748c-.353-.137-.882-.3-1.857-.344-1.023-.047-1.351-.058-3.807-.058zM12 6.865a5.135 5.135 0 110 10.27 5.135 5.135 0 010-10.27zm0 1.802a3.333 3.333 0 100 6.666 3.333 3.333 0 000-6.666zm5.338-3.205a1.2 1.2 0 110 2.4 1.2 1.2 0 010-2.4z" clip-rule="evenodd"></path>
              </svg>
            </a>
          </div>
        </div>
        <div>
          <h3 class="text-xl font-semibold mb-4">Enlaces rápidos</h3>
          <ul class="space-y-2">
            <li class="flex items-center">
              <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
              </svg>
              <a href="/" class="hover:text-accent transition-colors duration-300">Inicio</a>
            </li>
            <li class="flex items-center">
              <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
              </svg>
              <a href="/producto" class="hover:text-accent transition-colors duration-300">Producto</a>
            </li>
            <li class="flex items-center">
              <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
              </svg>
              <a href="/beneficios" class="hover:text-accent transition-colors duration-300">Beneficios</a>
            </li>
            <li class="flex items-center">
              <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
              </svg>
              <a href="/preguntas-frecuentes" class="hover:text-accent transition-colors duration-300">Preguntas frecuentes</a>
            </li>
            <li class="flex items-center">
              <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
              </svg>
              <a href="/contacto" class="hover:text-accent transition-colors duration-300">Contacto</a>
            </li>
          </ul>
        </div>
        <div>
          <h3 class="text-xl font-semibold mb-4">Contacto</h3>
          <ul class="space-y-2">
            <li class="flex items-start">
              <svg class="w-5 h-5 mt-1 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
              </svg>
              <span>Panamá</span>
            </li>
            <li class="flex items-start">
              <svg class="w-5 h-5 mt-1 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path>
              </svg>
              <span>info@wawispot.com</span>
            </li>
            <li class="flex items-start">
              <svg class="w-5 h-5 mt-1 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path>
              </svg>
              <span>+507 6422-9334</span>
            </li>
          </ul>
        </div>
      </div>
      <div class="border-t border-gray-700 mt-8 pt-6 text-center">
        <p>&copy; {new Date().getFullYear()} Wawi Spot. Todos los derechos reservados.</p>
      </div>
    </div>
  </footer>
</div>

<style>
  /* Estilos para el menú móvil */
  @media (max-width: 768px) {
    .menu-toggle {
      display: flex;
    }
  }
</style> 