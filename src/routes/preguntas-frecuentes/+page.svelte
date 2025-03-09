<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  
  let visible = false;
  let activeQuestion = null;
  
  onMount(() => {
    visible = true;
  });
  
  function toggleQuestion(index) {
    activeQuestion = activeQuestion === index ? null : index;
  }
  
  const faqs = [
    {
      category: "Sobre el producto",
      questions: [
        {
          question: "¿Qué es exactamente Wawi Spot?",
          answer: "Wawi Spot es una bandeja sanitaria para mascotas que utiliza pasto 100% natural en lugar de arena o materiales sintéticos. Está diseñada para proporcionar a tu mascota una experiencia más natural y saludable, mientras mantiene tu hogar limpio y libre de olores."
        },
        {
          question: "¿Para qué tipo de mascotas es adecuado Wawi Spot?",
          answer: "Wawi Spot es ideal para perros pequeños y medianos, así como para gatos. Es especialmente beneficioso para mascotas que pasan mucho tiempo en interiores o que tienen dificultades para salir con frecuencia."
        },
        {
          question: "¿Qué tamaños están disponibles?",
          answer: "Ofrecemos tres tamaños: Pequeño (40 x 30 cm), ideal para gatos y perros pequeños; Mediano (60 x 40 cm), recomendado para perros medianos; y Grande (80 x 60 cm), perfecto para perros grandes."
        },
        {
          question: "¿El pasto es real o artificial?",
          answer: "El pasto es 100% natural. Cultivamos nuestro propio pasto especialmente para mascotas, sin pesticidas ni químicos dañinos."
        }
      ]
    },
    {
      category: "Uso y mantenimiento",
      questions: [
        {
          question: "¿Cuánto tiempo dura el pasto?",
          answer: "Dependiendo del uso y del tamaño de tu mascota, el pasto puede durar entre 1 y 2 semanas. Factores como la frecuencia de uso, el tamaño de tu mascota y las condiciones ambientales pueden afectar la durabilidad."
        },
        {
          question: "¿Cómo se mantiene Wawi Spot?",
          answer: "El mantenimiento es sencillo. Recomendamos regar ligeramente el pasto cada 2-3 días para mantenerlo fresco, retirar los desechos sólidos diariamente y colocar la bandeja en un lugar con luz natural pero no directamente bajo el sol. Cuando notes que el pasto comienza a amarillear, es momento de reemplazarlo."
        },
        {
          question: "¿Cómo se reemplaza el pasto?",
          answer: "Ofrecemos un servicio de reemplazo de pasto. Simplemente solicita un nuevo pasto a través de nuestra página de contacto o WhatsApp, y te lo entregaremos directamente en tu puerta. También puedes optar por nuestros paquetes de suscripción para ahorrar en tus pedidos regulares."
        },
        {
          question: "¿Mi mascota se adaptará fácilmente a Wawi Spot?",
          answer: "La mayoría de las mascotas se adaptan rápidamente a Wawi Spot debido a su superficie natural. Para facilitar la transición, recomendamos colocar un poco de su arena o material anterior sobre el pasto durante los primeros días. También es útil colocar la bandeja en el mismo lugar donde tenían su bandeja anterior."
        }
      ]
    },
    {
      category: "Pedidos y entregas",
      questions: [
        {
          question: "¿Cómo puedo hacer un pedido?",
          answer: "Puedes hacer tu pedido a través de nuestra página de contacto o directamente por WhatsApp al +507 6422-9334. Simplemente indícanos el tamaño que necesitas y tu dirección de entrega."
        },
        {
          question: "¿Cuál es el tiempo de entrega?",
          answer: "Realizamos entregas en un plazo de 24 a 48 horas después de confirmar tu pedido, dependiendo de tu ubicación. Para áreas fuera de la ciudad, el tiempo de entrega puede ser mayor."
        },
        {
          question: "¿Ofrecen suscripciones o paquetes de reemplazo?",
          answer: "Sí, ofrecemos paquetes de reemplazo de pasto a precios especiales: Paquete de 4 reemplazos (15% de descuento), Paquete de 8 reemplazos (20% de descuento) y Suscripción mensual (25% de descuento). Consulta nuestras opciones de suscripción para más detalles."
        },
        {
          question: "¿Cuáles son los métodos de pago aceptados?",
          answer: "Aceptamos transferencias bancarias, pagos en efectivo al momento de la entrega y pagos a través de aplicaciones móviles como Yappy. Próximamente estaremos implementando pagos con tarjeta de crédito/débito."
        }
      ]
    }
  ];
