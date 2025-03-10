<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  
  let visible = false;
  
  onMount(() => {
    visible = true;
  });
  
  const benefits = [
    {
      title: "¿Cómo?",
      description: "Ofrecemos una solución única con pasto y madera de alta calidad, colores, texturas y personalización que se adaptan a las necesidades de cada cliente y sus mascotas. Nuestro diseño elegante pero vibrante combina funcionalidad y estética para un hogar armonioso.",
      image: "/img/como.jpg"
    },
    {
      title: "¿Qué ofrecemos?",
      description: "Nuestra oferta garantiza un espacio especial y cómodo para tus mascotas, proporcionando comodidad, frescura, elegancia y diversión. Wawi Spot es más que un producto, es una marca amiga que convierte cualquier lugar en el espacio favorito de tus adorados wawis.",
      image: "/img/que-ofrecemos.jpg"
    },
    {
      title: "¿Por qué?",
      description: "En Wawi Spot, entendemos la necesidad de brindar tranquilidad y confianza a los dueños de mascotas. Queremos asegurarnos de que, al regresar a casa, no habrá desastres y tus pequeños tendrán un espacio propio que les encante.",
      image: "/img/por-que.jpg"
    }
  ];
  
  const testimonials = [
    {
      quote: "Mi perro siempre tenía problemas para adaptarse a los baños tradicionales. Con Wawi Spot, ahora tiene su espacio favorito y ya no hay accidentes en casa. ¡Es increíble!",
      author: "Marina Sanchez",
      image: "/img/testimonial1.jpg"
    },
    {
      quote: "La diferencia en los olores es increíble. Mi apartamento ya no huele a bandeja sanitaria, y mi perro parece mucho más feliz.",
      author: "Rolando Flores",
      image: "/img/testimonial4.jpg"
    }
  ];
  
  // Información de mantenimiento
  const maintenance = {
    title: "Mantenimiento",
    description: "Luego del tiempo de vida útil de nuestra pasto, te lo cambiamos por uno nuevo:",
    prices: [
      { name: "Paquete Shaq", price: "20$" },
      { name: "Paquete Balú", price: "25$" },
      { name: "Paquete Cooper", price: "30$" }
    ],
    note: "La duración del pasto es de 25 a 30 días según su cuidado",
    image: "/img/mantenimiento.jpg"
  };
</script>

