<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  
  let activeTab = 'descripcion';
  let visible = false;
  
  onMount(() => {
    visible = true;
  });
  
  function setActiveTab(tab) {
    activeTab = tab;
  }
  
  const features = [
    {
      title: "Pasto 100% Natural",
      description: "Cultivado especialmente para mascotas, sin pesticidas ni químicos dañinos.",
      icon: `<svg class="w-10 h-10 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>`
    },
    {
      title: "Absorbe Olores",
      description: "El pasto natural neutraliza los olores de manera efectiva, manteniendo tu hogar fresco.",
      icon: `<svg class="w-10 h-10 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 20l-5.447-2.724A1 1 0 013 16.382V5.618a1 1 0 011.447-.894L9 7m0 13l6-3m-6 3V7m6 10l4.553 2.276A1 1 0 0021 18.382V7.618a1 1 0 00-.553-.894L15 4m0 13V4m0 0L9 7"></path>
            </svg>`
    },
    {
      title: "Fácil Mantenimiento",
      description: "Simplemente reemplaza el pasto cuando sea necesario. No más limpieza diaria.",
      icon: `<svg class="w-10 h-10 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"></path>
            </svg>`
    },
    {
      title: "Biodegradable",
      description: "Amigable con el medio ambiente. Reduce tu huella de carbono.",
      icon: `<svg class="w-10 h-10 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
            </svg>`
    },
    {
      title: "Delivery a Domicilio",
      description: "Recibe tu Wawi Spot directamente en tu puerta, sin complicaciones.",
      icon: `<svg class="w-10 h-10 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path d="M9 17a2 2 0 11-4 0 2 2 0 014 0zM19 17a2 2 0 11-4 0 2 2 0 014 0z"></path>
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16V6a1 1 0 00-1-1H4a1 1 0 00-1 1v10a1 1 0 001 1h1m8-1a1 1 0 01-1 1H9m4-1V8a1 1 0 011-1h2.586a1 1 0 01.707.293l3.414 3.414a1 1 0 01.293.707V16a1 1 0 01-1 1h-1m-6-1a1 1 0 001 1h1M5 17a2 2 0 104 0m-4 0a2 2 0 114 0m6 0a2 2 0 104 0m-4 0a2 2 0 114 0"></path>
            </svg>`
    },
    {
      title: "Saludable para tu Mascota",
      description: "Reduce el estrés y promueve comportamientos naturales en tu mascota.",
      icon: `<svg class="w-10 h-10 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"></path>
            </svg>`
    }
  ];
  
  const sizes = [
    { 
      name: "Paquete Shaq", 
      dimensions: "60 x 45 cm", 
      price: "$59.95", 
      recommended: "Gatos y perros pequeños",
      includes: [
        "Caja de Madera 60x45cm",
        "Bandeja de Pasto",
        "Plaquita con nombre del wawi",
        "Spray adiestrador",
        "Bolsitas de basura",
        "Regalo by Tobybandanas",
        "Delivery a la puerta de tu casa"
      ],
      image: "/img/shaq.jpg"
    },
    { 
      name: "Paquete Balú", 
      dimensions: "90 x 50 cm", 
      price: "$69.95", 
      recommended: "Perros medianos", 
      popular: true,
      includes: [
        "Caja de Madera 90x50cm",
        "Plaquita con nombre del wawi",
        "Bandeja de Pasto",
        "Spray adiestrador",
        "Bolsitas de basura",
        "Regalo by Tobybandanas",
        "Delivery a la puerta de tu casa"
      ],
      image: "/img/balu.jpg"
    },
    { 
      name: "Paquete Cooper", 
      dimensions: "100 x 75 cm", 
      price: "$79.95", 
      recommended: "Perros grandes",
      includes: [
        "Caja de Madera 100x75cm",
        "Plaquita con nombre del wawi",
        "Bandeja de Pasto",
        "Spray adiestrador",
        "Bolsitas de basura",
        "Regalo by Tobybandanas",
        "Delivery a la puerta de tu casa"
      ],
      image: "/img/cooper.jpg"
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
    note: "La duración del pasto es de 25 a 30 días según su cuidado"
  };
  
  // Información de entrega
  const delivery = {
    title: "Entregas",
    description: "El servicio de entrega se estará realizando en un periodo de 7 días posterior a su pago, hasta la puerta de su domicilio.",
    note: "Todos los paquetes incluyen delivery e instalación gratis"
  };
</script>

<!-- Hero Section -->
<section class="py-12 md:py-16 bg-gray-50">
  <div class="container mx-auto px-4">
    <div class="flex flex-col md:flex-row items-center gap-8 md:gap-16">
      <div class="w-full md:w-1/2">
        {#if visible}
          <h1 
            class="text-2xl md:text-4xl lg:text-5xl font-bold mb-4 md:mb-6 text-dark"
            in:fly={{y: 50, duration: 800}}
          >
            Wawi Spot: <span class="text-primary">Bandeja Sanitaria Natural</span>
          </h1>
          <p 
            class="text-base md:text-lg text-gray-700 mb-6 md:mb-8"
            in:fly={{y: 50, duration: 800, delay: 200}}
          >
            Wawi Spot es una innovadora bandeja sanitaria con pasto 100% natural, diseñada para proporcionar a tu mascota una experiencia más natural y saludable. Nuestro producto combina la comodidad de una bandeja tradicional con los beneficios del pasto real.
          </p>
          <div class="flex flex-wrap gap-3 md:gap-4" in:fade={{duration: 800, delay: 400}}>
            <a 
              href="/contacto" 
              class="inline-block bg-primary hover:bg-primary/90 text-white font-medium py-2 md:py-3 px-6 md:px-8 rounded-full transition-all duration-300 transform hover:scale-105 hover:shadow-lg"
            >
              Haz tu pedido
            </a>
            <a 
              href="#caracteristicas" 
              class="inline-block bg-white border border-primary text-primary hover:bg-primary/10 font-medium py-2 md:py-3 px-6 md:px-8 rounded-full transition-all duration-300"
            >
              Ver características
            </a>
          </div>
        {/if}
      </div>
      <div class="w-full md:w-1/2 mt-6 md:mt-0">
        {#if visible}
          <div 
            class="relative rounded-lg overflow-hidden shadow-xl"
            in:fade={{duration: 1000, delay: 300}}
          >
            <img 
              src="/img/banner.jpg" 
              alt="Wawi Spot Bandeja Sanitaria" 
              class="w-full h-auto rounded-lg"
            >
            <div class="absolute top-4 right-4 bg-primary text-white text-sm font-bold px-4 py-1 rounded-full">
              Nuevo
            </div>
          </div>
        {/if}
      </div>
    </div>
  </div>
</section>

<!-- Tabs Section -->
<section class="py-12 md:py-16">
  <div class="container mx-auto px-4">
    <div class="border-b border-gray-200 mb-6 md:mb-8 overflow-x-auto">
      <div class="flex flex-nowrap -mb-px min-w-max">
        <button 
          class="inline-block py-3 md:py-4 px-4 md:px-6 text-base md:text-lg font-medium whitespace-nowrap {activeTab === 'descripcion' ? 'text-primary border-b-2 border-primary' : 'text-gray-500 hover:text-primary'}"
          on:click={() => setActiveTab('descripcion')}
        >
          Descripción
        </button>
        <button 
          class="inline-block py-3 md:py-4 px-4 md:px-6 text-base md:text-lg font-medium whitespace-nowrap {activeTab === 'como-funciona' ? 'text-primary border-b-2 border-primary' : 'text-gray-500 hover:text-primary'}"
          on:click={() => setActiveTab('como-funciona')}
        >
          Cómo funciona
        </button>
        <button 
          class="inline-block py-3 md:py-4 px-4 md:px-6 text-base md:text-lg font-medium whitespace-nowrap {activeTab === 'tamanos' ? 'text-primary border-b-2 border-primary' : 'text-gray-500 hover:text-primary'}"
          on:click={() => setActiveTab('tamanos')}
        >
          Tamaños y precios
        </button>
      </div>
    </div>
    
    <!-- Contenido de las pestañas -->
    <div class="tab-content">
      <!-- Descripción -->
      <div class={activeTab === 'descripcion' ? 'block' : 'hidden'}>
        <div class="prose prose-lg max-w-none">
          <p class="mb-4 text-base md:text-lg">
            Wawi Spot es una bandeja sanitaria revolucionaria que utiliza pasto natural en lugar de arena o materiales sintéticos. Diseñada pensando en el bienestar de tu mascota y la comodidad de tu hogar.
          </p>
          <p class="mb-4 text-base md:text-lg">
            El pasto natural proporciona una superficie familiar y cómoda para tu mascota, reduciendo el estrés y promoviendo comportamientos naturales. Además, el pasto absorbe naturalmente los olores, manteniendo tu hogar fresco y limpio.
          </p>
          <p class="mb-6 md:mb-8 text-base md:text-lg">
            Nuestra bandeja está fabricada con materiales duraderos y de alta calidad, diseñados para contener el pasto de manera segura y prevenir fugas. El sistema de drenaje integrado ayuda a mantener el pasto fresco por más tiempo.
          </p>
          
          <h3 class="text-xl md:text-2xl font-semibold mb-3 md:mb-4">Beneficios principales:</h3>
          <ul class="list-disc pl-5 md:pl-6 mb-6 md:mb-8 space-y-1 md:space-y-2 text-base md:text-lg">
            <li>Reduce significativamente los olores en comparación con las bandejas tradicionales</li>
            <li>Más higiénico y saludable para tu mascota</li>
            <li>Ecológico y biodegradable</li>
            <li>Fácil de mantener</li>
            <li>Aspecto natural que se integra mejor en la decoración de tu hogar</li>
            <li>Servicio de entrega a domicilio para mayor comodidad</li>
          </ul>
          
          <div class="bg-primary/10 p-4 md:p-6 rounded-lg border-l-4 border-primary">
            <h4 class="text-lg md:text-xl font-semibold mb-2">¿Sabías que?</h4>
            <p class="text-base md:text-lg">Las mascotas que utilizan bandejas con superficies naturales muestran menos signos de estrés y ansiedad en comparación con las que usan bandejas tradicionales con arena o materiales sintéticos.</p>
          </div>
        </div>
      </div>
      
      <!-- Cómo funciona -->
      <div class={activeTab === 'como-funciona' ? 'block' : 'hidden'}>
        <div class="prose prose-lg max-w-none">
          <p class="mb-6 text-base md:text-lg">
            Wawi Spot funciona de manera simple pero efectiva, proporcionando a tu mascota una experiencia natural mientras mantiene tu hogar limpio y libre de olores.
          </p>
          
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-6 md:gap-8 mb-8 md:mb-10">
            <div class="text-center">
              <div class="bg-primary/10 w-14 h-14 md:w-16 md:h-16 rounded-full flex items-center justify-center mx-auto mb-3 md:mb-4">
                <span class="text-xl md:text-2xl font-bold text-primary">1</span>
              </div>
              <h4 class="text-lg md:text-xl font-semibold mb-2">Recibe tu Wawi Spot</h4>
              <p class="text-gray-600 text-sm md:text-base">Te entregamos la bandeja con pasto fresco directamente en tu puerta.</p>
            </div>
            
            <div class="text-center">
              <div class="bg-primary/10 w-14 h-14 md:w-16 md:h-16 rounded-full flex items-center justify-center mx-auto mb-3 md:mb-4">
                <span class="text-xl md:text-2xl font-bold text-primary">2</span>
              </div>
              <h4 class="text-lg md:text-xl font-semibold mb-2">Colócala en un lugar adecuado</h4>
              <p class="text-gray-600 text-sm md:text-base">Ubica la bandeja en un lugar accesible para tu mascota, preferiblemente en el mismo sitio donde tenía su bandeja anterior.</p>
            </div>
            
            <div class="text-center">
              <div class="bg-primary/10 w-14 h-14 md:w-16 md:h-16 rounded-full flex items-center justify-center mx-auto mb-3 md:mb-4">
                <span class="text-xl md:text-2xl font-bold text-primary">3</span>
              </div>
              <h4 class="text-lg md:text-xl font-semibold mb-2">Reemplaza cuando sea necesario</h4>
              <p class="text-gray-600 text-sm md:text-base">Dependiendo del uso, el pasto durará entre 1-2 semanas. Simplemente solicita un reemplazo cuando sea necesario.</p>
            </div>
          </div>
          
          <h3 class="text-xl md:text-2xl font-semibold mb-3 md:mb-4">Consejos para el mantenimiento:</h3>
          <ul class="list-disc pl-5 md:pl-6 mb-6 md:mb-8 space-y-1 md:space-y-2 text-base md:text-lg">
            <li>Riega ligeramente el pasto cada 2-3 días para mantenerlo fresco</li>
            <li>Retira los desechos sólidos diariamente</li>
            <li>Coloca la bandeja en un lugar con luz natural pero no directamente bajo el sol</li>
            <li>Si notas que el pasto comienza a amarillear, es momento de reemplazarlo</li>
          </ul>
          
          <div class="bg-yellow-50 p-4 md:p-6 rounded-lg border-l-4 border-yellow-400">
            <h4 class="text-lg md:text-xl font-semibold mb-2">Importante</h4>
            <p class="text-base md:text-lg">La adaptación de tu mascota puede tomar algunos días. Para facilitar la transición, puedes colocar un poco de su arena o material anterior sobre el pasto durante los primeros días.</p>
          </div>
        </div>
      </div>
      
      <!-- Tamaños y precios -->
      <div class={activeTab === 'tamanos' ? 'block' : 'hidden'}>
        <div class="prose prose-lg max-w-none">
          <p class="mb-6 md:mb-8 text-base md:text-lg">
            Ofrecemos diferentes tamaños para adaptarnos a las necesidades de tu mascota. Todos nuestros modelos incluyen la bandeja, el sistema de drenaje y el pasto natural.
          </p>
          
          <div class="grid grid-cols-1 md:grid-cols-3 gap-6 md:gap-8 mb-8 md:mb-10">
            {#each sizes as size}
              <div class="border rounded-lg overflow-hidden {size.popular ? 'border-primary shadow-lg relative' : 'border-gray-200'}">
                {#if size.popular}
                  <div class="absolute top-0 right-0 bg-primary text-white text-xs font-bold px-3 py-1 rounded-bl-lg">
                    Más popular
                  </div>
                {/if}
                <div class="p-0">
                  <div class="h-40 md:h-48 overflow-hidden">
                    <img src={size.image} alt={size.name} class="w-full h-full object-cover">
                  </div>
                  <div class="p-4 md:p-6">
                    <h3 class="text-lg md:text-xl font-bold mb-2">{size.name}</h3>
                    <p class="text-gray-600 mb-3 md:mb-4 text-sm md:text-base">Dimensiones: {size.dimensions}</p>
                    <p class="text-2xl md:text-3xl font-bold text-primary mb-3 md:mb-4">{size.price}</p>
                    <p class="text-xs md:text-sm text-gray-500 mb-3 md:mb-4">Recomendado para: {size.recommended}</p>
                    
                    <h4 class="font-semibold mb-2 text-sm md:text-base">Incluye:</h4>
                    <ul class="list-disc pl-4 md:pl-5 mb-4 md:mb-6 text-xs md:text-sm text-gray-600">
                      {#each size.includes as item}
                        <li>{item}</li>
                      {/each}
                    </ul>
                    
                    <a 
                      href="/contacto" 
                      class="block text-center bg-primary hover:bg-primary/90 text-white font-medium py-2 md:py-2.5 px-4 rounded-full transition-all duration-300 text-sm md:text-base"
                    >
                      Seleccionar
                    </a>
                  </div>
                </div>
              </div>
            {/each}
          </div>
          
          <!-- Información de entrega -->
          <div class="bg-gray-50 p-4 md:p-6 rounded-lg mb-6 md:mb-8">
            <h3 class="text-lg md:text-xl font-semibold mb-3 md:mb-4">{delivery.title}</h3>
            <p class="mb-3 md:mb-4 text-sm md:text-base">
              {delivery.description}
            </p>
            <div class="bg-green-50 p-3 md:p-4 rounded-lg border-l-4 border-green-500">
              <p class="text-xs md:text-sm italic text-gray-700">{delivery.note}</p>
            </div>
          </div>
          
          <!-- Información de mantenimiento -->
          <div class="bg-gray-50 p-4 md:p-6 rounded-lg">
            <h3 class="text-lg md:text-xl font-semibold mb-3 md:mb-4">{maintenance.title}</h3>
            <p class="mb-3 md:mb-4 text-sm md:text-base">
              {maintenance.description}
            </p>
            <ul class="list-disc pl-5 md:pl-6 mb-3 md:mb-4 space-y-1 md:space-y-2 text-sm md:text-base">
              {#each maintenance.prices as price}
                <li>{price.name}: <strong>{price.price}</strong></li>
              {/each}
            </ul>
            <div class="bg-yellow-50 p-3 md:p-4 rounded-lg border-l-4 border-yellow-500">
              <p class="text-xs md:text-sm italic text-gray-700">{maintenance.note}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Características Section -->
<section id="caracteristicas" class="py-12 md:py-16 bg-gray-50">
  <div class="container mx-auto px-4">
    <h2 class="text-2xl md:text-3xl font-bold text-center mb-8 md:mb-16">Características destacadas</h2>
    
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 md:gap-8">
      {#each features as feature, i}
        <div 
          class="bg-white rounded-lg shadow-md p-5 md:p-6 transition-all duration-300 hover:shadow-lg hover:-translate-y-1"
          in:fly={{y: 30, duration: 600, delay: 100 * i}}
        >
          <div class="bg-primary/10 w-14 h-14 md:w-16 md:h-16 rounded-full flex items-center justify-center mb-3 md:mb-4">
            {@html feature.icon}
          </div>
          <h3 class="text-lg md:text-xl font-semibold mb-2">{feature.title}</h3>
          <p class="text-gray-600 text-sm md:text-base">{feature.description}</p>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- CTA Section -->
<section class="py-12 md:py-16 bg-primary/10">
  <div class="container mx-auto px-4 text-center">
    <h2 class="text-2xl md:text-3xl font-bold mb-4 md:mb-6">¿Listo para darle a tu mascota lo mejor?</h2>
    <p class="text-base md:text-lg mb-6 md:mb-8 max-w-2xl mx-auto">
      Haz tu pedido hoy y recibe tu Wawi Spot en la comodidad de tu hogar. Tu mascota merece lo mejor.
    </p>
    <a 
      href="/contacto" 
      class="inline-block bg-primary hover:bg-primary/90 text-white font-medium py-2.5 md:py-3 px-6 md:px-8 rounded-full transition-all duration-300 transform hover:scale-105 hover:shadow-lg text-base md:text-lg"
    >
      ¡Haz tu pedido ahora!
    </a>
  </div>
</section> 