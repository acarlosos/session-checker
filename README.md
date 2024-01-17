
# Session Checker
Este pacote verificará se um usuário está logado em outro navegador e vai deslogar da sessão anterior.

## Installation

- Adicione o pacote com o comando abaixo:

    ```
    $ composer require acarlosos/session-checker
    ```

- Depois vamos gerar a migration com o comando artisan

    ```
    $ php artisan session:table
    $ php artisan migrate
    ```

- No arquivo de configuração .env alterar o valor da variável SESSION_DRIVER de file para database

```ENV
SESSION_DRIVER=database
```

- No arquivo AuthenticatedSessionController localizado em App\Http\Controllers\Auth na função store devemos adicionar a nossa validação.

```PHP
    /**
     * Handle an incoming authentication request.
     */
    public function store(LoginRequest $request): RedirectResponse
    {

        $request->authenticate();

        SessionChecker::check(); //Aqui acontece a validação

        $request->session()->regenerate();

        return redirect()->intended(RouteServiceProvider::HOME);
    }
```

Agora já deve estar funcionando