<!-- Hero Section -->
<section class="py-12 md:py-16 bg-primary/5">
  <div class="container mx-auto px-4">
    {#if visible}
      <div class="max-w-3xl mx-auto text-center" in:fade={{duration: 800}}>
        <h1 class="text-2xl md:text-4xl lg:text-5xl font-bold mb-4 md:mb-6 text-dark">Beneficios de <span class="text-primary">Wawi Spot</span></h1>
        <p class="text-base md:text-xl text-gray-700 mb-6 md:mb-8">
          Descubre por qué Wawi Spot es la mejor opción para tu mascota, tu hogar y el medio ambiente.
        </p>
      </div>
    {/if}
  </div>
</section>

<!-- Beneficios Sections -->
{#each benefits as benefit, i}
  <section class="py-12 md:py-16 {i % 2 === 1 ? 'bg-gray-50' : ''}">
    <div class="container mx-auto px-4">
      {#if visible}
        <div class="flex flex-col md:flex-row items-center gap-6 md:gap-8 {i % 2 === 1 ? 'md:flex-row-reverse' : ''}">
          <div class="w-full md:w-1/2"
            in:fly={{y: 30, duration: 800, delay: 200 * i}}>
            <img 
              src={benefit.image} 
              alt={benefit.title} 
              class="w-full h-auto rounded-lg shadow-lg"
            >
          </div>
          <div class="w-full md:w-1/2 mt-6 md:mt-0"
            in:fly={{y: 30, duration: 800, delay: 200 * i + 100}}>
            <h2 class="text-2xl md:text-3xl font-bold mb-4 md:mb-6 text-primary">{benefit.title}</h2>
            <p class="text-base md:text-lg text-gray-700 mb-4 md:mb-6">{benefit.description}</p>
          </div>
        </div>
      {/if}
    </div>
  </section>
{/each}

<!-- Mantenimiento Section -->
<section class="py-12 md:py-16 bg-gray-50">
  <div class="container mx-auto px-4">
    {#if visible}
      <div class="flex flex-col md:flex-row items-center gap-6 md:gap-8">
        <div class="w-full md:w-1/2"
          in:fly={{y: 30, duration: 800}}>
          <img 
            src={maintenance.image} 
            alt={maintenance.title} 
            class="w-full h-auto rounded-lg shadow-lg"
          >
        </div>
        <div class="w-full md:w-1/2 mt-6 md:mt-0"
          in:fly={{y: 30, duration: 800, delay: 100}}>
          <h2 class="text-2xl md:text-3xl font-bold mb-4 md:mb-6 text-primary">{maintenance.title}</h2>
          <p class="text-base md:text-lg text-gray-700 mb-4 md:mb-6">{maintenance.description}</p>
          <ul class="space-y-2 md:space-y-3 mb-4 md:mb-6">
            {#each maintenance.prices as price}
              <li class="flex items-center text-base md:text-lg">
                <span class="text-primary mr-2">•</span>
                <span>{price.name}: <strong>{price.price}</strong></span>
              </li>
            {/each}
          </ul>
          <div class="bg-primary/10 p-3 md:p-4 rounded-lg border-l-4 border-primary">
            <p class="text-sm md:text-base text-gray-700 italic">{maintenance.note}</p>
          </div>
        </div>
      </div>
    {/if}
  </div>
</section>

<!-- Comparación Section -->
<section class="py-12 md:py-16">
  <div class="container mx-auto px-4">
    {#if visible}
      <h2 
        class="text-2xl md:text-3xl font-bold mb-8 md:mb-12 text-center"
        in:fly={{y: 30, duration: 800}}
      >
        Wawi Spot vs. Bandejas Tradicionales
      </h2>
      
      <div class="overflow-x-auto" in:fade={{duration: 800, delay: 200}}>
        <table class="w-full bg-white rounded-lg shadow-md overflow-hidden">
          <thead class="bg-primary text-white">
            <tr>
              <th class="py-3 md:py-4 px-4 md:px-6 text-left text-sm md:text-base">Característica</th>
              <th class="py-3 md:py-4 px-4 md:px-6 text-center text-sm md:text-base">Wawi Spot</th>
              <th class="py-3 md:py-4 px-4 md:px-6 text-center text-sm md:text-base">Bandejas Tradicionales</th>
            </tr>
          </thead>
          <tbody>
            <tr class="border-b">
              <td class="py-3 md:py-4 px-4 md:px-6 font-medium text-sm md:text-base">Control de olores</td>
              <td class="py-3 md:py-4 px-4 md:px-6 text-center text-green-600">
                <svg class="w-5 h-5 md:w-6 md:h-6 mx-auto" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path>
                </svg>
                <span class="block mt-1 text-xs md:text-sm">Excelente</span>
              </td>
              <td class="py-3 md:py-4 px-4 md:px-6 text-center text-yellow-600">
                <svg class="w-5 h-5 md:w-6 md:h-6 mx-auto" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm-1-9a1 1 0 011-1h.01a1 1 0 110 2H10a1 1 0 01-1-1z" clip-rule="evenodd"></path>
                </svg>
                <span class="block mt-1 text-xs md:text-sm">Moderado</span>
              </td>
            </tr>
            <tr class="border-b">
              <td class="py-3 md:py-4 px-4 md:px-6 font-medium text-sm md:text-base">Impacto ambiental</td>
              <td class="py-3 md:py-4 px-4 md:px-6 text-center text-green-600">
                <svg class="w-5 h-5 md:w-6 md:h-6 mx-auto" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path>
                </svg>
                <span class="block mt-1 text-xs md:text-sm">Mínimo</span>
              </td>
              <td class="py-3 md:py-4 px-4 md:px-6 text-center text-red-600">
                <svg class="w-5 h-5 md:w-6 md:h-6 mx-auto" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path>
                </svg>
                <span class="block mt-1 text-xs md:text-sm">Alto</span>
              </td>
            </tr>
            <tr class="border-b">
              <td class="py-3 md:py-4 px-4 md:px-6 font-medium text-sm md:text-base">Salud de la mascota</td>
              <td class="py-3 md:py-4 px-4 md:px-6 text-center text-green-600">
                <svg class="w-5 h-5 md:w-6 md:h-6 mx-auto" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path>
                </svg>
                <span class="block mt-1 text-xs md:text-sm">Óptima</span>
              </td>
              <td class="py-3 md:py-4 px-4 md:px-6 text-center text-yellow-600">
                <svg class="w-5 h-5 md:w-6 md:h-6 mx-auto" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm-1-9a1 1 0 011-1h.01a1 1 0 110 2H10a1 1 0 01-1-1z" clip-rule="evenodd"></path>
                </svg>
                <span class="block mt-1 text-xs md:text-sm">Variable</span>
              </td>
            </tr>
            <tr class="border-b">
              <td class="py-3 md:py-4 px-4 md:px-6 font-medium text-sm md:text-base">Mantenimiento diario</td>
              <td class="py-3 md:py-4 px-4 md:px-6 text-center text-green-600">
                <svg class="w-5 h-5 md:w-6 md:h-6 mx-auto" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path>
                </svg>
                <span class="block mt-1 text-xs md:text-sm">Mínimo</span>
              </td>
              <td class="py-3 md:py-4 px-4 md:px-6 text-center text-red-600">
                <svg class="w-5 h-5 md:w-6 md:h-6 mx-auto" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path>
                </svg>
                <span class="block mt-1 text-xs md:text-sm">Frecuente</span>
              </td>
            </tr>
            <tr>
              <td class="py-3 md:py-4 px-4 md:px-6 font-medium text-sm md:text-base">Estética</td>
              <td class="py-3 md:py-4 px-4 md:px-6 text-center text-green-600">
                <svg class="w-5 h-5 md:w-6 md:h-6 mx-auto" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path>
                </svg>
                <span class="block mt-1 text-xs md:text-sm">Natural y atractiva</span>
              </td>
              <td class="py-3 md:py-4 px-4 md:px-6 text-center text-yellow-600">
                <svg class="w-5 h-5 md:w-6 md:h-6 mx-auto" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm-1-9a1 1 0 011-1h.01a1 1 0 110 2H10a1 1 0 01-1-1z" clip-rule="evenodd"></path>
                </svg>
                <span class="block mt-1 text-xs md:text-sm">Artificial</span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    {/if}
  </div>
</section>

<!-- Testimonios Section -->
<section class="py-12 md:py-16 bg-gray-50">
  <div class="container mx-auto px-4">
    {#if visible}
      <h2 
        class="text-2xl md:text-3xl font-bold mb-8 md:mb-12 text-center"
        in:fly={{y: 30, duration: 800}}
      >
        Lo que dicen nuestros clientes
      </h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 md:gap-8">
        {#each testimonials as testimonial, i}
          <div 
            class="bg-white rounded-lg shadow-md p-5 md:p-8 relative"
            in:fly={{y: 30, duration: 800, delay: 200 * i}}
          >
            <svg class="w-10 h-10 md:w-12 md:h-12 text-primary/20 absolute top-5 md:top-6 left-5 md:left-6" fill="currentColor" viewBox="0 0 24 24">
              <path d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-9.983zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h3.983v10h-9.983z" />
            </svg>
            <div class="relative z-10">
              <p class="text-base md:text-lg italic mb-4 md:mb-6 text-gray-700 pl-8 md:pl-10">{testimonial.quote}</p>
              <div class="flex items-center">
                <div class="w-10 h-10 md:w-12 md:h-12 rounded-full overflow-hidden mr-3 md:mr-4">
                  <img src={testimonial.image} alt={testimonial.author} class="w-full h-full object-cover">
                </div>
                <span class="font-semibold text-sm md:text-base">{testimonial.author}</span>
              </div>
            </div>
          </div>
        {/each}
      </div>
    {/if}
  </div>
</section>

<!-- CTA Section -->
<section class="py-12 md:py-16 bg-primary text-white">
  <div class="container mx-auto px-4 text-center">
    {#if visible}
      <div in:fade={{duration: 800}}>
        <h2 class="text-2xl md:text-3xl font-bold mb-4 md:mb-6">Experimenta los beneficios de Wawi Spot</h2>
        <p class="text-base md:text-xl mb-6 md:mb-8 max-w-2xl mx-auto">
          Tu mascota merece lo mejor. Haz tu pedido hoy y descubre la diferencia.
        </p>
        <a 
          href="/contacto" 
          class="inline-block bg-white text-primary hover:bg-gray-100 font-medium py-2.5 md:py-3 px-6 md:px-8 rounded-full transition-all duration-300 transform hover:scale-105 hover:shadow-lg text-base md:text-lg"
        >
          ¡Haz tu pedido ahora!
        </a>
      </div>
    {/if}
  </div>
</section> 