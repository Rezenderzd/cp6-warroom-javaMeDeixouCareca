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

Placar inicial: 🔥 7 · 💰 0 · 🧹 2 → placar final: 🔥 9 · 💰 R$ 100 mil · 🧹 2 (Perfil final: A Noite dos Heróis)

| # | Decisão | Nossa letra | Consequência que ELA teria tido |
|---|---|---|---|
| 1 | decisao: R1 - opcao C (garantir menos erros futuros com test) | C | Corrigimos a validação de saldo e cobrimos com teste unitário. 🔥 +1 · 💰 +35 mil · 🧹 −1 (2 → 1) |
| 2 | decisao: R1 - opcao D (melhor utilizar spring ja pronto) | D | Trocamos o SQL concatenado por Spring Data JPA com consultas parametrizadas. Foi mais lento, mas 🧹 −1 (1 → 0): zeramos a dívida técnica |
| 3 | decisao: R1 - opcao D (banco de dados gerar o UUID deixa o codigo com menos responsabilidades) | D | A numeração das contas saiu do Singleton em memória e passou para o banco, acabando com as contas duplicadas. 💰 +10 mil · 🧹 0 |
| 4 | decisao: R2 - opcao A (responsabilidade é corrigir o código) | A | Corrigimos o código, mas os comprovantes já gravados continuaram invertidos. 🔥 +1 · 💰 +15 mil · 🧹 +1 (0 → 1) |
| 5 | decisao: R2 - opcao B (melhor validar no controller e menos código para rodar) | B | Validamos no Controller, mas a fábrica continuou devolvendo `null` para outros chamadores. 🧹 +1 (1 → 2) |
| 6 | decisao: R2 - opcao B (builder padronizado facilita correção futura) | B | ⚡ Relâmpago: Builder com valores padrão. Placar inalterado (🔥 9 · 💰 60 mil · 🧹 2) |
| 7 | decisao: R2 - opcao A (melhor resolver depois pela falta de tempo disponível) | A | Desabilitamos o teste (`@Disabled`) e o deploy saiu na janela, mas a suíte verde deixou de ser confiável. 🧹 +1 (2 → 3): pico de dívida da noite |
| 8 | decisão: R3 - opcao B (contrato é sempre o que deve ser seguido) | B | ⚡ Relâmpago: mantivemos o TED a R$ 5,00, como manda o contrato. 🔥 −1 (9 → 8) |
| 9 | decisão: R3 - opcao B (prejuizo menor e menos itens para corrigir na segunda) | B | Go/No-Go: abrimos atrasado, sem tirar nenhuma forma de pagamento do ar. 🔥 +1 · 💰 +40 mil · 🧹 −1 (3 → 2) |


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

## EVENTO RELÂMPAGO E: "A taxa é 5 ou 50?" (05h58)
 
**Tipo:** relâmpago  · **Voto:** (B)
 
**Justificativa:** A prioridade é o contrato, pois essa é a regra de negócio que deve ser seguida tanto no código quanto no dia a dia.
 
**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 60 mil · 🧹 3

## Go/No-Go da Black Friday (06h15)
 
**Tipo:** rodada  · **Voto:** (B)
 
**Justificativa:** Embora ainda tenha prejuízo por abrir atrasado, esse prejuízo seria menor que tirar uma forma de pagamento por completo.
 
**Placar do grupo após esta decisão:** 🔥9 · 💰 R$ 100 mil · 🧹 2

---

# 📋 PÓS-MORTEM · relatório de incidente (montar em sala na 3ª aula)

> Rascunho em aula e commit final `pos-mortem:` até 23h59 do dia da 3ª aula.

## 1. Linha do tempo da madrugada


