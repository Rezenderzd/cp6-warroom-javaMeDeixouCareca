# FICHA DE DECISÕES · War Room FiapBank (CP6 · 3 aulas)

> Este arquivo é o **README.md do repositório do grupo** (`cp6-warroom-<nome-do-grupo>`).
> Vale **5,0 pontos** (rodadas 0,5 · relâmpagos 0,3), e a nota é pela
> **justificativa**, não pela letra. Preencham após cada aula e commitem até
> **23h59 do mesmo dia** (regras completas na seção 5 do enunciado).
>
> **Os incidentes da madrugada são revelados só em aula.** O título de cada registro
> será **ditado pelo professor na hora**; ninguém se antecipe.

**Grupo (nome da equipe plantonista):** javaMeDeixouCareca

**Turma:** 2CCPO **Repo:** `cp6-warroom-javaMeDeixouCareca`

**Integrantes (nome + RM):**

| Nome | RM |
|---|---|
| Fernando Caires Silva | 563415 |
| Guilherme Martins Rezende | 563500 |
|Gregory Debom Ferreira | 562346 |
| Gustavo Hackime Costa | 563751 |
| Luiz Henrique Barbosa Dias|562399 |
|Raphael Mischiatti de Souza | 563567 |

## 0. Setup do repositório (antes da 1ª aula; podem apagar esta seção depois)

1. Um integrante cria o repo **público** no GitHub: `cp6-warroom-<nome-do-grupo>`
   (ex.: `cp6-warroom-debugadores`), com um README qualquer
2. Substituam o conteúdo do `README.md` por este template (no navegador, pelo próprio
   GitHub, ou clonando):
   ```bash
   git clone https://github.com/<conta>/cp6-warroom-<nome-do-grupo>.git
   cd cp6-warroom-<nome-do-grupo>
   # substitua o conteúdo do README.md por este template e:
   git add .
   git commit -m "chore: ficha em branco do grupo"
   git push
   ```
3. Postem o **link no Teams** (o mesmo link para todo o grupo)

**Convenção de commits** (1 commit por rodada; relâmpagos podem ir junto com a
rodada seguinte):

```
decisao: R1 - opcao C (<resumo da justificativa em uma frase>)
decisao: R2 - opcao A (<resumo em uma frase>)
pos-mortem: relatorio de incidente da madrugada
```

---

## 📁 Dossiê técnico do FiapBank (MVP em produção)

**Stack:** Java 17 + Spring Boot + Spring Data JPA + Oracle. API com endpoints em
`/api/contas` e `/api/transferencias` (cenário visto desde a Aula 13).

**Contrato e regras de negócio que o banco prometeu aos clientes e aos reguladores:**

| Regra | Como deve ser |
|---|---|
| Transferência **PIX** | taxa **R$ 0,00** |
| Transferência **TED** | taxa fixa **R$ 5,00** |
| Saldo | **nunca fica negativo**: transferência/saque sem saldo é recusado com erro claro |
| Número de conta | **sequencial e único** (1001, 1002, 1003...), gerado pelo sistema |
| Extrato de transferência | grava **quem pagou** e **quem recebeu**, na ordem certa |
| CPF | **dado sensível**: nunca aparece nas respostas da API |
| Consultas ao banco | sempre parametrizadas, e cada operação **usa e libera** a conexão |
| Suíte de testes | roda antes de todo deploy; **verde** é pré-requisito pra subir |

**Como escrever a justificativa:** nomeie o **mecanismo técnico** em jogo (o
conceito das Aulas 11 a 15 que explica o incidente) e o **trade-off** (velocidade ×
segurança × faturamento × dívida). "Porque é mais seguro" não é justificativa.

---

# 📝 REGISTRO DE DECISÕES

> A cada incidente, o professor dita o título (ex.: "Rodada 1"). **Copiem o modelo
> abaixo, colem no fim desta seção** e preencham com o rascunho feito em aula, junto
> com o **placar do grupo** após a consequência. Commitem 1 commit por rodada até
> 23h59 do dia.
>
> **Eventos relâmpago:** registrem apenas se o grupo for **afetado** (o professor
> chama quem for; não ser chamado é bom sinal).

**Modelo (copiar para cada decisão):**

