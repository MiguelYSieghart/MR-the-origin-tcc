<script>
  import { onMount } from 'svelte';

  let activeTab = 'login';

  let loginForm = {
    email: '',
    password: '',
    rememberMe: false
  };

  let registerForm = {
    username: '',
    email: '',
    password: '',
    confirmPassword: '',
    acceptTerms: false
  };
  let loginErrors = {};
  let registerErrors = {};
  let isSubmitting = false;


  function setActiveTab(tab) {
    activeTab = tab;
    loginErrors = {};
    registerErrors = {};
  }

  function validateLoginForm() {
    const errors = {};

    if (!loginForm.email) {
      errors.email = 'E-mail é obrigatório';
    } else if (!/\S+@\S+\.\S+/.test(loginForm.email)) {
      errors.email = 'E-mail inválido';
    }

    if (!loginForm.password) {
      errors.password = 'Senha é obrigatória';
    } else if (loginForm.password.length < 6) {
      errors.password = 'Senha deve ter pelo menos 6 caracteres';
    }

    return errors;
  }

  function validateRegisterForm() {
    const errors = {};

    if (!registerForm.username) {
      errors.username = 'Nome de usuário é obrigatório';
    } else if (registerForm.username.length < 3) {
      errors.username = 'Nome de usuário deve ter pelo menos 3 caracteres';
    }

    if (!registerForm.email) {
      errors.email = 'E-mail é obrigatório';
    } else if (!/\S+@\S+\.\S+/.test(registerForm.email)) {
      errors.email = 'E-mail inválido';
    }

    if (!registerForm.password) {
      errors.password = 'Senha é obrigatória';
    } else if (registerForm.password.length < 6) {
      errors.password = 'Senha deve ter pelo menos 6 caracteres';
    }

    if (!registerForm.confirmPassword) {
      errors.confirmPassword = 'Confirmação de senha é obrigatória';
    } else if (registerForm.password !== registerForm.confirmPassword) {
      errors.confirmPassword = 'As senhas não coincidem';
    }

    if (!registerForm.acceptTerms) {
      errors.acceptTerms = 'Você deve aceitar os termos de uso';
    }

    return errors;
  }

  async function handleLoginSubmit() {
    loginErrors = validateLoginForm();

    if (Object.keys(loginErrors).length === 0) {
      isSubmitting = true;

      try {

        await new Promise(resolve => setTimeout(resolve, 1000));
        console.log('Login submetido:', loginForm);

        window.location.href = '/';
      } catch (error) {
        console.error('Erro ao fazer login:', error);
        loginErrors.general = 'Falha ao fazer login. Verifique suas credenciais.';
      } finally {
        isSubmitting = false;
      }
    }
  }

  async function handleRegisterSubmit() {
    registerErrors = validateRegisterForm();

    if (Object.keys(registerErrors).length === 0) {
      isSubmitting = true;

      try {
        await new Promise(resolve => setTimeout(resolve, 1000));
        console.log('Cadastro submetido:', registerForm);

        alert('Cadastro realizado com sucesso! Faça login para continuar.');
        setActiveTab('login');
      } catch (error) {
        console.error('Erro ao fazer cadastro:', error);
        registerErrors.general = 'Falha ao criar conta. Tente novamente mais tarde.';
      } finally {
        isSubmitting = false;
      }
    }
  }


  function handleSocialLogin(provider) {
    console.log(`Login com ${provider}`);
  }

  onMount(() => {
    const urlParams = new URLSearchParams(window.location.search);
    const tab = urlParams.get('tab');
    if (tab === 'register') {
      setActiveTab('register');
    }
  });
</script>

