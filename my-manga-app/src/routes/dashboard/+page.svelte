<script>
  import { onMount } from 'svelte';

  let sidebarOpen = true;
  let mobileMenuOpen = false;
  let activeSection = 'obras';

  // Dados de exemplo para mangás
  const mangas = [
    {
      id: 1,
      title: 'One Piece',
      cover: '/placeholder.svg?height=400&width=300',
      author: 'Eiichiro Oda',
      status: 'ongoing',
      chapters: 1089,
      views: 1250000,
      rating: 4.9,
      categories: ['Ação', 'Aventura', 'Comédia', 'Fantasia'],
      lastUpdated: '2023-05-01'
    },
    {
      id: 2,
      title: 'Berserk',
      cover: '/placeholder.svg?height=400&width=300',
      author: 'Kentaro Miura',
      status: 'ongoing',
      chapters: 364,
      views: 980000,
      rating: 4.8,
      categories: ['Ação', 'Aventura', 'Drama', 'Fantasia', 'Horror'],
      lastUpdated: '2023-04-15'
    },
    {
      id: 3,
      title: 'Vagabond',
      cover: '/placeholder.svg?height=400&width=300',
      author: 'Takehiko Inoue',
      status: 'hiatus',
      chapters: 327,
      views: 750000,
      rating: 4.7,
      categories: ['Ação', 'Aventura', 'Drama', 'Histórico'],
      lastUpdated: '2022-12-10'
    },
    {
      id: 4,
      title: 'Chainsaw Man',
      cover: '/placeholder.svg?height=400&width=300',
      author: 'Tatsuki Fujimoto',
      status: 'ongoing',
      chapters: 129,
      views: 890000,
      rating: 4.6,
      categories: ['Ação', 'Aventura', 'Horror', 'Sobrenatural'],
      lastUpdated: '2023-05-02'
    },
    {
      id: 5,
      title: 'Jujutsu Kaisen',
      cover: '/placeholder.svg?height=400&width=300',
      author: 'Gege Akutami',
      status: 'ongoing',
      chapters: 235,
      views: 920000,
      rating: 4.7,
      categories: ['Ação', 'Aventura', 'Sobrenatural'],
      lastUpdated: '2023-04-28'
    },
    {
      id: 6,
      title: 'My Hero Academia',
      cover: '/placeholder.svg?height=400&width=300',
      author: 'Kohei Horikoshi',
      status: 'ongoing',
      chapters: 402,
      views: 880000,
      rating: 4.5,
      categories: ['Ação', 'Aventura', 'Comédia', 'Super Poderes'],
      lastUpdated: '2023-04-30'
    },
    {
      id: 7,
      title: 'Demon Slayer',
      cover: '/placeholder.svg?height=400&width=300',
      author: 'Koyoharu Gotouge',
      status: 'completed',
      chapters: 205,
      views: 1100000,
      rating: 4.8,
      categories: ['Ação', 'Aventura', 'Sobrenatural', 'Histórico'],
      lastUpdated: '2022-05-15'
    },
    {
      id: 8,
      title: 'Tokyo Revengers',
      cover: '/placeholder.svg?height=400&width=300',
      author: 'Ken Wakui',
      status: 'completed',
      chapters: 278,
      views: 820000,
      rating: 4.4,
      categories: ['Ação', 'Drama', 'Sobrenatural'],
      lastUpdated: '2023-01-18'
    }
  ];

  const stats = {
    totalMangas: 12,
    totalChapters: 3368,
    totalViews: 9350000,
    ongoingMangas: 7,
    completedMangas: 4,
    hiatus: 1
  };

  const availableCategories = [
    'Ação', 'Aventura', 'Comédia', 'Drama', 'Fantasia',
    'Horror', 'Romance', 'Sci-Fi', 'Slice of Life', 'Esportes',
    'Sobrenatural', 'Mistério', 'Psicológico', 'Histórico', 'Super Poderes'
  ];

  // Função para alternar a barra lateral
  function toggleSidebar() {
    sidebarOpen = !sidebarOpen;
  }

  // Função para mudar a seção ativa
  function setActiveSection(section) {
    activeSection = section;
    if (window.innerWidth < 768) {
      mobileMenuOpen = false;
    }
  }

  // Função para formatar números grandes
  function formatNumber(num) {
    if (num >= 1000000) {
      return (num / 1000000).toFixed(1) + 'M';
    } else if (num >= 1000) {
      return (num / 1000).toFixed(1) + 'K';
    }
    return num;
  }

  onMount(() => {
    // Verificar tamanho da tela para definir estado inicial da sidebar
    if (window.innerWidth < 768) {
      sidebarOpen = false;
    }
  });