| Horário | Incidente | Decisão | Placar (🔥 · 💰 · 🧹) |
|---|---|---|---|
| início | — | — | 7 · 0 · 2 |
| 19h12 | O saldo que virou negativo | C: corrigir a regra + teste unitário | 8 · 35 mil · 1 |
| 21h02 | A injeção que derreteu o banco | D: migrar para Spring Data JPA | 8 · 35 mil · 0 |
| 22h50 | A noite das contas gêmeas | D: numeração gerada pelo banco | 8 · 45 mil · 0 |
| 00h47 | O comprovante que aponta pra pessoa errada | A: corrigir só o código | 9 · 60 mil · 1 |
| 01h30 | A fábrica que devolve null | B: validar no Controller | 9 · 60 mil · 2 |
| 02h20 | ⚡ O cadastro com metade dos campos | B: Builder com valores padrão | 9 · 60 mil · 2 |
| 03h45 | O teste vermelho (janela fecha às 04h) | A: desabilitar o teste e subir | 9 · 60 mil · 3 |
| 05h58 | ⚡ A taxa é 5 ou 50? | B: seguir o contrato (TED = R$ 5,00) | 8 · 60 mil · 3 |
| 06h15 | Go/No-Go da Black Friday | B: abrir atrasado, sem tirar meio de pagamento | 9 · 100 mil · 2 |

Até as 23h a equipe fez correções estruturais e a dívida técnica caiu de 2 para 0.
Depois da meia-noite, com cansaço e a janela de deploy apertando, passamos a escolher
atalhos e a dívida subiu até 3. O Go/No-Go recuperou parte dela.


## 2. Causa raiz de 2 incidentes (aula + mecanismo técnico)

**Incidente 1:** A injeção que derreteu o banco (21h02).


Aula/mecanismo: Aula 13 (JDBC / Spring Data JPA), **concatenação de SQL**

A consulta era montada concatenando a String da requisição
(`"... WHERE nome = '" + nome + "'"`). Assim, uma entrada como `' OR '1'='1` passa a fazer
parte do comando SQL: isso é **SQL Injection**. A correção é usar **consulta
parametrizada** (`PreparedStatement` com `?`, ou os métodos/`@Query` do Spring Data JPA),
que trata a entrada sempre como dado e nunca como comando. O código violava a regra do
contrato "consultas sempre parametrizadas".


**Incidente 2:** A noite das contas gêmeas (22h50)


Aula/mecanismo: Aula 15 (Padrões de projeto), **Singleton com estado em memória**.


O número da conta vinha de um contador guardado dentro de um Singleton. Esse estado vive
só enquanto a JVM está de pé. Quando a aplicação reinicia (ou sobe outra instância), o
contador volta ao valor inicial e gera de novo 1001, 1002... Sob concorrência, um
`proximo++` sem sincronização também pode entregar o mesmo número a duas threads. A
correção é tirar esse estado da aplicação: o **banco gera o número** (sequence /
`@GeneratedValue`) com **restrição de unicidade**, o que persiste entre reinícios e é
atômico.

## 3. O que faríamos diferente (2 rodadas + por quê)

**O teste vermelho às 03h45 (votamos A, desabilitar).** O `@Disabled` não corrige o bug,
só desliga o alarme. A suíte "verde" passa a mentir, o que quebra a regra "verde é
pré-requisito pra subir". Faríamos diferente: investigar o teste e, se o tempo não desse,
subir só o que estava verde em vez de trocar segurança por velocidade. Foi essa decisão
que levou a dívida ao pico da noite (🧹 3).

**O comprovante que aponta pra pessoa errada (votamos A, só o código).** O fix impediu
novos extratos invertidos, mas os já gravados continuaram com pagador e recebedor
trocados, e essa é uma regra prometida aos reguladores. Faríamos diferente: junto com o
fix, rodar um **script de correção dos dados** (UPDATE dos registros afetados, em
transação e validado), em vez de empurrar o problema para "outro departamento".


## 4. A maior lição da equipe

Atalho tomado sob pressão vira dívida, e essa dívida cobra juros na pior hora. Quando corrigimos a causa raiz (testes, consulta parametrizada, numeração no banco), a dívida técnica zerou. Quando remendamos sintomas (desabilitar teste, corrigir só metade), ela voltou a subir. Teste desabilitado é alarme de incêndio desligado.
