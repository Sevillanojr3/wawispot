<script>
  import { onMount } from 'svelte';
  import { fade, fly, scale } from 'svelte/transition';
  import { backOut } from 'svelte/easing';

  let visible = false;
  let testimonials = [
    {
      name: "Carlos Rodríguez",
      text: "Mi perro adora su Wawi Spot. Ya no tengo que preocuparme por los olores en casa.",
      image: "/img/testimonial1.jpg"
    },
    {
      name: "María González",
      text: "La mejor inversión para mi mascota. El pasto natural es mucho mejor que las alternativas sintéticas.",
      image: "/img/testimonial2.jpg"
    },
    {
      name: "Juan Pérez",
      text: "El servicio de entrega es excelente y mi gato se adaptó rápidamente a su nueva bandeja.",
      image: "/img/testimonial3.jpg"
    }
  ];

  // Añadir información de paquetes para mostrar en la página principal
  const packages = [
    { 
      name: "Paquete Shaq", 
      dimensions: "60 x 45 cm", 
      price: "$59.95",
      image: "/img/shaq.jpg"
    },
    { 
      name: "Paquete Balú", 
      dimensions: "90 x 50 cm", 
      price: "$69.95",
      image: "/img/balu.jpg"
    },
    { 
      name: "Paquete Cooper", 
      dimensions: "100 x 75 cm", 
      price: "$79.95",
      image: "/img/cooper.jpg"
    }
  ];

  onMount(() => {
    visible = true;
    
    // Inicializar contador para estadísticas
    const counters = document.querySelectorAll('.counter');
    const speed = 200;
    
    const startCounting = (entries, observer) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          const counter = entry.target;
          const target = +counter.getAttribute('data-target');
          let count = 0;
          
          const updateCount = () => {
            const increment = target / speed;
            if (count < target) {
              count += increment;
              counter.innerText = Math.ceil(count);
              setTimeout(updateCount, 1);
            } else {
              counter.innerText = target;
            }
          };
          
          updateCount();
          observer.unobserve(counter);
        }
      });
    };
    
    const observer = new IntersectionObserver(startCounting, {
      threshold: 0.4
    });
    
    counters.forEach(counter => {
      observer.observe(counter);
    });

    // Smooth scroll para los enlaces de navegación
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function(e) {
        e.preventDefault();
        const href = this.getAttribute('href');
        if (href) {
          const element = document.querySelector(href);
          if (element) {
            element.scrollIntoView({
              behavior: 'smooth'
            });
          }
        }
      });
    });
  });
</script>