<div class="min-h-screen bg-gray-900 text-white flex flex-col">
  <!-- Cabeçalho simplificado -->
  <header class="bg-gray-800 shadow-lg">
    <div class="container mx-auto px-4 py-3">
      <div class="flex items-center">
        <a href="/" class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-red-500" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M4 19.5v-15A2.5 2.5 0 0 1 6.5 2H20v20H6.5a2.5 2.5 0 0 1 0-5H20"></path>
          </svg>
          <span class="ml-2 text-xl font-bold">MangáReader</span>
        </a>
      </div>
    </div>
  </header>

  <!-- Conteúdo principal -->
  <main class="flex-grow flex items-center justify-center py-12 px-4">
    <div class="w-full max-w-md">
      <!-- Card de autenticação -->
      <div class="bg-gray-800 rounded-lg shadow-xl overflow-hidden">
        <!-- Abas -->
        <div class="flex border-b border-gray-700">
          <button
            class={`flex-1 py-4 text-center font-medium transition-colors ${activeTab === 'login' ? 'bg-gray-700 text-white' : 'text-gray-400 hover:text-white hover:bg-gray-700'}`}
            on:click={() => setActiveTab('login')}
          >
            Login
          </button>
          <button
            class={`flex-1 py-4 text-center font-medium transition-colors ${activeTab === 'register' ? 'bg-gray-700 text-white' : 'text-gray-400 hover:text-white hover:bg-gray-700'}`}
            on:click={() => setActiveTab('register')}
          >
            Cadastro
          </button>
        </div>

        <!-- Formulário de Login -->
        {#if activeTab === 'login'}
          <div class="p-6">
            <h2 class="text-2xl font-bold mb-6 text-center">Bem-vindo de volta!</h2>

            {#if loginErrors.general}
              <div class="mb-4 p-3 bg-red-900/50 border border-red-500 rounded-md text-sm">
                {loginErrors.general}
              </div>
            {/if}

            <form on:submit|preventDefault={handleLoginSubmit} class="space-y-4">
              <!-- Email -->
              <div>
                <label for="login-email" class="block text-sm font-medium mb-1">E-mail</label>
                <input
                  type="email"
                  id="login-email"
                  bind:value={loginForm.email}
                  class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 text-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                  placeholder="seu@email.com"
                />
                {#if loginErrors.email}
                  <p class="mt-1 text-red-400 text-xs">{loginErrors.email}</p>
                {/if}
              </div>

              <!-- Senha -->
              <div>
                <div class="flex justify-between items-center mb-1">
                  <label for="login-password" class="block text-sm font-medium">Senha</label>
                  <a href="/recuperar-senha" class="text-xs text-red-400 hover:text-red-300 transition-colors">
                    Esqueceu a senha?
                  </a>
                </div>
                <input
                  type="password"
                  id="login-password"
                  bind:value={loginForm.password}
                  class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 text-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                  placeholder="••••••••"
                />
                {#if loginErrors.password}
                  <p class="mt-1 text-red-400 text-xs">{loginErrors.password}</p>
                {/if}
              </div>

              <!-- Lembrar-me -->
              <div class="flex items-center">
                <input
                  type="checkbox"
                  id="remember-me"
                  bind:checked={loginForm.rememberMe}
                  class="h-4 w-4 rounded border-gray-600 bg-gray-700 text-red-600 focus:ring-red-500"
                />
                <label for="remember-me" class="ml-2 block text-sm text-gray-300">
                  Lembrar-me
                </label>
              </div>

              <!-- Botão de Login -->
              <button
                type="submit"
                class="w-full bg-red-600 hover:bg-red-700 text-white py-2 px-4 rounded-md font-medium transition-colors focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2 focus:ring-offset-gray-800 disabled:opacity-50"
                disabled={isSubmitting}
              >
                {isSubmitting ? 'Entrando...' : 'Entrar'}
              </button>
            </form>

            <!-- Separador -->
            <div class="relative my-6">
              <div class="absolute inset-0 flex items-center">
                <div class="w-full border-t border-gray-600"></div>
              </div>
              <div class="relative flex justify-center text-sm">
                <span class="px-2 bg-gray-800 text-gray-400">ou continue com</span>
              </div>
            </div>

            <!-- Botões de login social -->
            <div class="grid grid-cols-2 gap-3">
              <button
                type="button"
                on:click={() => handleSocialLogin('google')}
                class="flex items-center justify-center py-2 px-4 bg-gray-700 hover:bg-gray-600 rounded-md transition-colors"
              >
                <svg class="w-5 h-5 mr-2" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M12.545 10.239v3.821h5.445c-.712 2.315-2.647 3.972-5.445 3.972a6.033 6.033 0 110-12.064c1.498 0 2.866.549 3.921 1.453l2.814-2.814A9.969 9.969 0 0012.545 2C7.021 2 2.543 6.477 2.543 12s4.478 10 10.002 10c8.396 0 10.249-7.85 9.426-11.748l-9.426-.013z" />
                </svg>
                Google
              </button>
              <button
                type="button"
                on:click={() => handleSocialLogin('facebook')}
                class="flex items-center justify-center py-2 px-4 bg-gray-700 hover:bg-gray-600 rounded-md transition-colors"
              >
                <svg class="w-5 h-5 mr-2" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z" />
                </svg>
                Facebook
              </button>
            </div>
          </div>
        {:else}
          <!-- Formulário de Cadastro -->
          <div class="p-6">
            <h2 class="text-2xl font-bold mb-6 text-center">Crie sua conta</h2>

            {#if registerErrors.general}
              <div class="mb-4 p-3 bg-red-900/50 border border-red-500 rounded-md text-sm">
                {registerErrors.general}
              </div>
            {/if}

            <form on:submit|preventDefault={handleRegisterSubmit} class="space-y-4">
              <!-- Nome de usuário -->
              <div>
                <label for="register-username" class="block text-sm font-medium mb-1">Nome de usuário</label>
                <input
                  type="text"
                  id="register-username"
                  bind:value={registerForm.username}
                  class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 text-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                  placeholder="mangalover123"
                />
                {#if registerErrors.username}
                  <p class="mt-1 text-red-400 text-xs">{registerErrors.username}</p>
                {/if}
              </div>

              <!-- Email -->
              <div>
                <label for="register-email" class="block text-sm font-medium mb-1">E-mail</label>
                <input
                  type="email"
                  id="register-email"
                  bind:value={registerForm.email}
                  class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 text-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                  placeholder="seu@email.com"
                />
                {#if registerErrors.email}
                  <p class="mt-1 text-red-400 text-xs">{registerErrors.email}</p>
                {/if}
              </div>

              <!-- Senha -->
              <div>
                <label for="register-password" class="block text-sm font-medium mb-1">Senha</label>
                <input
                  type="password"
                  id="register-password"
                  bind:value={registerForm.password}
                  class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 text-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                  placeholder="••••••••"
                />
                {#if registerErrors.password}
                  <p class="mt-1 text-red-400 text-xs">{registerErrors.password}</p>
                {/if}
              </div>

              <!-- Confirmar Senha -->
              <div>
                <label for="register-confirm-password" class="block text-sm font-medium mb-1">Confirmar Senha</label>
                <input
                  type="password"
                  id="register-confirm-password"
                  bind:value={registerForm.confirmPassword}
                  class="w-full px-4 py-2 rounded-md bg-gray-700 border border-gray-600 text-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                  placeholder="••••••••"
                />
                {#if registerErrors.confirmPassword}
                  <p class="mt-1 text-red-400 text-xs">{registerErrors.confirmPassword}</p>
                {/if}
              </div>

              <!-- Termos e Condições -->
              <div class="flex items-start">
                <div class="flex items-center h-5">
                  <input
                    type="checkbox"
                    id="accept-terms"
                    bind:checked={registerForm.acceptTerms}
                    class="h-4 w-4 rounded border-gray-600 bg-gray-700 text-red-600 focus:ring-red-500"
                  />
                </div>
                <div class="ml-3 text-sm">
                  <label for="accept-terms" class="text-gray-300">
                    Eu aceito os <a href="/termos" class="text-red-400 hover:text-red-300 transition-colors">Termos de Serviço</a> e a <a href="/privacidade" class="text-red-400 hover:text-red-300 transition-colors">Política de Privacidade</a>
                  </label>
                  {#if registerErrors.acceptTerms}
                    <p class="mt-1 text-red-400 text-xs">{registerErrors.acceptTerms}</p>
                  {/if}
                </div>
              </div>

              <!-- Botão de Cadastro -->
              <button
                type="submit"
                class="w-full bg-red-600 hover:bg-red-700 text-white py-2 px-4 rounded-md font-medium transition-colors focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2 focus:ring-offset-gray-800 disabled:opacity-50"
                disabled={isSubmitting}
              >
                {isSubmitting ? 'Cadastrando...' : 'Criar Conta'}
              </button>
            </form>

            <!-- Separador -->
            <div class="relative my-6">
              <div class="absolute inset-0 flex items-center">
                <div class="w-full border-t border-gray-600"></div>
              </div>
              <div class="relative flex justify-center text-sm">
                <span class="px-2 bg-gray-800 text-gray-400">ou continue com</span>
              </div>
            </div>

            <!-- Botões de cadastro social -->
            <div class="grid grid-cols-2 gap-3">
              <button
                type="button"
                on:click={() => handleSocialLogin('google')}
                class="flex items-center justify-center py-2 px-4 bg-gray-700 hover:bg-gray-600 rounded-md transition-colors"
              >
                <svg class="w-5 h-5 mr-2" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M12.545 10.239v3.821h5.445c-.712 2.315-2.647 3.972-5.445 3.972a6.033 6.033 0 110-12.064c1.498 0 2.866.549 3.921 1.453l2.814-2.814A9.969 9.969 0 0012.545 2C7.021 2 2.543 6.477 2.543 12s4.478 10 10.002 10c8.396 0 10.249-7.85 9.426-11.748l-9.426-.013z" />
                </svg>
                Google
              </button>
              <button
                type="button"
                on:click={() => handleSocialLogin('facebook')}
                class="flex items-center justify-center py-2 px-4 bg-gray-700 hover:bg-gray-600 rounded-md transition-colors"
              >
                <svg class="w-5 h-5 mr-2" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z" />
                </svg>
                Facebook
              </button>
            </div>
          </div>
        {/if}
      </div>

      <!-- Link para alternar entre login e cadastro -->
      <div class="mt-6 text-center text-sm text-gray-400">
        {#if activeTab === 'login'}
          Não tem uma conta?
          <button
            on:click={() => setActiveTab('register')}
            class="text-red-400 hover:text-red-300 transition-colors font-medium"
          >
            Cadastre-se
          </button>
        {:else}
          Já tem uma conta?
          <button
            on:click={() => setActiveTab('login')}
            class="text-red-400 hover:text-red-300 transition-colors font-medium"
          >
            Faça login
          </button>
        {/if}
      </div>
    </div>
  </main>

  <!-- Rodapé simplificado -->
  <footer class="bg-gray-800 py-4 border-t border-gray-700">
    <div class="container mx-auto px-4 text-center">
      <p class="text-gray-400 text-sm">© {new Date().getFullYear()} MangáReader. Todos os direitos reservados.</p>
    </div>
  </footer>
</div>

<style>
  :global(body) {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
</style>