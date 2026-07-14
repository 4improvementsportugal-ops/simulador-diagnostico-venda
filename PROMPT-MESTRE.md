═══════════════════════════════════════════════════════════════
PROMPT-MESTRE — GERAR SIMULADOR "DIAGNÓSTICO DE VENDA"
(2 páginas HTML + Meta Pixel + Webhook GoHighLevel)
Versão 3.0 — para VENDEDORES de casa · testada em produção
═══════════════════════════════════════════════════════════════

COMO USAR ESTE DOCUMENTO
1. Preenche SÓ o BLOCO 1. Escreve sempre DENTRO dos colchetes [ ].
2. Copia o documento INTEIRO e cola no Claude Code.
3. A IA devolve dois ficheiros prontos para GitHub Pages:
   index.html e resultado.html.

⚠️ NÃO APAGUES os BLOCOS 2 a 10. São a especificação fixa que garante
que o resultado sai sempre igual e — mais importante — que o PIXEL e o
WEBHOOK funcionam de verdade. Este simulador é DIFERENTE do "Troca de
Casa": fala com quem VENDE, e o resultado não é um score /10 — são três
eixos, uma janela de tempo e uma checklist de documentos (ver BLOCO 5).

───────────────────────────────────────────────────────────────
INSTRUÇÃO DIRETA À IA QUE VAI LER ISTO
───────────────────────────────────────────────────────────────
"Lê o documento todo antes de escrever uma única linha.

O BLOCO 3 é a parte crítica: segue a ORDEM e os TEMPOS da função
finalizar() ao detalhe. Não 'simplifiques' o redirect nem juntes o
envio do pixel ao window.location na mesma instrução — isso cancela o
evento e é o bug nº1 destes simuladores.

Três regras que NÃO podes contrariar, mesmo que te pareçam melhoráveis:
  1. O webhook vai com Content-Type: application/json. NUNCA text/plain.
  2. No resultado.html, a guarda de sessionStorage corre ANTES do
     fbq('track','PageView'). Nunca ao contrário.
  3. O evento Lead vai SEM value e SEM currency.
As três estão explicadas no BLOCO 3. Foram aprendidas a partir de bugs
reais em produção.

Entrega os dois ficheiros COMPLETOS, sem comentários a dizer 'resto do
código aqui'. Código inteiro, pronto a publicar."


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 1 — PREENCHER (o que muda em cada cliente)             ║
╚══════════════════════════════════════════════════════════════╝

NICHO:................................ [ imobiliário — vendedores ]

— Marca / cliente —
NOME DA MARCA:........................ [ ex: Nova Casa ]
SIGLA / LOGO CURTO (2-3 letras):...... [ ex: NC ]
TOM:.................................. [ luxo/sofisticado | próximo/amigável | técnico/profissional ]