<!-- Hero Section -->
<section id="inicio" class="relative min-h-screen flex items-center justify-center overflow-hidden">
  <div class="absolute inset-0 z-0">
    <div class="absolute inset-0 bg-black/60 z-10"></div>
    <video autoplay muted loop playsinline class="absolute inset-0 w-full h-full object-cover">
      <source src="/video/video1.mp4" type="video/mp4">
    </video>
  </div>
  
  <div class="relative z-20 text-center px-4 max-w-4xl mx-auto py-16 md:py-0">
    {#if visible}
      <img 
        src="/img/logonf.PNG" 
        alt="Wawi Spot Logo" 
        class="w-48 md:w-64 lg:w-80 mx-auto mb-6 md:mb-8"
        in:scale={{duration: 1000, delay: 200, easing: backOut}}
      >
      <h1 
        class="text-3xl md:text-5xl lg:text-6xl font-bold text-white mb-4 md:mb-6"
        in:fly={{y: 50, duration: 1000, delay: 500}}
      >
        Bandeja Sanitaria Natural
      </h1>
      <p 
        class="text-lg md:text-xl lg:text-2xl text-white mb-8 md:mb-10 max-w-2xl mx-auto"
        in:fly={{y: 50, duration: 1000, delay: 700}}
      >
        La solución ecológica y saludable para tu mascota. Pasto 100% natural que mantiene tu hogar limpio y libre de olores.
      </p>
      <div class="flex flex-col sm:flex-row justify-center gap-4 sm:gap-6" in:fade={{duration: 1000, delay: 1000}}>
        <a 
          href="/producto" 
          class="inline-block bg-primary hover:bg-primary/90 text-white font-medium py-3 px-8 rounded-full transition-all duration-300 transform hover:scale-105 hover:shadow-lg"
        >
          Conoce el producto
        </a>
        <a 
          href="/contacto" 
          class="inline-block bg-white hover:bg-gray-100 text-primary font-medium py-3 px-8 rounded-full transition-all duration-300 transform hover:scale-105 hover:shadow-lg"
        >
          Haz tu pedido
        </a>
      </div>
    {/if}
  </div>
  
  <div class="absolute bottom-10 left-0 right-0 z-20 text-center hidden md:block">
    <a href="#caracteristicas" class="text-white animate-bounce inline-block">
      <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3"></path>
      </svg>
    </a>
  </div>
</section>

<!-- Características Section -->
<section id="caracteristicas" class="py-16 md:py-20 bg-gray-50">
  <div class="container mx-auto px-4">
    <h2 class="text-2xl md:text-3xl lg:text-4xl font-bold text-center mb-10 md:mb-16 text-dark">¿Por qué elegir <span class="text-primary">Wawi Spot</span>?</h2>
    
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 md:gap-10">
      <div class="bg-white rounded-lg shadow-md p-6 md:p-8 text-center transform transition-all duration-300 hover:-translate-y-2 hover:shadow-xl">
        <div class="bg-primary/10 w-16 h-16 md:w-20 md:h-20 rounded-full flex items-center justify-center mx-auto mb-4 md:mb-6">
          <svg class="w-8 h-8 md:w-10 md:h-10 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
          </svg>
        </div>
        <h3 class="text-lg md:text-xl font-semibold mb-3 md:mb-4">100% Natural</h3>
        <p class="text-gray-600">Pasto real cultivado especialmente para mascotas. Sin químicos ni materiales sintéticos.</p>
      </div>
      
      <div class="bg-white rounded-lg shadow-md p-6 md:p-8 text-center transform transition-all duration-300 hover:-translate-y-2 hover:shadow-xl">
        <div class="bg-primary/10 w-16 h-16 md:w-20 md:h-20 rounded-full flex items-center justify-center mx-auto mb-4 md:mb-6">
          <svg class="w-8 h-8 md:w-10 md:h-10 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"></path>
          </svg>
        </div>
        <h3 class="text-lg md:text-xl font-semibold mb-3 md:mb-4">Saludable</h3>
        <p class="text-gray-600">Reduce el estrés de tu mascota y previene problemas de salud asociados con bandejas tradicionales.</p>
      </div>
      
      <div class="bg-white rounded-lg shadow-md p-6 md:p-8 text-center transform transition-all duration-300 hover:-translate-y-2 hover:shadow-xl">
        <div class="bg-primary/10 w-16 h-16 md:w-20 md:h-20 rounded-full flex items-center justify-center mx-auto mb-4 md:mb-6">
          <svg class="w-8 h-8 md:w-10 md:h-10 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 6l3 1m0 0l-3 9a5.002 5.002 0 006.001 0M6 7l3 9M6 7l6-2m6 2l3-1m-3 1l-3 9a5.002 5.002 0 006.001 0M18 7l3 9m-3-9l-6-2m0-2v2m0 16V5m0 16H9m3 0h3"></path>
          </svg>
        </div>
        <h3 class="text-lg md:text-xl font-semibold mb-3 md:mb-4">Ecológico</h3>
        <p class="text-gray-600">Biodegradable y respetuoso con el medio ambiente. Reduce tu huella de carbono.</p>
      </div>
    </div>
  </div>
</section>

<!-- Estadísticas Section -->
<section class="py-12 md:py-16 bg-primary text-white">
  <div class="container mx-auto px-4">
    <div class="grid grid-cols-1 sm:grid-cols-3 gap-8 text-center">
      <div>
        <h3 class="text-3xl md:text-4xl font-bold mb-2"><span class="counter" data-target="500">0</span>+</h3>
        <p class="text-lg md:text-xl">Clientes satisfechos</p>
      </div>
      <div>
        <h3 class="text-3xl md:text-4xl font-bold mb-2"><span class="counter" data-target="1200">0</span>+</h3>
        <p class="text-lg md:text-xl">Bandejas entregadas</p>
      </div>
      <div>
        <h3 class="text-3xl md:text-4xl font-bold mb-2"><span class="counter" data-target="98">0</span>%</h3>
        <p class="text-lg md:text-xl">Tasa de satisfacción</p>
      </div>
    </div>
  </div>
</section>

<!-- Paquetes Section -->
<section class="py-16 md:py-20 bg-gray-50">
  <div class="container mx-auto px-4">
    <h2 class="text-2xl md:text-3xl lg:text-4xl font-bold text-center mb-10 md:mb-16 text-dark">Nuestros <span class="text-primary">Paquetes</span></h2>
    
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 md:gap-8">
      {#each packages as pack, i}
        <div 
          class="bg-white rounded-lg shadow-lg overflow-hidden transform transition-all duration-300 hover:-translate-y-2 hover:shadow-xl"
          in:fly={{y: 50, duration: 800, delay: 200 * i}}
        >
          <div class="h-40 md:h-48 overflow-hidden">
            <img src={pack.image} alt={pack.name} class="w-full h-full object-cover">
          </div>
          <div class="p-5 md:p-6">
            <h3 class="text-xl md:text-2xl font-bold mb-2 text-primary">{pack.name}</h3>
            <p class="text-gray-600 mb-2">Dimensiones: {pack.dimensions}</p>
            <p class="text-2xl md:text-3xl font-bold mb-4">{pack.price}</p>
            <a 
              href="/producto" 
              class="block text-center bg-primary hover:bg-primary/90 text-white font-medium py-2 md:py-3 px-6 rounded-full transition-all duration-300"
            >
              Ver detalles
            </a>
          </div>
        </div>
      {/each}
    </div>
    
    <div class="text-center mt-8 md:mt-10">
      <a 
        href="/producto" 
        class="inline-block bg-white border-2 border-primary text-primary hover:bg-primary/10 font-medium py-2 md:py-3 px-6 md:px-8 rounded-full transition-all duration-300"
      >
        Ver todos los detalles
      </a>
    </div>
  </div>
</section>

<!-- Entregas Section -->
<section class="py-12 md:py-16 bg-white">
  <div class="container mx-auto px-4">
    <div class="flex flex-col md:flex-row items-center gap-8 md:gap-12">
      <div class="w-full md:w-1/2">
        {#if visible}
          <div in:fly={{y: 30, duration: 800}}>
            <h2 class="text-2xl md:text-3xl lg:text-4xl font-bold mb-4 md:mb-6 text-primary">Entregas</h2>
            <p class="text-base md:text-lg text-gray-700 mb-4 md:mb-6">
              El servicio de entrega se estará realizando en un periodo de 7 días posterior a su pago, hasta la puerta de su domicilio.
            </p>
            <div class="bg-primary/10 p-4 md:p-5 rounded-lg border-l-4 border-primary">
              <p class="text-gray-700 font-medium">Todos los paquetes incluyen delivery e instalación gratis</p>
            </div>
          </div>
        {/if}
      </div>
      <div class="w-full md:w-1/2">
        {#if visible}
          <div 
            class="bg-white rounded-lg shadow-xl p-6 md:p-8 text-center"
            in:fly={{y: 30, duration: 800, delay: 200}}
          >
            <div class="w-20 h-20 md:w-24 md:h-24 bg-primary/10 rounded-full flex items-center justify-center mx-auto mb-4 md:mb-6">
              <svg class="w-10 h-10 md:w-12 md:h-12 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path d="M9 17a2 2 0 11-4 0 2 2 0 014 0zM19 17a2 2 0 11-4 0 2 2 0 014 0z"></path>
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16V6a1 1 0 00-1-1H4a1 1 0 00-1 1v10a1 1 0 001 1h1m8-1a1 1 0 01-1 1H9m4-1V8a1 1 0 011-1h2.586a1 1 0 01.707.293l3.414 3.414a1 1 0 01.293.707V16a1 1 0 01-1 1h-1m-6-1a1 1 0 001 1h1M5 17a2 2 0 104 0m-4 0a2 2 0 114 0m6 0a2 2 0 104 0m-4 0a2 2 0 114 0"></path>
              </svg>
            </div>
            <h3 class="text-xl md:text-2xl font-bold mb-3 md:mb-4">Entrega a domicilio</h3>
            <p class="text-gray-600 mb-4 md:mb-6">
              Recibe tu Wawi Spot directamente en la puerta de tu casa, sin complicaciones y con instalación incluida.
            </p>
            <a 
              href="/contacto" 
              class="inline-block bg-primary hover:bg-primary/90 text-white font-medium py-2 md:py-3 px-6 md:px-8 rounded-full transition-all duration-300"
            >
              Haz tu pedido
            </a>
          </div>
        {/if}
      </div>
    </div>
  </div>
</section>

<!-- Mantenimiento Section -->
<section class="py-12 md:py-16 bg-gray-50">
  <div class="container mx-auto px-4">
    <div class="flex flex-col md:flex-row items-center gap-8 md:gap-12">
      <div class="w-full md:w-1/2 order-2 md:order-1">
        {#if visible}
          <div 
            class="bg-white rounded-lg shadow-xl overflow-hidden"
            in:fly={{y: 30, duration: 800}}
          >
            <img 
              src="/img/mantenimiento.jpg" 
              alt="Mantenimiento Wawi Spot" 
              class="w-full h-auto"
            >
            <div class="p-6 md:p-8">
              <h3 class="text-xl md:text-2xl font-bold mb-3 md:mb-4">Servicio de mantenimiento</h3>
              <p class="text-gray-600 mb-4 md:mb-6">
                Nos encargamos de mantener tu Wawi Spot siempre fresco y en perfectas condiciones para tu mascota.
              </p>
              <div class="bg-green-50 p-3 md:p-4 rounded-lg border-l-4 border-green-500">
                <p class="text-sm md:text-base italic text-gray-700">La duración del pasto es de 25 a 30 días según su cuidado</p>
              </div>
            </div>
          </div>
        {/if}
      </div>
      <div class="w-full md:w-1/2 order-1 md:order-2">
        {#if visible}
          <div in:fly={{y: 30, duration: 800, delay: 200}}>
            <h2 class="text-2xl md:text-3xl lg:text-4xl font-bold mb-4 md:mb-6 text-primary">Mantenimiento</h2>
            <p class="text-base md:text-lg text-gray-700 mb-4 md:mb-6">
              Luego del tiempo de vida útil de nuestra pasto, te lo cambiamos por uno nuevo:
            </p>
            <ul class="space-y-3 md:space-y-4 mb-6 md:mb-8">
              <li class="flex items-center text-base md:text-lg">
                <span class="w-7 h-7 md:w-8 md:h-8 bg-primary/10 rounded-full flex items-center justify-center mr-3">
                  <span class="text-primary font-bold">1</span>
                </span>
                <span>Paquete Shaq: <strong class="text-primary">20$</strong></span>
              </li>
              <li class="flex items-center text-base md:text-lg">
                <span class="w-7 h-7 md:w-8 md:h-8 bg-primary/10 rounded-full flex items-center justify-center mr-3">
                  <span class="text-primary font-bold">2</span>
                </span>
                <span>Paquete Balú: <strong class="text-primary">25$</strong></span>
              </li>
              <li class="flex items-center text-base md:text-lg">
                <span class="w-7 h-7 md:w-8 md:h-8 bg-primary/10 rounded-full flex items-center justify-center mr-3">
                  <span class="text-primary font-bold">3</span>
                </span>
                <span>Paquete Cooper: <strong class="text-primary">30$</strong></span>
              </li>
            </ul>
            <a 
              href="/contacto" 
              class="inline-block bg-primary hover:bg-primary/90 text-white font-medium py-2 md:py-3 px-6 md:px-8 rounded-full transition-all duration-300"
            >
              Solicitar mantenimiento
            </a>
          </div>
        {/if}
      </div>
    </div>
  </div>
</section>

<!-- Testimonios Section -->
<section class="py-16 md:py-20">
  <div class="container mx-auto px-4">
    <h2 class="text-2xl md:text-3xl lg:text-4xl font-bold text-center mb-10 md:mb-16 text-dark">Lo que dicen nuestros clientes</h2>
    
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 md:gap-8">
      {#each testimonials as testimonial, i}
        <div 
          class="bg-white rounded-lg shadow-md overflow-hidden transition-transform duration-300 hover:shadow-xl"
          in:fly={{y: 50, duration: 800, delay: 300 * i}}
        >
          <div class="p-5 md:p-6">
            <div class="flex items-center mb-3 md:mb-4">
              <div class="w-10 h-10 md:w-12 md:h-12 rounded-full overflow-hidden mr-3 md:mr-4">
                <img src={testimonial.image} alt={testimonial.name} class="w-full h-full object-cover">
              </div>
              <h3 class="font-semibold">{testimonial.name}</h3>
            </div>
            <p class="text-gray-600 italic text-sm md:text-base">"{testimonial.text}"</p>
            <div class="mt-3 md:mt-4 flex text-yellow-400">
              <svg class="w-4 h-4 md:w-5 md:h-5" fill="currentColor" viewBox="0 0 20 20">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
              </svg>
              <svg class="w-4 h-4 md:w-5 md:h-5" fill="currentColor" viewBox="0 0 20 20">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
              </svg>
              <svg class="w-4 h-4 md:w-5 md:h-5" fill="currentColor" viewBox="0 0 20 20">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
              </svg>
              <svg class="w-4 h-4 md:w-5 md:h-5" fill="currentColor" viewBox="0 0 20 20">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
              </svg>
              <svg class="w-4 h-4 md:w-5 md:h-5" fill="currentColor" viewBox="0 0 20 20">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
              </svg>
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- CTA Section -->
<section class="py-16 md:py-20 bg-gray-900 text-white">
  <div class="container mx-auto px-4 text-center">
    <h2 class="text-2xl md:text-3xl lg:text-4xl font-bold mb-4 md:mb-6">¿Listo para mejorar la vida de tu mascota?</h2>
    <p class="text-lg md:text-xl mb-8 md:mb-10 max-w-2xl mx-auto">Haz tu pedido hoy y recibe tu Wawi Spot directamente en tu puerta. Tu mascota te lo agradecerá.</p>
    <a 
      href="/contacto" 
      class="inline-block bg-primary hover:bg-primary/90 text-white font-medium py-3 md:py-4 px-8 md:px-10 rounded-full text-base md:text-lg transition-all duration-300 transform hover:scale-105 hover:shadow-lg"
    >
      ¡Haz tu pedido ahora!
    </a>
  </div>
</section>

<style>
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(-20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
</style>
