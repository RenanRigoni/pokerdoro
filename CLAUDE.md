# POKERDORO

Timer Pomodoro para sessões de poker. Rastreia tempo, bankroll, sessões e grind semanal (meta 40h).

## Stack

- HTML/CSS/JS puro — arquivo único `index.html`
- Sem build, sem dependências, sem framework
- Dados persistidos em `localStorage` (`pokerdoro.sessions.v2`)

## Deploy

- **GitHub:** https://github.com/RenanRigoni/pokerdoro
- **Vercel:** https://pokerdoro.vercel.app

## Workflow obrigatório após qualquer edição

Após cada correção ou feature, executar **sempre**:

```bash
git add index.html
git commit -m "descrição da mudança"
git push
vercel --prod --yes
```

Nunca deixar edição sem commit + push + deploy.

## Estrutura do index.html

- **CSS** (~1500 linhas): design tokens em `:root`, layout responsivo (breakpoints 1120px / 760px / 420px)
- **HTML**: SPA com 4 rotas via hash (`#dashboard`, `#sessions`, `#reports`, `#settings`)
- **JS** (IIFE): state machine, localStorage, timer Pomodoro, cálculos de stats

## Tokens CSS principais

| Token | Valor | Uso |
|-------|-------|-----|
| `--green` | `#35f28d` | Accent principal |
| `--btn-bg` | `#252d28` | Background botões secundários |
| `--green-bright` | `#79ffba` | Gradientes verdes |
| `--green-pale` | `#8cffbd` | Gradientes verdes claros |
| `--red-pale` | `#ff9b9b` | Status encerrada, danger links |
| `--panel` | `#1b201d` | Background panels |
| `--text` | `#f3f7f4` | Texto principal |
| `--muted` | `#a4afa8` | Texto secundário |

## State (JS)

```js
state = {
  sessionMinutes,      // duração do ciclo de sessão
  breakMinutes,        // duração do break
  mode,                // "session" | "break"
  running,             // timer ativo
  paused,              // timer pausado
  activeSessionStarted,// sessão iniciada (aguardando finalização)
  loggedCurrentSession,// sessão já salva
  sessions[],          // array de sessões salvas
}
```

## Semana de grind

- Começa segunda-feira 00h00, encerra domingo 23h59
- Meta: 40h semanais
- `getWeeklySeconds()` soma sessões salvas desta semana + tempo live do timer ativo
- Exibido no stats panel como "Grind Semanal"