— Cores (deixa vazio = paleta verde-profundo/terracota por defeito) —
COR PRINCIPAL:........................ [ ex: #0E4D45 ]
COR DESTAQUE:......................... [ ex: #C2703D ]
FUNDO:................................ [ ex: #F7F4EF ]
TEXTO ESCURO:......................... [ ex: #14201E ]

— Imagem do hero —
FOTO (URL Unsplash ou do cliente):.... [ ex: https://images.unsplash.com/photo-1600585154340-be6161a56a0c?w=900&q=85 ]
   ▸ Preferir SEMPRE uma foto real de um imóvel da carteira do cliente.
ESTATÍSTICA DO CARTÃO:................ [ ex: 7 em 10 | vendedores anunciam sem ter os documentos obrigatórios prontos ]
   ▸ Usa um número que consigas SUSTENTAR. Se não tiveres, escreve
     "SEM NÚMERO" e a IA usa uma frase sem estatística.

— Mensagem do hero —
(NÃO preencher. Título e subtítulo são gerados com copy persuasiva — ver BLOCO 2.)

— Contactos / CTAs —
WHATSAPP (internacional, só dígitos):. [ ex: 351912931023 ]
TELEFONE (Ligar agora):............... [ ex: +351912931023 ]
INSTAGRAM (URL):...................... [ ex: https://instagram.com/novacasa ]

— Integrações (SEMPRE DIFERENTES POR CLIENTE — nunca reaproveitar!) —
META PIXEL ID:........................ [ ex: 2974835026201382 ]
WEBHOOK URL (GoHighLevel):............ [ cola o URL do webhook DESTE cliente ]
NOME DA ORIGEM (no webhook):.......... [ ex: Nova Casa — Diagnóstico de Venda ]
DOMÍNIO FINAL:........................ [ ex: https://4improvementsportugal-ops.github.io/simulador-novacasa/ ]
PREFIXO TELEFÓNICO DO PAÍS:........... [ ex: 351 ]
CHAVE ÚNICA DE SESSÃO:................ [ ex: diag_novacasa — tem de ser diferente por projeto ]

— Privacidade —
LINK DA POLÍTICA DE PRIVACIDADE:...... [ cola o URL da política do cliente | ou escreve SEM LINK ]
   ▸ Se escreveres SEM LINK, a IA não cria nem liga página nenhuma.
   ▸ AVISO A QUEM PREENCHE: o Meta exige política de privacidade
     acessível em anúncios de geração de leads, e o RGPD obriga a
     informar antes de recolher dados. Sem link, a campanha fica
     exposta a rejeição de anúncios e o cliente à CNPD. A decisão é
     do cliente — mas tem de ser uma decisão informada, não um
     esquecimento.


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 2 — O QUE CONSTRUIR (especificação fixa)               ║
╚══════════════════════════════════════════════════════════════╝

Constrói um simulador de leads em formato quiz, com DUAS páginas HTML
independentes (1 ficheiro cada, CSS e JS 100% inline, sem dependências
externas além de Google Fonts e do Meta Pixel):

  index.html    → Hero + Quiz de 5 passos + banner de consentimento
  resultado.html → Página de diagnóstico com URL própria

OBJETIVO: gerar leads (enviadas ao GoHighLevel) e registar a conversão
no Meta através de uma CONVERSÃO PERSONALIZADA POR URL (regra: o URL
contém "resultado").

PROPOSTA DE VALOR (é isto que distingue este simulador):
O utilizador NÃO recebe uma nota de 0 a 10. Recebe:
  1. Uma JANELA DE TEMPO estimada até vender ("6 a 10 semanas");
  2. TRÊS EIXOS independentes em barras (Documentação · Preço vs.
     Mercado · Estado e Prontidão);
  3. Uma CHECKLIST DE DOCUMENTOS em falta, personalizada;
  4. Os TRAVÕES identificados (dinâmicos, tirados das respostas);
  5. PRÓXIMOS PASSOS ordenados pelo caso concreto dele.

───────────────────────────────────────────────────────────────
COPY DO HERO (gera tu — não é campo a preencher)
───────────────────────────────────────────────────────────────
• Ângulo: PAS (Problema → Agitação → Solução). O problema é o TEMPO
  perdido e o dinheiro deixado na mesa, não a "viabilidade".
• Título: uma PERGUNTA curta + uma segunda frase em itálico, na cor de
  destaque, com a consequência negativa.
• Subtítulo: contraste concreto (duas casas iguais, tempos diferentes)
  + a promessa de descobrir onde está a dele.
• 3 selos: "3 minutos · Sem compromisso · Resultado imediato".
• Referência de estilo (adapta ao TOM e à MARCA, não copies):
    título:    "A sua casa está pronta para ir a mercado?
                /Ou vai ficar meses à espera?/"
    subtítulo: "Duas casas iguais, na mesma rua: uma vende em 6 semanas,
                a outra fica 8 meses. A diferença raramente é o imóvel —
                é um documento em falta ou um preço mal ancorado.
                Descubra onde está a sua."
    botão:     "Começar o diagnóstico →"

───────────────────────────────────────────────────────────────
LAYOUT DO HERO — split editorial (obrigatório)
───────────────────────────────────────────────────────────────
• Fundo CLARO (cor de FUNDO), não escuro. Gradientes radiais subtis
  nos cantos, sem imagem de fundo.
• DESKTOP (≥900px): duas colunas. Texto à esquerda, foto 4:3 em cartão
  arredondado à direita, e um cartão branco sólido com a ESTATÍSTICA a
  sair pela esquerda da foto (position:absolute, left:-34px).
• MOBILE: a FOTO VEM PRIMEIRO (order:-1), como banner 16:10 com
  max-height:34svh. O cartão da estatística flutua DENTRO da foto
  (absolute, left/right 10px, bottom 10px, fundo branco translúcido +
  backdrop-filter). NUNCA por baixo a empurrar o conteúdo.
• Regra @media(max-height:700px): foto desce a 26svh, para o botão não
  sair do ecrã em iPhone SE e afins.
• Título mobile: clamp(27px, 7.4vw, 52px), line-height 1.1,
  letter-spacing -.026em, text-wrap: balance (evita linhas órfãs).
  A 2.ª frase é um <em> em display:block, itálico, cor de destaque,
  font-size .7em.
• Tudo (logo, foto, título, subtítulo, botão, selos) TEM de caber
  acima da dobra num telemóvel normal. Testa a 390×844.

───────────────────────────────────────────────────────────────
REGRAS DE UX OBRIGATÓRIAS
───────────────────────────────────────────────────────────────
• Todas as perguntas são OBRIGATÓRIAS, com validação e marcação visual
  de erro (contorno vermelho + fundo suave + mensagem) antes de avançar.
• Ao errar, faz scrollIntoView ao primeiro campo inválido.
• E-mail validado por regex. Telemóvel exige ≥ 9 dígitos.
  Nome exige ≥ 3 caracteres E um espaço (nome completo).
• Barra de progresso + contador "Passo X de 5".
• Botões "Voltar" e "Continuar". No último passo: "Ver o meu diagnóstico".
• Botão desativado enquanto envia + flag aEnviar (evita duplo lead).
• Perguntas CONDICIONAIS escondem-se e limpam o valor (ver BLOCO 4).
• Mobile-first, limpo e premium, coerente com as cores do BLOCO 1.
• Tipografia: Google Fonts — serif elegante nos títulos (ex: Fraunces)
  + sans-serif no corpo (ex: Inter).
• Acessibilidade: <label> em todos os inputs, role="group" +
  aria-labelledby nos grupos de botões, aria-hidden nos ícones
  decorativos, role="progressbar" com aria-valuenow, contraste AA.
• Performance: zero bibliotecas JS. Imagens Unsplash com ?w=900&q=85.

───────────────────────────────────────────────────────────────
BANNER DE CONSENTIMENTO (obrigatório)
───────────────────────────────────────────────────────────────
O Meta Pixel NÃO pode carregar automaticamente. A diretiva ePrivacy
exige consentimento PRÉVIO para cookies de publicidade.
• Banner fixo no fundo, com "Aceitar" e "Recusar".
• O snippet do pixel vive dentro de uma função carregarPixel(), só
  chamada depois do "Aceitar".
• A escolha guarda-se em localStorage e é respeitada nas duas páginas.
• Quem recusa faz o diagnóstico na mesma e o lead CONTINUA a ir para o
  GoHighLevel — só não é medido no Meta.


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 3 — FLUXO TÉCNICO (pixel, webhook, redirect)           ║
║ ★ A PARTE MAIS IMPORTANTE — LÊ COM ATENÇÃO ★                 ║
╚══════════════════════════════════════════════════════════════╝

Seis erros que fazem estes simuladores perder conversões e leads.
Os três primeiros são clássicos. Os três últimos foram apanhados em
produção e são silenciosos — o sistema parece funcionar e não funciona.

──────────────────────────────────────────────────────────────
ERRO Nº1 — o redirect cancela o evento do pixel
──────────────────────────────────────────────────────────────
fbq('track','Lead') envia um pedido ASSÍNCRONO. Se a página navegar
(window.location) logo a seguir, o browser CANCELA esse pedido → o lead
chega ao GHL mas NUNCA aparece no pixel.
SOLUÇÃO: dispara o evento e só redireciona ~800 ms depois, com fallback.

──────────────────────────────────────────────────────────────
ERRO Nº2 — o telemóvel não chega ao campo certo do GHL
──────────────────────────────────────────────────────────────
O GoHighLevel só mapeia sozinho quando as chaves se chamam exatamente
phone, email, name/first_name/last_name. E rejeita telemóveis com
espaços — têm de ir em E.164 (+351912345678).
SOLUÇÃO: normalizarTel() + enviar as chaves padrão ALÉM dos rótulos.

──────────────────────────────────────────────────────────────
ERRO Nº3 — lead contado a dobrar
──────────────────────────────────────────────────────────────
Disparar Lead no index E no resultado conta duas vezes.
SOLUÇÃO: Lead UMA vez, no index, com eventID único. No resultado só
PageView — é o PageView do URL /resultado que alimenta a conversão
personalizada por URL.

──────────────────────────────────────────────────────────────
ERRO Nº4 — Content-Type text/plain parte o mapping do GHL  ★
──────────────────────────────────────────────────────────────
Muitos tutoriais mandam usar Content-Type: text/plain "para evitar o
preflight CORS". É MENTIRA e é um bug grave: com text/plain o GHL NÃO
faz parse do corpo, o mapping fica VAZIO e os leads chegam sem telefone
nem email. Pior: o webhook devolve 200 OK na mesma, por isso ninguém dá
por nada durante semanas.
CORS não é problema — o endpoint LeadConnector responde ao preflight com
Allow-Origin: *.
SOLUÇÃO: Content-Type: application/json. Sempre. Sem exceção.

──────────────────────────────────────────────────────────────
ERRO Nº5 — conversões fantasma no resultado.html  ★
──────────────────────────────────────────────────────────────
Se o pixel estiver no topo do <head>, o PageView dispara antes de o
script do corpo verificar o sessionStorage. Resultado: qualquer bot,
scraper de preview de link ou pessoa que abra /resultado à mão gera uma
conversão falsa — e é exatamente o PageView deste URL que alimenta a
conversão personalizada.
SOLUÇÃO: a guarda do sessionStorage corre ANTES de carregar o pixel.
Sem dados válidos → window.location.replace('index.html') e o pixel
nunca chega a existir. Além disso, marca uma flag para o PageView só
disparar UMA vez (um refresh não pode contar segunda conversão).

──────────────────────────────────────────────────────────────
ERRO Nº6 — o score enviado como se fosse dinheiro  ★
──────────────────────────────────────────────────────────────
Mandar value:<score> + currency:'EUR' no evento Lead faz o Meta tratar
o score como RECEITA. O ROAS da conta fica poluído com euros que não
existem.
SOLUÇÃO: o evento Lead vai SEM value e SEM currency.

──────────────────────────────────────────────────────────────
META PIXEL — carregamento condicionado (nas DUAS páginas)
──────────────────────────────────────────────────────────────
No <head>, ANTES de tudo:

  var PIXEL_ID = '<PIXEL_ID>';
  var PIXEL_ATIVO = PIXEL_ID.indexOf('AQUI') === -1;   // modo demo
  var CHAVE_CONSENTIMENTO = '<CHAVE_UNICA>_cookies';

  function carregarPixel(){
    if(!PIXEL_ATIVO || window.fbq) return;
    /* snippet oficial do Meta aqui */
    fbq('init', PIXEL_ID);
    fbq('track','PageView');
  }
  function temConsentimento(){
    try { return localStorage.getItem(CHAVE_CONSENTIMENTO)==='aceite'; }
    catch(e){ return false; }
  }
  if (temConsentimento()) carregarPixel();

Advanced Matching: no momento do envio, re-inicializa com os dados do
utilizador ANTES do track('Lead'). O pixel faz o hash SHA-256 sozinho.

──────────────────────────────────────────────────────────────
index.html — finalizar() — ORDEM E TEMPOS EXATOS
──────────────────────────────────────────────────────────────
function normalizarTel(v){
  let d = (v||'').replace(/\D/g,'');
  if(!d) return '';
  if(d.indexOf('00') === 0) d = d.slice(2);        // 00351… → 351…
  if(d.length === 9) d = '<PREFIXO_PAIS>' + d;     // nº local
  return '+' + d;                                   // E.164
}

function finalizar(){
  if(aEnviar) return;                               // trava duplo clique
  aEnviar = true;
  btn.disabled = true;
  btn.textContent = 'A preparar o seu diagnóstico…';

  const D       = diagnosticar();                   // BLOCO 5
  const tel     = normalizarTel(A.tel);
  const partes  = (A.nome||'').trim().split(/\s+/);
  const first   = partes[0]||'', last = partes.slice(1).join(' ')||'';
  const eventId = 'lead-'+Date.now()+'-'+Math.random().toString(36).slice(2,8);

  // 1) guarda PRIMEIRO — a página de resultado lê daqui
  try { sessionStorage.setItem('<CHAVE_UNICA>',
        JSON.stringify({A, D, eventId, ts:Date.now()})); } catch(e){}

  // 2) Advanced Matching antes do evento
  if(PIXEL_ATIVO && typeof fbq==='function'){
    fbq('init', PIXEL_ID, { em:A.email, ph:tel, fn:first, ln:last });

    // 3) Lead UMA vez. SEM value. SEM currency. (ver ERRO Nº6)
    fbq('track','Lead', {
      content_name:'<NOME ORIGEM>', content_category:'<MARCA>'
    }, { eventID:eventId });
  }

  // 4) webhook (keepalive sobrevive ao redirect)
  enviarWebhook(tel, first, last, D, eventId);

  // 5) SÓ AGORA o redirect. Sem este atraso o window.location
  //    cancela o pedido do pixel. (ver ERRO Nº1)
  let jaFoi=false;
  const ir=()=>{ if(jaFoi) return; jaFoi=true;
                 window.location.href='resultado.html'; };
  setTimeout(ir, 800);
  setTimeout(ir, 2500);                             // fallback
}

──────────────────────────────────────────────────────────────
enviarWebhook() — payload completo
──────────────────────────────────────────────────────────────
POST para o WEBHOOK URL, com:
  headers: { 'Content-Type': 'application/json' }   ← NUNCA text/plain
  keepalive: true
  body: JSON.stringify(payload)
  .catch() a registar a falha na consola

payload:
• Chaves PADRÃO que o GHL mapeia sozinho:
    name, first_name, last_name,
    phone  ← E.164 obrigatório
    email
• Metadados:
    timestamp   : new Date().toISOString()
    origem      : '<NOME ORIGEM>'
    pagina_url  : window.location.href
    event_id    : <eventId>
    consentimento_rgpd : 'Sim' | 'Não'
• TODAS as respostas com RÓTULOS LEGÍVEIS (nunca códigos internos):
    imovel_tipo, imovel_tipologia, imovel_area, imovel_localizacao,
    imovel_ano, titularidade, acordo_venda, documentos_que_tem,
    documentos_em_falta, encargos, valor_pretendido, origem_do_valor,
    capital_em_divida, flexibilidade_preco, motivo_venda, prazo_venda,
    ocupacao, ja_no_mercado, tempo_no_mercado, quer_avaliacao
• Diagnóstico:
    score_documentacao, score_preco, score_estado, score_global,
    tempo_estimado, travoes (string separada por " | ")
• raw: { ...A }   (cópia bruta, para depuração)

Se o WEBHOOK URL vier vazio (modo demo), NÃO faças fetch: faz
console.log do payload. Assim o ficheiro abre-se localmente sem erros.

──────────────────────────────────────────────────────────────
resultado.html — a ordem no <head> é sagrada
──────────────────────────────────────────────────────────────
1º  lê o sessionStorage e o consentimento
2º  se NÃO houver dados → window.location.replace('index.html')
    e NÃO carrega pixel nenhum (ver ERRO Nº5)
3º  só se houver dados E consentimento → carrega o pixel + PageView,
    com flag '<CHAVE_UNICA>_pv' para não contar duas vezes num refresh
4º  NUNCA disparar 'Lead' aqui


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 4 — PERGUNTAS (usar tal e qual)                        ║
╚══════════════════════════════════════════════════════════════╝

Cinco passos: quatro de qualificação + um de contacto.
Cada pergunta existe porque um consultor imobiliário PRECISA da
resposta antes de pegar no telefone. Não acrescentes perguntas
"giras" — cada campo extra custa conversão.

── PASSO 1 · "Comecemos pelo imóvel" ──
• Tipo (grelha 2 col): Apartamento | Moradia | Terreno | Outro
• Tipologia (grelha 4 col): T0/T1 | T2 | T3 | T4+
      ▸ ESCONDER se tipo = Terreno
• Área aproximada (number, m², validar entre 10 e 5000)
• Localização (texto livre — concelho e freguesia)
• Ano de construção (select): Antes de 1980 | 1980–2000 | 2001–2015 |
  Depois de 2015 | Não sei ao certo

── PASSO 2 · "Quem é o dono e o que já tem em mãos" ──
   ★ É AQUI QUE ESTÁ O OURO. É onde os negócios morrem.
• Proprietário (lista): Só eu | Eu e o meu cônjuge |
  É uma herança ou partilha | Vários proprietários
• Estão todos de acordo em vender? (lista): Sim, está tudo acordado |
  Ainda não há acordo entre todos | Não sei / ainda não falámos
      ▸ MOSTRAR só se proprietário ≠ "Só eu"
• Que documentos já tem? (MULTI-SELEÇÃO, chips):
  Caderneta predial | Certidão permanente do registo |
  Licença de utilização | Certificado energético |
  Nenhum destes / não sei  ← opção EXCLUSIVA (limpa as outras)
• Encargos (lista): Não, está livre | Hipoteca — tenho crédito |
  Penhora ou processo judicial | Usufruto | Não sei

── PASSO 3 · "O preço — e de onde vem esse número" ──
• Valor pretendido (select): Até 150.000 € | 150–250k | 250–400k |
  400–600k | Mais de 600.000 € | Ainda não defini
• Como chegou a esse valor? (lista)  ★ A PERGUNTA MAIS REVELADORA
  Fiz uma avaliação profissional |
  Vi anúncios de casas parecidas |
  É o valor de que preciso para os meus planos |
  Sinceramente, não faço ideia
      ▸ Quem responde "é o que preciso" ancorou num número emocional.
        É o principal motivo de casas que não vendem.
• Capital em dívida (select): Não tenho crédito — está pago |
  Menos de 50k | 50–100k | 100–200k | Mais de 200k | Não sei
• Margem de negociação (lista): Sim, tenho alguma margem |
  Pouca — só para fechar negócio | Nenhuma, é este valor

── PASSO 4 · "O seu contexto" ──
• Motivo (lista): Vou mudar de casa | Recebi uma herança |
  Quero rentabilizar o investimento | Mudança de vida (trabalho,
  separação, família) | Vou emigrar | Outro
• Prazo (lista): O mais rápido possível | Até 3 meses | 3 a 6 meses |
  Mais de 6 meses | Estou só a explorar a ideia
• Ocupação (lista): Vivo lá | Está vazio | Está arrendado a inquilinos |
  Uso ocasional
      ▸ "Arrendado" muda tudo: reduz compradores e afeta o preço.
• Já está à venda? (lista): Não, ainda não | Sim, com agência em
  exclusivo | Sim, com agência sem exclusivo | Sim, por minha conta
      ▸ "Exclusivo" significa que NÃO pode ser angariado agora.
• Há quanto tempo está no mercado? (select): <1 mês | 1–3 meses |
  3–6 meses | Mais de 6 meses
      ▸ MOSTRAR só se já está à venda

── PASSO 5 · Contacto ──
• Nome completo | Telemóvel | E-mail
• Quer marcar uma avaliação gratuita? (lista): Sim, quero marcar |
  Talvez — primeiro quero saber mais | Não, só queria o diagnóstico
• Checkbox de consentimento (obrigatória):
  "Autorizo a <MARCA> a contactar-me sobre o meu diagnóstico."
  ▸ Se o BLOCO 1 tiver LINK DA POLÍTICA, acrescenta:
    "…e li a política de privacidade." com o link.


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 5 — MOTOR DE DIAGNÓSTICO (3 eixos, não um score)       ║
╚══════════════════════════════════════════════════════════════╝

Cada eixo é independente, de 0 a 100, limitado com Math.max/min.

── EIXO 1 · DOCUMENTAÇÃO (parte de 100) ──
Documentos em falta:
  Caderneta predial       −10
  Certidão permanente     −10
  Licença de utilização   −15
  Certificado energético  −25   ← pesa mais: é BLOQUEANTE por lei
Encargos:
  Hipoteca −5 | Penhora −30 | Usufruto −20 | Não sei −10
Titularidade:
  Herança/partilha −15 | Vários proprietários −10
  Sem acordo −20 | Não sei se há acordo −15

── EIXO 2 · PREÇO vs MERCADO ──
Base pela ORIGEM do valor (não pelo valor em si):
  Avaliação profissional 90 | Anúncios semelhantes 68 |
  "É o que preciso de receber" 32 | "Não faço ideia" 45
Ajustes:
  Tem margem +10 | Nenhuma margem −15 | Valor ainda não definido −8
  No mercado há 3–6 meses −12 | há mais de 6 meses −22

── EIXO 3 · ESTADO E PRONTIDÃO (base 78) ──
  Vazio +15 | Vivo lá +5 | Uso ocasional +5 | Arrendado −30
  Antes de 1980 −15 | 1980–2000 −5 | Depois de 2015 +8 | Não sei −5
  "Só a explorar" −10

── TEMPO ESTIMADO DE VENDA ──
global = doc*0.35 + preco*0.40 + estado*0.25
  ≥80 → "4 a 8 semanas"    · "A sua casa está pronta a ir a mercado."
  ≥65 → "6 a 10 semanas"   · "Está quase — faltam ajustes pontuais."
  ≥50 → "2 a 4 meses"      · "Há pontos a resolver antes de anunciar."
  ≥35 → "4 a 6 meses"      · "Vários travões vão atrasar a venda."
   <35 → "Mais de 6 meses" · "Sem intervenção, a venda vai arrastar-se."
▸ SEMPRE uma janela, nunca um número exato. Um número exato seria falso
  e legalmente imprudente.

── TRAVÕES (dinâmicos, por ordem de gravidade, mostrar no máx. 3) ──
Cada regra que dispara gera um travão com título + explicação honesta:
  • Falta o certificado energético → é obrigatório por lei para anunciar
  • Não há acordo entre proprietários → a escritura precisa de todos
  • Penhora sobre o imóvel → tem de ser levantada antes da escritura
  • Imóvel arrendado → reduz compradores e afeta o preço
  • Preço ancorado na necessidade → "o mercado não paga o que precisamos"
  • Não sabe quanto vale → anunciar acima de mercado queima a casa
  • Demasiado tempo no mercado → anúncio velho = "tem problema"
  • Contrato de exclusividade ativo → só pode mudar no fim do contrato
  • Usufruto → o usufrutuário tem de consentir
  • Faltam ≥3 documentos → reunir tudo leva semanas, comece já
  • Quer vender depressa mas sem ceder no preço → tem de escolher


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 6 — PÁGINA DE RESULTADO                                ║
╚══════════════════════════════════════════════════════════════╝

Ordem das secções (é uma narrativa: veredicto → diagnóstico → o que
está mal → o que fazer → falar connosco):

1. CABEÇALHO (fundo na cor principal):
   "O seu diagnóstico · <primeiro nome>"
   A janela de tempo em tipografia grande (o veredicto).
   A nota curta por baixo. Aviso: "Estimativa indicativa. Não substitui
   uma avaliação presencial."

2. OS TRÊS EIXOS — barras animadas (transition width 1.1s), com a
   percentagem e cor por escalão: ≥70 verde | ≥45 terracota | <45 vermelho.
   Cada eixo tem uma legenda curta a explicar o que mede.

3. CHECKLIST DE DOCUMENTOS — os 4 documentos, cada um com ✓ ou ✕,
   uma linha a explicar onde se pede, e a etiqueta "BLOQUEIA O ANÚNCIO"
   no certificado energético quando está em falta.
   Subtítulo dinâmico: "Faltam-lhe N documentos" ou "Tem tudo."

4. O QUE ESTÁ A TRAVAR A SUA VENDA — os travões (máx. 3), numerados.
   Se não houver nenhum: caixa verde "Não identificámos travões críticos."

5. O QUE FAZER A SEGUIR — 4 passos, ORDENADOS pelo caso concreto:
   certificado energético primeiro se faltar; acordo entre proprietários
   antes de mostrar a casa; avaliação se o eixo do preço for fraco;
   estratégia com inquilino se estiver arrendado; preparar a casa para
   visitas sempre no fim.

6. CTA (fundo na cor principal):
   "Quer saber quanto vale MESMO a sua casa?"
   • WhatsApp (principal) — mensagem PRÉ-PREENCHIDA com o contexto real:
     tempo estimado, tipo, tipologia e localização do imóvel.
   • Ligar agora (tel:)
   • Instagram (link discreto)
   ▸ Se o utilizador escolheu "Sim, quero marcar", o texto do CTA muda
     para reconhecer isso e prometer contacto em 48h.


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 7 — ADAPTAR A OUTROS NICHOS                            ║
╚══════════════════════════════════════════════════════════════╝

Este simulador vive de UMA ideia: em vez de dizer "és um bom lead",
diz "isto é o que te falta e isto é o que te vai custar em tempo".
Para levar a outro nicho, mantém a ARQUITETURA e troca os EIXOS:

• Crédito habitação → eixos: Documentação | Capacidade de
  endividamento | Entrada disponível. Saída: "aprovação estimada em X".
• Dentário/estética → eixos: Urgência clínica | Orçamento |
  Disponibilidade. Saída: "tratamento em X consultas".
• Automóvel → eixos: Retoma | Financiamento | Prazo.
  Saída: "entrega em X semanas".

REGRA: mantém sempre 4 passos de qualificação + 1 de contacto, os três
eixos, a janela de tempo, a checklist e os travões dinâmicos. E mantém
o BLOCO 3 INTACTO — o fluxo técnico não muda com o nicho.


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 8 — CHECKLIST DE QA (antes de publicar)                ║
╚══════════════════════════════════════════════════════════════╝

Testa SEMPRE no telemóvel antes de pôr anúncios a correr:

[ ] O hero cabe todo no ecrã a 390×844 (foto + título + botão).
[ ] O quiz avança e a validação bloqueia campos vazios/inválidos.
[ ] As perguntas condicionais aparecem e desaparecem como devem
    (tipologia com Terreno; acordo com "Só eu"; tempo no mercado).
[ ] O banner de cookies aparece; "Recusar" NÃO carrega o pixel.
[ ] No fim, o redirect para resultado.html acontece (~0,8 s).
[ ] Abrir resultado.html diretamente → reencaminha para index.html
    E NÃO regista PageView (confirma no "Testar eventos").
[ ] Refresh no resultado.html NÃO conta uma segunda conversão.
[ ] No GHL chega o lead COM telemóvel no campo Telefone (+351…),
    nome e email preenchidos. ← se vier vazio, é o Content-Type.
[ ] No Meta › Gestor de Eventos › "Testar eventos": aparece PageView
    e Lead em tempo real (depois de aceitar cookies).
[ ] O evento Lead NÃO traz value nem currency.
[ ] Pixel ID e Webhook URL são os DESTE cliente (não copiados de outro).
[ ] A chave de sessão é única deste projeto.


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 9 — CONFIGURAÇÃO NO META (para o gestor de tráfego)    ║
╚══════════════════════════════════════════════════════════════╝

CRIAR A CONVERSÃO PERSONALIZADA (método principal de medição):
Gestor de Eventos › Conversões personalizadas › Criar
  • Fonte de dados: Pixel DESTE cliente
  • Evento: "Tráfego completo do URL"
  • Regra: URL · contém · resultado     (mais robusto que "é igual a")
  • Categoria: Lead
  • Nome: Lead — <MARCA>

NA CAMPANHA:
  • Objetivo: Leads
  • Conjunto de dados: o Pixel do cliente
  • Evento de conversão: a CONVERSÃO PERSONALIZADA acima,
    NÃO o evento padrão "Lead" vazio
  • Categoria especial de anúncios: marcar "Habitação/Imobiliário"
    (obrigatório em PT para imobiliário, crédito e emprego)

Não é preciso criar campanha nova por teres configurado a conversão
depois. Edita a existente e troca o evento. Isso reinicia a fase de
aprendizagem (normal), mas não perdes histórico.

NOTA SOBRE VOLUME: com o banner de consentimento, só medes quem aceita
cookies. Vais ver MENOS conversões do que num simulador sem banner —
isso não é um bug, é a realidade legal. Para recuperar a medição de
quem recusa, o caminho é a Conversions API (server-side).


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 10 — ENTREGA                                           ║
╚══════════════════════════════════════════════════════════════╝

Devolve DOIS ficheiros completos, prontos para GitHub Pages:
  • index.html     (hero + quiz + banner + pixel + webhook + finalizar())
  • resultado.html (guarda + pixel só PageView + 3 eixos + checklist +
                    travões + próximos passos + CTAs)

Requisitos:
• Código 100% inline (CSS e JS dentro de cada ficheiro).
  Sem "…resto do código aqui…". Código INTEIRO.
• Sem dependências externas além de Google Fonts e do Meta Pixel.
• Substitui TODOS os marcadores (<PIXEL_ID>, <MARCA>, <NOME ORIGEM>,
  <CHAVE_UNICA>, <PREFIXO_PAIS>, WEBHOOK URL, cores, contactos) pelos
  valores do BLOCO 1.
• A CHAVE_UNICA tem de ser específica do projeto (ex: 'diag_novacasa').
  Duas instalações com a mesma chave partilham sessionStorage no mesmo
  domínio — e o GitHub Pages da organização É o mesmo domínio.
• Se o PIXEL ID ou o WEBHOOK vierem vazios/placeholder, o simulador tem
  de continuar a abrir e a funcionar localmente (modo demo, com
  console.log do payload em vez de fetch).

═══════════════════════════════════════════════════════════════
FIM DO PROMPT · v3.0
═══════════════════════════════════════════════════════════════
