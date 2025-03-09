<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  
  let visible = false;
  let formSubmitted = false;
  
  let formData = {
    nombre: '',
    email: '',
    telefono: '',
    mensaje: '',
    tamano: 'mediano',
    interes: []
  };
  
  onMount(() => {
    visible = true;
  });
  
  function handleSubmit() {
    // Aquí iría la lógica para enviar el formulario
    console.log('Formulario enviado:', formData);
    formSubmitted = true;
    
    // Resetear el formulario después de 5 segundos
    setTimeout(() => {
      formSubmitted = false;
      formData = {
        nombre: '',
        email: '',
        telefono: '',
        mensaje: '',
        tamano: 'mediano',
        interes: []
      };
    }, 5000);
  }
  
  function handleCheckbox(event, value) {
    const checked = event.target.checked;
    
    if (checked) {
      formData.interes = [...formData.interes, value];
    } else {
      formData.interes = formData.interes.filter(item => item !== value);
    }
  }
</script>

<!-- Hero Section -->
<section class="py-16 bg-primary/5">
  <div class="container mx-auto px-4">
    {#if visible}
      <div class="max-w-3xl mx-auto text-center" in:fade={{duration: 800}}>
        <h1 class="text-4xl md:text-5xl font-bold mb-6 text-dark">Contacto</h1>
        <p class="text-xl text-gray-700 mb-8">
          Estamos aquí para ayudarte. Ponte en contacto con nosotros para hacer tu pedido o resolver cualquier duda.
        </p>
      </div>
    {/if}
  </div>
</section>

<!-- Contacto Section -->
<section class="py-16">
  <div class="container mx-auto px-4">
    <div class="flex flex-col lg:flex-row gap-12">
      <!-- Formulario de contacto -->
      <div class="w-full lg:w-2/3">
        {#if visible}
          <div 
            class="bg-white rounded-lg shadow-md p-8"
            in:fly={{y: 30, duration: 800}}
          >
            <h2 class="text-2xl font-bold mb-6">Envíanos un mensaje</h2>
            
            {#if formSubmitted}
              <div class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded mb-6" transition:fade>
                <p>¡Gracias por tu mensaje! Te contactaremos pronto.</p>
              </div>
            {/if}
            
            <form on:submit|preventDefault={handleSubmit} class="space-y-6">
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                  <label for="nombre" class="block text-gray-700 font-medium mb-2">Nombre completo *</label>
                  <input 
                    type="text" 
                    id="nombre" 
                    bind:value={formData.nombre} 
                    required
                    class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent"
                  >
                </div>
                
                <div>
                  <label for="email" class="block text-gray-700 font-medium mb-2">Correo electrónico *</label>
                  <input 
                    type="email" 
                    id="email" 
                    bind:value={formData.email} 
                    required
                    class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent"
                  >
                </div>
              </div>
              
              <div>
                <label for="telefono" class="block text-gray-700 font-medium mb-2">Teléfono</label>
                <input 
                  type="tel" 
                  id="telefono" 
                  bind:value={formData.telefono}
                  class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent"
                >
              </div>
              
              <div>
                <label class="block text-gray-700 font-medium mb-2">¿Qué te interesa? (opcional)</label>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
                  <label class="flex items-center">
                    <input 
                      type="checkbox" 
                      value="compra" 
                      on:change={(e) => handleCheckbox(e, 'compra')}
                      class="mr-2 h-5 w-5 text-primary focus:ring-primary"
                    >
                    <span>Comprar Wawi Spot</span>
                  </label>
                  <label class="flex items-center">
                    <input 
                      type="checkbox" 
                      value="reemplazo" 
                      on:change={(e) => handleCheckbox(e, 'reemplazo')}
                      class="mr-2 h-5 w-5 text-primary focus:ring-primary"
                    >
                    <span>Reemplazo de pasto</span>
                  </label>
                  <label class="flex items-center">
                    <input 
                      type="checkbox" 
                      value="suscripcion" 
                      on:change={(e) => handleCheckbox(e, 'suscripcion')}
                      class="mr-2 h-5 w-5 text-primary focus:ring-primary"
                    >
                    <span>Suscripción</span>
                  </label>
                  <label class="flex items-center">
                    <input 
                      type="checkbox" 
                      value="informacion" 
                      on:change={(e) => handleCheckbox(e, 'informacion')}
                      class="mr-2 h-5 w-5 text-primary focus:ring-primary"
                    >
                    <span>Información general</span>
                  </label>
                </div>
              </div>
              
              <div>
                <label for="tamano" class="block text-gray-700 font-medium mb-2">Tamaño de interés (opcional)</label>
                <select 
                  id="tamano" 
                  bind:value={formData.tamano}
                  class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent"
                >
                  <option value="pequeno">Pequeño (40 x 30 cm)</option>
                  <option value="mediano">Mediano (60 x 40 cm)</option>
                  <option value="grande">Grande (80 x 60 cm)</option>
                </select>
              </div>
              
              <div>
                <label for="mensaje" class="block text-gray-700 font-medium mb-2">Mensaje *</label>
                <textarea 
                  id="mensaje" 
                  bind:value={formData.mensaje} 
                  required
                  rows="4"
                  class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent"
                ></textarea>
              </div>
              
              <div>
                <button 
                  type="submit" 
                  class="inline-block bg-primary hover:bg-primary/90 text-white font-medium py-3 px-8 rounded-md transition-all duration-300 transform hover:scale-105 hover:shadow-lg"
                >
                  Enviar mensaje
                </button>
              </div>
            </form>
          </div>
        {/if}
      </div>
      
      <!-- Información de contacto -->
      <div class="w-full lg:w-1/3">
        {#if visible}
          <div 
            class="bg-white rounded-lg shadow-md p-8 mb-8"
            in:fly={{y: 30, duration: 800, delay: 200}}
          >
            <h2 class="text-2xl font-bold mb-6">Información de contacto</h2>
            
            <ul class="space-y-4">
              <li class="flex items-start">
                <svg class="w-6 h-6 mt-1 mr-3 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path>
                </svg>
                <div>
                  <p class="font-medium">Teléfono</p>
                  <p class="text-gray-600">+507 6422-9334</p>
                </div>
              </li>
              
              <li class="flex items-start">
                <svg class="w-6 h-6 mt-1 mr-3 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path>
                </svg>
                <div>
                  <p class="font-medium">Email</p>
                  <p class="text-gray-600">info@wawispot.com</p>
                </div>
              </li>
              
              <li class="flex items-start">
                <svg class="w-6 h-6 mt-1 mr-3 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
                </svg>
                <div>
                  <p class="font-medium">Ubicación</p>
                  <p class="text-gray-600">Panamá</p>
                </div>
              </li>
              
              <li class="flex items-start">
                <svg class="w-6 h-6 mt-1 mr-3 text-primary" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                </svg>
                <div>
                  <p class="font-medium">Horario de atención</p>
                  <p class="text-gray-600">Lunes a Viernes: 9:00 AM - 6:00 PM</p>
                  <p class="text-gray-600">Sábados: 9:00 AM - 1:00 PM</p>
                </div>
              </li>
            </ul>
          </div>
          
          <div 
            class="bg-primary/10 rounded-lg p-8"
            in:fly={{y: 30, duration: 800, delay: 400}}
          >
            <h3 class="text-xl font-bold mb-4">Contacto rápido por WhatsApp</h3>
            <p class="text-gray-700 mb-6">
              Para una respuesta más rápida, contáctanos directamente por WhatsApp.
            </p>
            <a 
              href="http://wa.me/50764229334" 
              target="_blank" 
              class="flex items-center justify-center gap-2 bg-[#25D366] hover:bg-[#20BD5C] text-white font-medium py-3 px-6 rounded-md transition-all duration-300 w-full"
            >
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
              </svg>
              Contactar por WhatsApp
            </a>
          </div>
        {/if}
      </div>
    </div>
  </div>
</section>

<!-- Mapa Section -->
<section class="py-16 bg-gray-50">
  <div class="container mx-auto px-4">
    {#if visible}
      <div class="max-w-3xl mx-auto text-center mb-12" in:fade={{duration: 800}}>
        <h2 class="text-3xl font-bold mb-4">Nuestra ubicación</h2>
        <p class="text-lg text-gray-700">
          Estamos ubicados en Panamá, con servicio de entrega a domicilio en toda la ciudad.
        </p>
      </div>
      
      <div class="rounded-lg overflow-hidden shadow-md" in:fade={{duration: 800, delay: 200}}>
        <iframe 
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d254509.99450564097!2d-79.6270648!3d8.9714249!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x8faca8f1dbe80363%3A0xaba25df1f042c10e!2sPanam%C3%A1!5e0!3m2!1ses!2spa!4v1646252524818!5m2!1ses!2spa" 
          width="100%" 
          height="450" 
          style="border:0;" 
          allowfullscreen="" 
          loading="lazy"
          title="Mapa de ubicación"
        ></iframe>
      </div>
    {/if}
  </div>
</section> 