```
## <título ditado pelo professor>

**Tipo:** ( rodada / relâmpago ) · **Voto:** ( A / B / C / D )

**Justificativa:**

<2 a 3 linhas: mecanismo técnico + trade-off>

**Placar do grupo após esta decisão:** 🔥 __ · 💰 R$ __ mil · 🧹 __
```

*(as decisões entram aqui, na ordem em que a madrugada as trouxer; placar inicial:
🔥 7 · 💰 0 · 🧹 2)*

---

## 🔎 O caminho do MEU grupo (preencher na 3ª aula, quando o mapa for revelado)

Uma linha por decisão registrada acima (usem os títulos ditados em aula):

| # | Decisão | Nossa letra | Consequência que ELA teria tido |
|---|---|---|---|
| | | | |
| | | | |
| | | | |

*(adicionem linhas conforme as decisões da madrugada)*

*(as decisões entram aqui, na ordem em que a madrugada as trouxer; placar inicial:
🔥 7 · 💰 0 · 🧹 2)*


## O saldo que virou negativo (19h12) 

**Tipo:**  rodada  · **Voto:** (C)

**Justificativa:** Corrigir o código em questão é uma questão simples de alterar uma única linha de código. Além disso, escrever os testes unitários não é uma tarefa que demanda muito tempo e evita efeito rebote no futuro.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1


## A injeção que derreteu o banco (21h02) 
 
**Tipo:** rodada · **Voto:** (D)
 
**Justificativa:** Utilizar o Spring, embora seja mais demorado por necessitar a limpeza do código anterior, ajuda na manutenibilidade futura do código e evita problemas de retrabalho, uma vez que possui proteção contra SQL Injection embutida.
 
**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 0
 

 ## A noite das contas gêmeas (22h50)
 
**Tipo:** rodada  · **Voto:** (D)
 
**Justificativa:** Delegar a numeração para o banco de dados evita que os UUID recomecem caso a aplicação caia e a instância do Singleton deixe de existir. Desse modo, o banco de dados consegue sempre seguir a sequência mesmo que esteja fora do ar, já que seus dados persistem.
 
**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 45 mil · 🧹 0


## O comprovante que aponta pra pessoa errada (00h47)
 
**Tipo:** rodada  · **Voto:** (A)
 
**Justificativa:** Nossa responsabilidade é corrigir o código para a black friday, o banco de dados pode ser corrigido por outro departamento em outro momento.
 
**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 60 mil · 🧹 1

## A fábrica que devolve null (01h30)
 
**Tipo:** rodada  · **Voto:** (B)
 
**Justificativa:** É melhor fazer a validação diretamente no Controller, além disso, se a validação for feita antes de chamar a função, o código não vai rodar coisas desnecessárias, já que vai ocorrer uma Exception antes.
 
**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 60 mil · 🧹 2

## O cadastro com metade dos campos (02h20)
 
**Tipo:** relâmpago  · **Voto:** (B)
 
**Justificativa:** Com os valores padronizados no builder, fica mais fácil de fazer a correção pós black friday, mesmo que seja mais demorado do que implementar um construtor sobrecarregado, é preciso pensar na manutenção que será feita pós o evento.
 
**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 60 mil · 🧹 2


## O teste vermelho às 03h45 (a janela fecha às 04h)
 
**Tipo:** rodada  · **Voto:** (A)
 
**Justificativa:** Como estamos com pouco tempo e a regra de negócio diz que todos os testes devem passar, consideramos desabilita-lo e esperar a black friday passar para resolver o erro, o grupo considera essa decisão melhor em relação a perder a janela de deploy
 
**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 60 mil · 🧹 3

---

# 📋 PÓS-MORTEM · relatório de incidente (montar em sala na 3ª aula)

> Rascunho em aula e commit final `pos-mortem:` até 23h59 do dia da 3ª aula.

## 1. Linha do tempo da madrugada

_______________________________________________________________________________________

_______________________________________________________________________________________

_______________________________________________________________________________________

## 2. Causa raiz de 2 incidentes (aula + mecanismo técnico)

**Incidente 1:** _______________________________________________

Aula/mecanismo:

_______________________________________________________________________________________

**Incidente 2:** _______________________________________________

Aula/mecanismo:

_______________________________________________________________________________________

## 3. O que faríamos diferente (2 rodadas + por quê)

_______________________________________________________________________________________

_______________________________________________________________________________________

## 4. A maior lição da equipe

_______________________________________________________________________________________
