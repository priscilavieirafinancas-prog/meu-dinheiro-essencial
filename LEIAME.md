# OrganizaSaldo — Controle Financeiro Pessoal · Atualização e guia

Desenvolvido por Priscila Vieira · © 2026 Priscila Vieira. Todos os direitos reservados. Licença de uso pessoal.

## PARTE 1 — Para você (vendedora): configurar uma única vez (custo zero)

### A) Hospedagem gratuita (obrigatória: o Google só funciona em endereço https próprio)
1. Crie uma conta gratuita no **GitHub** (ou Cloudflare Pages / Netlify).
2. Crie um repositório e envie os 4 arquivos desta pasta: `index.html`, `sw.js`, `manifest.webmanifest`, `icon.svg`.
3. GitHub: *Settings → Pages → Deploy from a branch → main / root*. Anote o endereço (ex.: `https://seunome.github.io/meu-dinheiro/`).

### B) Login com Google (gratuito)
1. Acesse console.cloud.google.com → crie um projeto "OrganizaSaldo".
2. *APIs e serviços → Biblioteca* → ative **Google Drive API**.
3. *Tela de consentimento OAuth*: tipo **Externo**; nome do app, e-mail de suporte; em *Escopos* adicione **somente** `.../auth/drive.appdata`.
4. Clique em **Publicar app** (status *Em produção*). Em "Testando" só 100 usuários cadastrados à mão conseguem entrar.
5. *Credenciais → Criar credenciais → ID do cliente OAuth → Aplicativo da Web*. Em **Origens JavaScript autorizadas** coloque o endereço do passo A (sem barra no final).
6. Copie o **ID do cliente** (termina em `.apps.googleusercontent.com`). Ele é público; não existe chave secreta neste app.
7. O ID público do Google já está preenchido no arquivo `config.js`. Para futuras alterações, edite somente `config.js`.

### C) O que o Google exige (conferido na documentação do Google em nov/2026 — confirme no seu console)
- O escopo `drive.appdata` é classificado pelo Google como **não sensível**; por isso, a publicação **não exige a análise de verificação** de escopos sensíveis. A verificação de marca (nome/logotipo) é opcional.
- Pode aparecer o aviso de "app não verificado" se o Google pedir verificação de marca ou de domínio; confirme no console após publicar.
- Se algum dia você pedir outro escopo (ex.: ver todos os arquivos do Drive), a análise passa a ser obrigatória.
- Teste com **uma conta Google comum** (não a sua de desenvolvedora) antes de vender.
- Entregue ao comprador o **link** do app; ele usa a conta Google dele e cada um enxerga só os próprios dados.

### D) Testes que só você pode fazer (ainda NÃO foram feitos)
Chrome → Edge, celular → computador, offline → online, instalação do atalho. Veja a lista na resposta do Claude.

## PARTE 2 — Guia do comprador (3 passos)
1. **Abra o link** e toque em **Conectar com Google**. Autorize. Pronto: a mensagem **“✓ Tudo salvo”** aparece no topo sempre que seus dados estiverem protegidos.
2. **Use normalmente.** Cada lançamento é salvo na hora e enviado ao seu Google Drive sozinho. Sem internet, continue usando: aparece “Sem internet: dados guardados neste aparelho” e tudo é enviado quando a internet voltar.
3. **Em outro aparelho**, abra o mesmo link, toque em **Conectar com Google** com a **mesma conta** e seus dados aparecem.

Dicas: instale o app (Chrome/Edge: ícone de instalar na barra de endereço; Android: menu ⋮ → *Instalar app*). Em *Configurações* há **Versões anteriores** (uma cópia por dia, 14 dias) e o botão **FAZER BACKUP** (arquivo seu, guarde onde quiser).
Se a conexão com o Google expirar (acontece após cerca de 1 hora), toque em **Conectar com Google** de novo; seus dados continuam salvos no aparelho.
Evite usar o mesmo lançamento nos dois aparelhos **sem internet ao mesmo tempo**: o app junta tudo sem perder nada, mas confira o aviso vermelho se aparecer.

## Migração dos dados da versão antiga
Abra a versão nova **no mesmo navegador** da antiga: os dados locais continuam ali. Ao conectar com o Google, o app guarda uma cópia (Configurações → Desfazer última restauração), junta os dados locais com os da nuvem e **nunca apaga nada**. Se os dados estiverem em outro navegador, use FAZER BACKUP lá e Restaurar backup aqui.

---
## ATUALIZAR O GITHUB (versão OrganizaSaldo) — sem perder nada
1. **Antes de substituir**, abra o `index.html` que está hoje no GitHub, localize `const GCLIENT='...'` e copie o ID (termina em `.apps.googleusercontent.com`).
2. No GitHub envie **todos os arquivos desta pasta**: `index.html`, `sw.js`, `manifest.webmanifest`, `icon.svg`, `icon-192.png`, `icon-512.png` e `config.js`.
3. O arquivo `config.js` já está preenchido com o ID público OAuth existente. Envie-o junto com os outros arquivos; não coloque uma chave secreta no repositório.
4. O endereço do GitHub Pages e as configurações do Google Cloud **não mudam**. Os dados dos compradores também não: as chaves de armazenamento e o arquivo do Drive são os mesmos.
5. No navegador: recarregue com Ctrl+F5 (ou limpe o cache do app instalado) para o novo nome e ícone aparecerem. O ícone instalado no celular/computador pode precisar ser reinstalado para trocar de imagem.

## Novidades desta versão
- Novo nome: **OrganizaSaldo — Controle Financeiro Pessoal**.
- Painel separa **Resultado do mês**, **Saldo disponível** (desconta aportes e soma resgates) e **Patrimônio investido**.
- Lançamentos de receitas e despesas agora podem ser **editados** e **cancelados** (e reativados). Nada é apagado: o cancelamento recalcula saldos, gráficos e contas a pagar.
- Aviso de **possível contagem dupla** quando uma despesa parece ser o mesmo dinheiro de um aporte já registrado em Investimentos.