</script>

<!-- Hero Section -->
<section class="py-16 bg-primary/5">
  <div class="container mx-auto px-4">
    {#if visible}
      <div class="max-w-3xl mx-auto text-center" in:fade={{duration: 800}}>
        <h1 class="text-4xl md:text-5xl font-bold mb-6 text-dark">Preguntas Frecuentes</h1>
        <p class="text-xl text-gray-700 mb-8">
          Encuentra respuestas a las preguntas más comunes sobre Wawi Spot. Si no encuentras lo que buscas, no dudes en contactarnos.
        </p>
      </div>
    {/if}
  </div>
</section>

<!-- FAQ Sections -->
{#each faqs as category, i}
  <section class="py-12 {i % 2 === 1 ? 'bg-gray-50' : ''}">
    <div class="container mx-auto px-4">
      {#if visible}
        <h2 
          class="text-2xl md:text-3xl font-bold mb-8 {i % 2 === 1 ? '' : 'text-primary'}"
          in:fly={{y: 30, duration: 800, delay: 200 * i}}
        >
          {category.category}
        </h2>
        
        <div class="space-y-4">
          {#each category.questions as faq, j}
            <div 
              class="bg-white rounded-lg shadow-md overflow-hidden transition-all duration-300"
              in:fly={{y: 20, duration: 600, delay: 200 * i + 100 * j}}
            >
              <button 
                class="w-full px-6 py-4 text-left flex justify-between items-center focus:outline-none"
                on:click={() => toggleQuestion(i * 100 + j)}
              >
                <span class="font-medium text-lg">{faq.question}</span>
                <svg 
                  class="w-5 h-5 text-primary transition-transform duration-300 {activeQuestion === i * 100 + j ? 'transform rotate-180' : ''}" 
                  fill="none" 
                  stroke="currentColor" 
                  viewBox="0 0 24 24"
                >
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                </svg>
              </button>
              
              {#if activeQuestion === i * 100 + j}
                <div 
                  class="px-6 py-4 bg-gray-50 border-t border-gray-100"
                  transition:fade={{duration: 300}}
                >
                  <p class="text-gray-700">{faq.answer}</p>
                </div>
              {/if}
            </div>
          {/each}
        </div>
      {/if}
    </div>
  </section>
{/each}

<!-- Contacto Section -->
<section class="py-16 bg-primary/10">
  <div class="container mx-auto px-4 text-center">
    {#if visible}
      <div in:fade={{duration: 800}}>
        <h2 class="text-3xl font-bold mb-6">¿No encontraste lo que buscabas?</h2>
        <p class="text-lg mb-8 max-w-2xl mx-auto">
          Estamos aquí para ayudarte. Contáctanos directamente y responderemos a todas tus preguntas.
        </p>
        <div class="flex flex-wrap justify-center gap-4">
          <a 
            href="/contacto" 
            class="inline-block bg-primary hover:bg-primary/90 text-white font-medium py-3 px-8 rounded-full transition-all duration-300 transform hover:scale-105 hover:shadow-lg"
          >
            Contactar
          </a>
          <a 
            href="http://wa.me/50764229334" 
            target="_blank" 
            class="inline-flex items-center gap-2 bg-[#25D366] hover:bg-[#20BD5C] text-white font-medium py-3 px-8 rounded-full transition-all duration-300 transform hover:scale-105 hover:shadow-lg"
          >
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
            </svg>
            WhatsApp
          </a>
        </div>
      </div>
    {/if}
  </div>
</section> 