</script>

<div class="min-h-screen bg-gray-900 text-white flex">
  <!-- Sidebar -->
  <aside class={`bg-gray-800 w-64 fixed h-full transition-all duration-300 ease-in-out z-30 ${sidebarOpen ? 'left-0' : '-left-64'}`}>
    <div class="p-4 border-b border-gray-700">
      <div class="flex items-center">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-red-500" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1 0-5H20"></path>
        </svg>
        <span class="ml-2 text-xl font-bold">MangáReader</span>
      </div>
      <div class="mt-2 text-sm text-gray-400">Painel de Administração</div>
    </div>

    <nav class="mt-4">
      <div class="px-4 py-2 text-xs font-semibold text-gray-400 uppercase tracking-wider">
        Gerenciamento
      </div>
      <a
        href="#dashboard"
        class={`flex items-center px-4 py-3 text-gray-300 hover:bg-gray-700 hover:text-white transition-colors ${activeSection === 'dashboard' ? 'bg-gray-700 text-white border-l-4 border-red-500' : ''}`}
        on:click|preventDefault={() => setActiveSection('dashboard')}
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <rect x="3" y="3" width="7" height="7"></rect>
          <rect x="14" y="3" width="7" height="7"></rect>
          <rect x="14" y="14" width="7" height="7"></rect>
          <rect x="3" y="14" width="7" height="7"></rect>
        </svg>
        Dashboard
      </a>
      <a
        href="#obras"
        class={`flex items-center px-4 py-3 text-gray-300 hover:bg-gray-700 hover:text-white transition-colors ${activeSection === 'obras' ? 'bg-gray-700 text-white border-l-4 border-red-500' : ''}`}
        on:click|preventDefault={() => setActiveSection('obras')}
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1 0-5H20"></path>
        </svg>
        Obras
      </a>
      <a
        href="#capitulos"
        class={`flex items-center px-4 py-3 text-gray-300 hover:bg-gray-700 hover:text-white transition-colors ${activeSection === 'capitulos' ? 'bg-gray-700 text-white border-l-4 border-red-500' : ''}`}
        on:click|preventDefault={() => setActiveSection('capitulos')}
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path>
          <rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect>
        </svg>
        Capítulos
      </a>
      <a
        href="#categorias"
        class={`flex items-center px-4 py-3 text-gray-300 hover:bg-gray-700 hover:text-white transition-colors ${activeSection === 'categorias' ? 'bg-gray-700 text-white border-l-4 border-red-500' : ''}`}
        on:click|preventDefault={() => setActiveSection('categorias')}
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M9 19.5v-15A2.5 2.5 0 0 1 11.5 2H20v20H11.5a2.5 2.5 0 0 1-2.5-2.5z"></path>
          <path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"></path>
          <path d="M4 14.5A2.5 2.5 0 0 1 6.5 12H20"></path>
          <path d="M4 9.5A2.5 2.5 0 0 1 6.5 7H20"></path>
        </svg>
        Categorias
      </a>

      <div class="px-4 py-2 mt-4 text-xs font-semibold text-gray-400 uppercase tracking-wider">
        Usuários
      </div>
      <a
        href="#usuarios"
        class={`flex items-center px-4 py-3 text-gray-300 hover:bg-gray-700 hover:text-white transition-colors ${activeSection === 'usuarios' ? 'bg-gray-700 text-white border-l-4 border-red-500' : ''}`}
        on:click|preventDefault={() => setActiveSection('usuarios')}
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path>
          <circle cx="12" cy="7" r="4"></circle>
        </svg>
        Usuários
      </a>
      <a
        href="#comentarios"
        class={`flex items-center px-4 py-3 text-gray-300 hover:bg-gray-700 hover:text-white transition-colors ${activeSection === 'comentarios' ? 'bg-gray-700 text-white border-l-4 border-red-500' : ''}`}
        on:click|preventDefault={() => setActiveSection('comentarios')}
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"></path>
        </svg>
        Comentários
      </a>

      <div class="px-4 py-2 mt-4 text-xs font-semibold text-gray-400 uppercase tracking-wider">
        Configurações
      </div>
      <a
        href="#configuracoes"
        class={`flex items-center px-4 py-3 text-gray-300 hover:bg-gray-700 hover:text-white transition-colors ${activeSection === 'configuracoes' ? 'bg-gray-700 text-white border-l-4 border-red-500' : ''}`}
        on:click|preventDefault={() => setActiveSection('configuracoes')}
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="12" cy="12" r="3"></circle>
          <path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z"></path>
        </svg>
        Configurações
      </a>
    </nav>
  </aside>

  <!-- Overlay para fechar sidebar em dispositivos móveis -->
  {#if sidebarOpen && window.innerWidth < 768}
    <div
      class="fixed inset-0 bg-black bg-opacity-50 z-20"
      on:click={toggleSidebar}
    ></div>
  {/if}

  <!-- Conteúdo principal -->
  <div class={`flex-1 transition-all duration-300 ease-in-out ${sidebarOpen ? 'md:ml-64' : 'ml-0'}`}>
    <!-- Cabeçalho -->
    <header class="bg-gray-800 shadow-lg">
      <div class="px-4 py-3 flex items-center justify-between">
        <div class="flex items-center">
          <button
            class="text-gray-300 hover:text-white focus:outline-none"
            on:click={toggleSidebar}
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
          </button>
          <div class="ml-4 md:hidden">
            <span class="text-lg font-bold">MangáReader Admin</span>
          </div>
        </div>

        <div class="flex items-center">
          <div class="relative">
            <button class="flex items-center text-gray-300 hover:text-white focus:outline-none">
              <span class="mr-2 hidden md:block">Admin</span>
              <div class="h-8 w-8 rounded-full bg-red-500 flex items-center justify-center">
                <span class="font-bold">A</span>
              </div>
            </button>
          </div>
        </div>
      </div>
    </header>

    <!-- Conteúdo da página -->
    <main class="p-4 md:p-6">
      {#if activeSection === 'dashboard'}
        <!-- Dashboard -->
        <div>
          <h1 class="text-2xl font-bold mb-6">Dashboard</h1>

          <!-- Cards de estatísticas -->
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mb-8">
            <div class="bg-gray-800 rounded-lg shadow-lg p-6">
              <div class="flex items-center">
                <div class="p-3 rounded-full bg-red-500/20 text-red-500">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1 0-5H20"></path>
                  </svg>
                </div>
                <div class="ml-4">
                  <h2 class="text-gray-400 text-sm font-medium">Total de Obras</h2>
                  <p class="text-2xl font-bold">{stats.totalMangas}</p>
                </div>
              </div>
            </div>

            <div class="bg-gray-800 rounded-lg shadow-lg p-6">
              <div class="flex items-center">
                <div class="p-3 rounded-full bg-green-500/20 text-green-500">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path>
                    <rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect>
                  </svg>
                </div>
                <div class="ml-4">
                  <h2 class="text-gray-400 text-sm font-medium">Total de Capítulos</h2>
                  <p class="text-2xl font-bold">{stats.totalChapters}</p>
                </div>
              </div>
            </div>

            <div class="bg-gray-800 rounded-lg shadow-lg p-6">
              <div class="flex items-center">
                <div class="p-3 rounded-full bg-blue-500/20 text-blue-500">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"></path>
                    <circle cx="12" cy="12" r="3"></circle>
                  </svg>
                </div>
                <div class="ml-4">
                  <h2 class="text-gray-400 text-sm font-medium">Total de Visualizações</h2>
                  <p class="text-2xl font-bold">{formatNumber(stats.totalViews)}</p>
                </div>
              </div>
            </div>

            <div class="bg-gray-800 rounded-lg shadow-lg p-6">
              <div class="flex items-center">
                <div class="p-3 rounded-full bg-yellow-500/20 text-yellow-500">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="12" cy="12" r="10"></circle>
                    <polyline points="12 6 12 12 16 14"></polyline>
                  </svg>
                </div>
                <div class="ml-4">
                  <h2 class="text-gray-400 text-sm font-medium">Em Andamento</h2>
                  <p class="text-2xl font-bold">{stats.ongoingMangas}</p>
                </div>
              </div>
            </div>

            <div class="bg-gray-800 rounded-lg shadow-lg p-6">
              <div class="flex items-center">
                <div class="p-3 rounded-full bg-purple-500/20 text-purple-500">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"></path>
                    <polyline points="22 4 12 14.01 9 11.01"></polyline>
                  </svg>
                </div>
                <div class="ml-4">
                  <h2 class="text-gray-400 text-sm font-medium">Concluídos</h2>
                  <p class="text-2xl font-bold">{stats.completedMangas}</p>
                </div>
              </div>
            </div>

            <div class="bg-gray-800 rounded-lg shadow-lg p-6">
              <div class="flex items-center">
                <div class="p-3 rounded-full bg-orange-500/20 text-orange-500">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <rect x="2" y="7" width="20" height="14" rx="2" ry="2"></rect>
                    <path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"></path>
                  </svg>
                </div>
                <div class="ml-4">
                  <h2 class="text-gray-400 text-sm font-medium">Em Hiato</h2>
                  <p class="text-2xl font-bold">{stats.hiatus}</p>
                </div>
              </div>
            </div>
          </div>

          <!-- Atividade Recente -->
          <div class="bg-gray-800 rounded-lg shadow-lg p-6 mb-8">
            <h2 class="text-xl font-bold mb-4">Atividade Recente</h2>
            <div class="space-y-4">
              <div class="flex items-start">
                <div class="h-8 w-8 rounded-full bg-red-500 flex items-center justify-center mr-3">
                  <span class="font-bold">A</span>
                </div>
                <div>
                  <p class="text-sm">
                    <span class="font-medium">Admin</span> adicionou um novo capítulo para <span class="text-red-400">One Piece</span>
                  </p>
                  <p class="text-xs text-gray-400">Hoje, 10:30</p>
                </div>
              </div>
              <div class="flex items-start">
                <div class="h-8 w-8 rounded-full bg-blue-500 flex items-center justify-center mr-3">
                  <span class="font-bold">M</span>
                </div>
                <div>
                  <p class="text-sm">
                    <span class="font-medium">Moderador</span> atualizou as informações de <span class="text-red-400">Chainsaw Man</span>
                  </p>
                  <p class="text-xs text-gray-400">Ontem, 15:45</p>
                </div>
              </div>
              <div class="flex items-start">
                <div class="h-8 w-8 rounded-full bg-green-500 flex items-center justify-center mr-3">
                  <span class="font-bold">A</span>
                </div>
                <div>
                  <p class="text-sm">
                    <span class="font-medium">Admin</span> adicionou uma nova obra <span class="text-red-400">Oshi no Ko</span>
                  </p>
                  <p class="text-xs text-gray-400">2 dias atrás, 09:15</p>
                </div>
              </div>
            </div>
          </div>

          <!-- Gráfico de Visualizações (Mockup) -->
          <div class="bg-gray-800 rounded-lg shadow-lg p-6 mb-8">
            <h2 class="text-xl font-bold mb-4">Visualizações por Dia</h2>
            <div class="h-64 w-full bg-gray-700 rounded-lg p-4 flex items-center justify-center">
              <p class="text-gray-400">Gráfico de visualizações diárias</p>
              <!-- Aqui seria renderizado um gráfico real -->
            </div>
          </div>
        </div>
      {:else if activeSection === 'obras'}
        <!-- Gerenciamento de Obras -->
        <div>
          <div class="flex justify-between items-center mb-6">
            <h1 class="text-2xl font-bold">Gerenciamento de Obras</h1>
            <button
              class="bg-red-600 hover:bg-red-700 text-white px-4 py-2 rounded-md transition-colors flex items-center"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <line x1="12" y1="5" x2="12" y2="19"></line>
                <line x1="5" y1="12" x2="19" y2="12"></line>
              </svg>
              Adicionar Obra
            </button>
          </div>

          <!-- Filtros e pesquisa -->
          <div class="bg-gray-800 rounded-lg shadow-lg p-4 mb-6">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
              <div class="md:col-span-2">
                <label for="search" class="block text-sm font-medium text-gray-400 mb-1">Pesquisar</label>
                <div class="relative">
                  <input
                    type="text"
                    id="search"
                    placeholder="Buscar por título ou autor..."
                    class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 text-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent pl-10"
                  />
                  <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                      <circle cx="11" cy="11" r="8"></circle>
                      <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
                    </svg>
                  </div>
                </div>
              </div>

              <div>
                <label for="status-filter" class="block text-sm font-medium text-gray-400 mb-1">Status</label>
                <select
                  id="status-filter"
                  class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 text-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                >
                  <option value="all">Todos</option>
                  <option value="ongoing">Em Andamento</option>
                  <option value="completed">Concluído</option>
                  <option value="hiatus">Hiato</option>
                </select>
              </div>

              <div>
                <label for="sort-by" class="block text-sm font-medium text-gray-400 mb-1">Ordenar por</label>
                <select
                  id="sort-by"
                  class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 text-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                >
                  <option value="title">Título</option>
                  <option value="author">Autor</option>
                  <option value="chapters">Capítulos</option>
                  <option value="views">Visualizações</option>
                  <option value="rating">Avaliação</option>
                  <option value="lastUpdated">Última Atualização</option>
                </select>
              </div>
            </div>
          </div>

          <!-- Tabela de mangás -->
          <div class="bg-gray-800 rounded-lg shadow-lg overflow-hidden mb-6">
            <div class="overflow-x-auto">
              <table class="min-w-full divide-y divide-gray-700">
                <thead class="bg-gray-700">
                  <tr>
                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-300 uppercase tracking-wider">
                      Obra
                    </th>
                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-300 uppercase tracking-wider hidden md:table-cell">
                      Autor
                    </th>
                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-300 uppercase tracking-wider hidden md:table-cell">
                      Status
                    </th>
                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-300 uppercase tracking-wider hidden lg:table-cell">
                      Capítulos
                    </th>
                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-300 uppercase tracking-wider hidden lg:table-cell">
                      Visualizações
                    </th>
                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-300 uppercase tracking-wider hidden lg:table-cell">
                      Avaliação
                    </th>
                    <th scope="col" class="px-6 py-3 text-right text-xs font-medium text-gray-300 uppercase tracking-wider">
                      Ações
                    </th>
                  </tr>
                </thead>
                <tbody class="bg-gray-800 divide-y divide-gray-700">
                  {#each mangas as manga}
                    <tr class="hover:bg-gray-700">
                      <td class="px-6 py-4 whitespace-nowrap">
                        <div class="flex items-center">
                          <div class="h-10 w-10 flex-shrink-0">
                            <img class="h-10 w-10 rounded object-cover" src={manga.cover || "/placeholder.svg"} alt={manga.title} />
                          </div>
                          <div class="ml-4">
                            <div class="text-sm font-medium">{manga.title}</div>
                            <div class="text-sm text-gray-400 md:hidden">{manga.author}</div>
                          </div>
                        </div>
                      </td>
                      <td class="px-6 py-4 whitespace-nowrap hidden md:table-cell">
                        <div class="text-sm">{manga.author}</div>
                      </td>
                      <td class="px-6 py-4 whitespace-nowrap hidden md:table-cell">
                        <span class={`px-2 inline-flex text-xs leading-5 font-semibold rounded-full
                          ${manga.status === 'ongoing' ? 'bg-green-100 text-green-800' :
                          manga.status === 'completed' ? 'bg-blue-100 text-blue-800' :
                          'bg-yellow-100 text-yellow-800'}`}>
                          {manga.status === 'ongoing' ? 'Em Andamento' :
                           manga.status === 'completed' ? 'Concluído' : 'Hiato'}
                        </span>
                      </td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm hidden lg:table-cell">
                        {manga.chapters}
                      </td>
                      <td class="px-6 py-4 whitespace-nowrap text-sm hidden lg:table-cell">
                        {formatNumber(manga.views)}
                      </td>
                      <td class="px-6 py-4 whitespace-nowrap hidden lg:table-cell">
                        <div class="flex items-center">
                          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-yellow-400" viewBox="0 0 20 20" fill="currentColor">
                            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                          </svg>
                          <span class="ml-1">{manga.rating}</span>
                        </div>
                      </td>
                      <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                        <div class="flex justify-end space-x-2">
                          <button class="text-indigo-400 hover:text-indigo-300 transition-colors">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                              <path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path>
                              <path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path>
                            </svg>
                          </button>
                          <button class="text-red-400 hover:text-red-300 transition-colors">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                              <polyline points="3 6 5 6 21 6"></polyline>
                              <path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path>
                              <line x1="10" y1="11" x2="10" y2="17"></line>
                              <line x1="14" y1="11" x2="14" y2="17"></line>
                            </svg>
                          </button>
                        </div>
                      </td>
                    </tr>
                  {/each}
                </tbody>
              </table>
            </div>

            <!-- Paginação -->
            <div class="px-6 py-3 flex items-center justify-between border-t border-gray-700">
              <div class="flex-1 flex justify-between sm:hidden">
                <button class="relative inline-flex items-center px-4 py-2 border border-gray-600 text-sm font-medium rounded-md text-gray-300 bg-gray-700 hover:bg-gray-600">
                  Anterior
                </button>
                <button class="ml-3 relative inline-flex items-center px-4 py-2 border border-gray-600 text-sm font-medium rounded-md text-gray-300 bg-gray-700 hover:bg-gray-600">
                  Próximo
                </button>
              </div>
              <div class="hidden sm:flex-1 sm:flex sm:items-center sm:justify-between">
                <div>
                  <p class="text-sm text-gray-400">
                    Mostrando <span class="font-medium">1</span> a <span class="font-medium">8</span> de <span class="font-medium">12</span> resultados
                  </p>
                </div>
                <div>
                  <nav class="relative z-0 inline-flex rounded-md shadow-sm -space-x-px" aria-label="Pagination">
                    <button class="relative inline-flex items-center px-2 py-2 rounded-l-md border border-gray-600 bg-gray-700 text-sm font-medium text-gray-300 hover:bg-gray-600">
                      <span class="sr-only">Primeira</span>
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <polyline points="11 17 6 12 11 7"></polyline>
                        <polyline points="18 17 13 12 18 7"></polyline>
                      </svg>
                    </button>
                    <button class="relative inline-flex items-center px-2 py-2 border border-gray-600 bg-gray-700 text-sm font-medium text-gray-300 hover:bg-gray-600">
                      <span class="sr-only">Anterior</span>
                      <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                        <path fill-rule="evenodd" d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd" />
                      </svg>
                    </button>

                    <button class="relative inline-flex items-center px-4 py-2 border border-gray-600 bg-red-600 text-sm font-medium text-white">
                      1
                    </button>
                    <button class="relative inline-flex items-center px-4 py-2 border border-gray-600 bg-gray-700 text-sm font-medium text-gray-300 hover:bg-gray-600">
                      2
                    </button>

                    <button class="relative inline-flex items-center px-2 py-2 border border-gray-600 bg-gray-700 text-sm font-medium text-gray-300 hover:bg-gray-600">
                      <span class="sr-only">Próximo</span>
                      <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                        <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd" />
                      </svg>
                    </button>
                    <button class="relative inline-flex items-center px-2 py-2 rounded-r-md border border-gray-600 bg-gray-700 text-sm font-medium text-gray-300 hover:bg-gray-600">
                      <span class="sr-only">Última</span>
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <polyline points="13 17 18 12 13 7"></polyline>
                        <polyline points="6 17 11 12 6 7"></polyline>
                      </svg>
                    </button>
                  </nav>
                </div>
              </div>
            </div>
          </div>
        </div>
      {:else if activeSection === 'capitulos'}
        <!-- Gerenciamento de Capítulos -->
        <div>
          <h1 class="text-2xl font-bold mb-6">Gerenciamento de Capítulos</h1>
          <div class="bg-gray-800 rounded-lg shadow-lg p-6 text-center">
            <p class="text-gray-400">Selecione uma obra para gerenciar seus capítulos.</p>
          </div>
        </div>
      {:else if activeSection === 'categorias'}
        <!-- Gerenciamento de Categorias -->
        <div>
          <h1 class="text-2xl font-bold mb-6">Gerenciamento de Categorias</h1>
          <div class="bg-gray-800 rounded-lg shadow-lg p-6">
            <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
              {#each availableCategories as category}
                <div class="bg-gray-700 rounded-lg p-4 flex justify-between items-center">
                  <span>{category}</span>
                  <div class="flex space-x-2">
                    <button class="text-indigo-400 hover:text-indigo-300 transition-colors">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path>
                        <path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path>
                      </svg>
                    </button>
                    <button class="text-red-400 hover:text-red-300 transition-colors">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <polyline points="3 6 5 6 21 6"></polyline>
                        <path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path>
                      </svg>
                    </button>
                  </div>
                </div>
              {/each}
            </div>
          </div>
        </div>
      {:else if activeSection === 'usuarios' || activeSection === 'comentarios' || activeSection === 'configuracoes'}
        <!-- Outras seções -->
        <div>
          <h1 class="text-2xl font-bold mb-6">Gerenciamento de {activeSection.charAt(0).toUpperCase() + activeSection.slice(1)}</h1>
          <div class="bg-gray-800 rounded-lg shadow-lg p-6 text-center">
            <p class="text-gray-400">Esta seção está em desenvolvimento.</p>
          </div>
        </div>
      {/if}
    </main>
  </div>
</div>

<style>
  :global(body) {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
</style>