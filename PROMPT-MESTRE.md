═══════════════════════════════════════════════════════════════
PROMPT-MESTRE — SIMULADOR "DIAGNÓSTICO DE VENDA"
Base: Feel Your Home (em produção)
Versão 4.0 · 2 páginas HTML + Meta Pixel + Webhook GoHighLevel
═══════════════════════════════════════════════════════════════

COMO USAR
1. Preenche SÓ o BLOCO 1. Escreve sempre DENTRO dos colchetes [ ].
2. Copia o documento INTEIRO e cola no Claude Code.
3. Recebes index.html e resultado.html prontos para GitHub Pages.

⚠️ NÃO APAGUES os BLOCOS 2 a 9. São a especificação fixa que garante
que o simulador sai igual ao Feel Your Home e que o PIXEL e o WEBHOOK
funcionam mesmo. Só muda o que está no BLOCO 1.

───────────────────────────────────────────────────────────────
INSTRUÇÃO DIRETA À IA
───────────────────────────────────────────────────────────────
"Lê o documento todo antes de escrever uma linha.

Replica a estrutura do BLOCO 4 (4 passos) e do BLOCO 5 (2 eixos)
EXATAMENTE. Não acrescentes perguntas nem eixos — a versão em
produção foi enxugada de propósito: cada campo extra custa conversão.

O BLOCO 3 é crítico. Três regras que não podes contrariar, mesmo que
te pareçam melhoráveis:
  1. Webhook com Content-Type: application/json. NUNCA text/plain.
  2. No resultado.html, a guarda de sessionStorage corre ANTES do
     fbq('track','PageView'). Nunca ao contrário.
  3. O evento Lead vai SEM value e SEM currency.

Entrega os dois ficheiros COMPLETOS. Sem '…resto do código aqui…'.
Código inteiro, pronto a publicar."


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 1 — PREENCHER (o único que muda por cliente)           ║
╚══════════════════════════════════════════════════════════════╝

── MARCA ──
NOME DA MARCA:................. [ ex: Feel Your Home ]
LOGO:.......................... [ URL da imagem | ou SIGLA: ex: FYH ]
   ▸ Se for URL, o logo entra como <img> no hero e no cabeçalho do
     resultado (altura máx. 34px). Se for sigla, entra num quadrado
     na cor principal.
TOM:........................... [ luxo/sofisticado | próximo/amigável | técnico/profissional ]

── CORES ──
   ▸ Deixa vazio = preto/branco minimalista do Feel Your Home.
COR PRINCIPAL:................. [ ex: #000000 ]  → botões, cabeçalhos, logo
COR DESTAQUE:.................. [ ex: #FFFFFF ]  → texto sobre a principal
FUNDO:......................... [ ex: #FFFFFF ]
TEXTO ESCURO:.................. [ ex: #000000 ]
   ▸ FIXAS (não mudar — são semânticas do resultado):
     verde #1a7a4a (eixo bom) · terracota #b85c38 (alerta/travão)

── TÍTULOS (hero) ──
   ▸ Deixa vazio = usa os do Feel Your Home (ver BLOCO 2).
ETIQUETA (topo):............... [ ex: Diagnóstico de Venda Gratuito ]
TÍTULO:........................ [ ex: A sua casa está pronta para entrar no mercado? ]
SUBTÍTULO (itálico):........... [ ex: Ou vai ficar meses à espera de um comprador? ]
TEXTO DE APOIO:................ [ ex: Duas casas iguais, na mesma rua: uma vende em 6 semanas, a outra fica 8 meses. A diferença está na preparação. Descubra onde está a sua. ]
BOTÃO:......................... [ ex: Começar o diagnóstico ]
FOTO DO HERO:.................. [ URL da foto | ou SEM FOTO para fundo sólido ]

── CONTACTOS / CTAs ──
WHATSAPP (só dígitos):......... [ ex: 351915000141 ]
TELEFONE (Ligar agora):........ [ ex: +351915000141 ]
INSTAGRAM (URL):............... [ ex: https://instagram.com/feelyour.home ]

── INTEGRAÇÕES (SEMPRE DIFERENTES POR CLIENTE) ──
META PIXEL ID:................. [ ex: 2546786472431675 ]
WEBHOOK URL (GoHighLevel):..... [ ex: https://services.leadconnectorhq.com/hooks/.../webhook-trigger/... ]
NOME DA ORIGEM:................ [ ex: Feel Your Home: Diagnóstico de Venda ]
CHAVE ÚNICA:................... [ ex: diag_fyh_venda — diferente em cada projeto ]
PREFIXO DO PAÍS:............... [ ex: 351 ]
DOMÍNIO FINAL:................. [ ex: https://4improvementsportugal-ops.github.io/simulador-fyh/ ]
POLÍTICA DE PRIVACIDADE:....... [ URL do cliente | ou SEM LINK ]


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 2 — ESPECIFICAÇÃO GERAL                                ║
╚══════════════════════════════════════════════════════════════╝

DUAS páginas independentes, CSS e JS 100% inline, sem dependências
externas além de Google Fonts e do Meta Pixel:

  index.html     → Hero + quiz de 4 passos + banner de consentimento
  resultado.html → Diagnóstico com URL própria

OBJETIVO: gerar leads para o GoHighLevel e registar a conversão no
Meta por CONVERSÃO PERSONALIZADA POR URL (regra: o URL contém
"resultado").

O QUE O UTILIZADOR RECEBE (não é um score /10):
  1. Uma JANELA DE TEMPO até vender ("6 a 10 semanas")
  2. DOIS EIXOS em barras (Documentação · Estado e Prontidão)
  3. CHECKLIST dos 4 documentos, com ✓/✕
  4. Até 3 TRAVÕES, tirados das respostas
  5. PRÓXIMOS PASSOS ordenados pelo caso dele

── BLOCO DE CONFIGURAÇÃO (topo do <head>, nas duas páginas) ──
Escreve as integrações num bloco comentado e visível, assim:

  <!-- ========================================================
    INTEGRACOES: SUBSTITUIR ANTES DE PUBLICAR
    PIXEL_ID      → ID do Meta Pixel deste cliente
    WEBHOOK_URL   → URL do webhook GoHighLevel deste cliente
    CHAVE_UNICA   → chave única deste projeto
    NOME_ORIGEM   → nome da origem no webhook
    PREFIXO_PAIS  → 351
  ======================================================== -->
  <script>
    var PIXEL_ID            = '<PIXEL_ID>';
    var WEBHOOK_URL         = '<WEBHOOK_URL>';
    var NOME_ORIGEM         = '<NOME ORIGEM>';
    var PREFIXO_PAIS        = '<PREFIXO_PAIS>';
    var CHAVE_UNICA         = '<CHAVE_UNICA>';
    var CHAVE_CONSENTIMENTO = CHAVE_UNICA + '_cookies';
    var PIXEL_ATIVO   = PIXEL_ID.indexOf('AQUI') === -1;
    var WEBHOOK_ATIVO = WEBHOOK_URL.indexOf('AQUI') === -1;
    /* carregarPixel() e temConsentimento() — ver BLOCO 3 */
  </script>

▸ Este bloco é o que permite trocar de cliente sem procurar valores
  espalhados pelo ficheiro. Mantém-no no topo e com estes nomes.

── TIPOGRAFIA ──
Google Fonts: Fraunces (títulos, com itálico) + Inter (corpo).
  Fraunces: ital,opsz,wght@0,9..144,300;0,9..144,400;0,9..144,600;
            1,9..144,300;1,9..144,400
  Inter: wght@300;400;500;600

── HERO ──
• Etiqueta pequena no topo (maiúsculas, espaçada).
• Título grande em Fraunces. A 2ª frase em ITÁLICO, tom mais suave —
  é a agitação do problema.
• Texto de apoio a seguir, em Inter, cor suave.
• Botão na cor principal.
• 3 selos: "3 minutos · Sem compromisso · Resultado imediato".
• Copy do Feel Your Home (usar se o BLOCO 1 vier vazio):
    etiqueta:  "Diagnóstico de Venda Gratuito"
    título:    "A sua casa está pronta para entrar no mercado?"
    itálico:   "Ou vai ficar meses à espera de um comprador?"
    apoio:     "Duas casas iguais, na mesma rua: uma vende em 6
                semanas, a outra fica 8 meses. A diferença está na
                preparação: documentação completa e um preço ajustado
                ao mercado. Descubra onde está a sua."
    botão:     "Começar o diagnóstico"

── UX OBRIGATÓRIA ──
• Todas as perguntas OBRIGATÓRIAS, com erro visual (contorno
  #e53935 + fundo #fff5f5 + mensagem) antes de avançar.
• scrollIntoView ao primeiro campo inválido.
• E-mail por regex. Telemóvel ≥ 9 dígitos. Nome ≥ 3 caracteres com
  espaço.
• Barra de progresso + "Passo X de 4".
• "Voltar" e "Continuar". No último passo: "Ver o meu diagnóstico".
• Botão desativado enquanto envia + flag aEnviar (evita duplo lead).
• Mobile-first. Acessibilidade: <label>, role="group" +
  aria-labelledby, aria-hidden nos ícones, contraste AA.
• Zero bibliotecas JS.

── BANNER DE CONSENTIMENTO (obrigatório) ──
O pixel NÃO carrega sozinho — a diretiva ePrivacy exige consentimento
prévio para cookies de publicidade.
• Banner fixo no fundo, "Aceitar" e "Recusar".
• O snippet do pixel vive dentro de carregarPixel(), só chamada
  depois do "Aceitar". Escolha guardada em localStorage e respeitada
  nas duas páginas.
• Quem recusa faz o diagnóstico na mesma e o lead CONTINUA a ir para
  o GoHighLevel — só não é medido no Meta.


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 3 — FLUXO TÉCNICO ★ A PARTE MAIS IMPORTANTE ★          ║
╚══════════════════════════════════════════════════════════════╝

Seis erros que fazem estes simuladores perder leads e conversões.
Os três primeiros são clássicos. Os três últimos são SILENCIOSOS —
o sistema parece funcionar e não funciona.

── ERRO 1 · o redirect cancela o evento do pixel ──
fbq('track','Lead') é um pedido ASSÍNCRONO. Se a página navegar logo
a seguir, o browser CANCELA-o → o lead chega ao GHL mas nunca ao Meta.
SOLUÇÃO: dispara o evento e só redireciona ~800 ms depois, com
fallback aos 2500 ms.

── ERRO 2 · o telemóvel não chega ao campo certo do GHL ──
O GHL só mapeia sozinho com as chaves phone, email, name,
first_name, last_name. E rejeita telemóveis com espaços — tem de ir
em E.164 (+351912345678).
SOLUÇÃO: normalizarTel() + chaves padrão ALÉM dos rótulos legíveis.

── ERRO 3 · lead contado a dobrar ──
Disparar Lead no index E no resultado conta duas vezes.
SOLUÇÃO: Lead UMA vez, no index, com eventID único. No resultado só
PageView — é esse PageView que alimenta a conversão por URL.

── ERRO 4 · Content-Type text/plain parte o mapping do GHL ★ ──
Muitos tutoriais mandam usar text/plain "para evitar o preflight
CORS". É falso e é grave: com text/plain o GHL NÃO faz parse do corpo,
o mapping fica VAZIO e os leads chegam sem telefone nem email. Pior, o
webhook devolve 200 OK à mesma — passa semanas sem ninguém dar por
nada. O endpoint LeadConnector responde ao preflight com
Allow-Origin: *, portanto CORS nunca foi problema.
SOLUÇÃO: application/json. Sempre.

── ERRO 5 · conversões fantasma no resultado.html ★ ──
Com o pixel no topo do <head>, o PageView dispara antes de o script
verificar o sessionStorage. Qualquer bot, preview de link ou pessoa
que abra /resultado à mão gera uma conversão falsa.
SOLUÇÃO: a guarda do sessionStorage corre ANTES de carregar o pixel.
Sem dados → window.location.replace('index.html') e o pixel nunca
existe. Mais uma flag CHAVE_UNICA+'_pv' para o PageView não contar
duas vezes num refresh.

── ERRO 6 · o score enviado como se fosse dinheiro ★ ──
value:<score> + currency:'EUR' faz o Meta tratar o score como RECEITA
e polui o ROAS da conta com euros que não existem.
SOLUÇÃO: o evento Lead vai SEM value e SEM currency.

───────────────────────────────────────────────────────────────
carregamento do pixel (nas duas páginas)
───────────────────────────────────────────────────────────────
  function carregarPixel() {
    if (!PIXEL_ATIVO || window.fbq) return;
    /* snippet oficial do Meta */
    fbq('init', PIXEL_ID);
    fbq('track', 'PageView');
  }
  function temConsentimento() {
    try { return localStorage.getItem(CHAVE_CONSENTIMENTO) === 'aceite'; }
    catch(e) { return false; }
  }
  if (temConsentimento()) carregarPixel();

───────────────────────────────────────────────────────────────
index.html — finalizar() — ORDEM E TEMPOS EXATOS
───────────────────────────────────────────────────────────────
function normalizarTel(v){
  var d = (v||'').replace(/\D/g,'');
  if(!d) return '';
  if(d.indexOf('00') === 0) d = d.slice(2);      // 00351… → 351…
  if(d.length === 9) d = PREFIXO_PAIS + d;       // nº local
  return '+' + d;                                 // E.164
}

function finalizar(){
  if(aEnviar) return;                             // trava duplo clique
  aEnviar = true;
  btn.disabled = true;
  btn.textContent = 'A preparar o seu diagnóstico…';

  var D       = diagnosticar();                   // BLOCO 5
  var tel     = normalizarTel(A.tel);
  var partes  = (A.nome||'').trim().split(/\s+/);
  var first   = partes[0]||'', last = partes.slice(1).join(' ')||'';
  var eventId = 'lead-'+Date.now()+'-'+Math.random().toString(36).slice(2,8);

  // 1) guardar PRIMEIRO — o resultado.html lê daqui
  try { sessionStorage.setItem(CHAVE_UNICA,
        JSON.stringify({A:A, D:D, eventId:eventId, ts:Date.now()})); } catch(e){}

  // 2) Advanced Matching antes do evento (o pixel faz o hash sozinho)
  if(PIXEL_ATIVO && typeof fbq === 'function'){
    fbq('init', PIXEL_ID, { em:A.email, ph:tel, fn:first, ln:last });

    // 3) Lead UMA vez. SEM value. SEM currency. (ERRO 6)
    fbq('track','Lead', {
      content_name: NOME_ORIGEM, content_category: '<MARCA>'
    }, { eventID: eventId });
  }

  // 4) webhook (keepalive sobrevive ao redirect)
  enviarWebhook(tel, first, last, D, eventId);

  // 5) SÓ AGORA o redirect. Sem este atraso o window.location
  //    cancela o pedido do pixel. (ERRO 1)
  var jaFoi = false;
  var ir = function(){ if(jaFoi) return; jaFoi = true;
                       window.location.href = 'resultado.html'; };
  setTimeout(ir, 800);
  setTimeout(ir, 2500);                           // fallback
}

───────────────────────────────────────────────────────────────
enviarWebhook() — payload
───────────────────────────────────────────────────────────────
  fetch(WEBHOOK_URL, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },   // ← NUNCA text/plain
    body: JSON.stringify(payload),
    keepalive: true
  }).catch(function(e){ console.error('Falha no envio do lead:', e); });

payload:
• Chaves PADRÃO que o GHL mapeia sozinho:
    name, first_name, last_name, phone (E.164), email
• Metadados:
    timestamp, origem, pagina_url, event_id, consentimento_rgpd
• Respostas com RÓTULOS LEGÍVEIS (nunca códigos internos):
    imovel_tipo, imovel_tipologia, imovel_localizacao,
    documentos_que_tem, documentos_em_falta, encargos,
    motivo_venda, prazo_venda, ocupacao, ja_no_mercado,
    tempo_no_mercado
• Diagnóstico:
    score_documentacao, score_estado, score_global,
    tempo_estimado, travoes
• raw: cópia bruta das respostas (depuração)

▸ Se WEBHOOK_ATIVO for false, NÃO faças fetch: console.log do payload.
  Assim o ficheiro abre localmente sem erros.

───────────────────────────────────────────────────────────────
resultado.html — a ordem no <head> é sagrada
───────────────────────────────────────────────────────────────
1º  lê sessionStorage e o consentimento
2º  sem dados → window.location.replace('index.html'), e NÃO carrega
    pixel nenhum (ERRO 5)
3º  com dados E consentimento → pixel + PageView, com flag
    CHAVE_UNICA+'_pv' para não contar duas vezes num refresh
4º  NUNCA disparar 'Lead' aqui


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 4 — AS PERGUNTAS (4 passos · usar tal e qual)          ║
╚══════════════════════════════════════════════════════════════╝

Não acrescentes perguntas. Esta lista já foi enxugada em produção:
cada campo extra custa conversão.

── PASSO 1 · "Comecemos pelo imóvel" ──
• Que tipo de imóvel pretende vender?  (grelha 2 col)
    Apartamento | Moradia | Terreno | Outro
• Tipologia  (grelha 4 col)
    T0/T1 | T2 | T3 | T4+
    ▸ ESCONDER se tipo = Terreno
• Localização (concelho e freguesia)  — texto livre

── PASSO 2 · "O que já tem em mãos" ──
• Que documentos já tem? (selecione todos)  — MULTI-SELEÇÃO
    Caderneta predial | Certidão permanente do registo |
    Licença de utilização | Certificado energético |
    Nenhum / não sei     ← opção EXCLUSIVA (limpa as outras)
    ▸ É o gancho do simulador: sem certificado energético não é
      legal anunciar, e a maioria dos vendedores não sabe.
• O imóvel tem algum encargo?  (lista)
    Não, está livre | Hipoteca / crédito | Penhora / processo |
    Usufruto | Não sei

── PASSO 3 · "Ajude-nos a perceber a sua situação" ──
• Por que motivo pretende vender?  (dropdown)
    Vou mudar de casa | Recebi uma herança |
    Quero rentabilizar o investimento | Mudança de vida |
    Vou emigrar | Outro
• Com que urgência quer vender?  (lista)
    O mais rápido possível | Até 3 meses | 3 a 6 meses |
    Mais de 6 meses | Estou só a explorar a ideia
• Estado atual do imóvel  (lista)
    Vivo lá | Está vazio | Está arrendado | Uso ocasional
    ▸ Arrendado muda tudo: o inquilino tem direito de preferência
      e as visitas têm de ser combinadas.
• Já está à venda?  (lista)
    Não, ainda não | Sim, em exclusivo | Sim, sem exclusivo |
    Sim, por conta própria
    ▸ Em exclusivo = não pode ser angariado agora.
• Há quanto tempo está no mercado?  (dropdown)
    Menos de 1 mês | 1 a 3 meses | 3 a 6 meses | Mais de 6 meses
    ▸ MOSTRAR só se já está à venda

── PASSO 4 · "Receber o seu diagnóstico" ──
• Nome completo | Telemóvel | E-mail
• Checkbox de consentimento (obrigatória):
    "Autorizo a <MARCA> a contactar-me sobre o meu diagnóstico."
    ▸ Se o BLOCO 1 trouxer POLÍTICA DE PRIVACIDADE, acrescenta
      "…e li a política de privacidade." com o link.


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 5 — MOTOR DE DIAGNÓSTICO (2 eixos)                     ║
╚══════════════════════════════════════════════════════════════╝

Dois eixos de 0 a 100, limitados com Math.max/min.
NÃO há eixo de preço — as perguntas de preço foram removidas.

── EIXO 1 · DOCUMENTAÇÃO (peso 60%) ── parte de 100
  falta Caderneta predial              −10
  falta Certidão permanente do registo −10
  falta Licença de utilização          −15
  falta Certificado energético         −25   ← bloqueante por lei
  respondeu "Nenhum / não sei"          −5   (penalização extra)
  encargo Hipoteca / crédito            −5
  encargo Penhora / processo           −30
  encargo Usufruto                     −20
  encargo "Não sei"                    −10

── EIXO 2 · ESTADO E PRONTIDÃO (peso 40%) ── base 78
  Está vazio                           +15
  Vivo lá                               +5
  Uso ocasional                         +5
  Está arrendado                       −30
  No mercado há 3 a 6 meses            −12
  No mercado há mais de 6 meses        −22
  "Estou só a explorar a ideia"        −10

── JANELA DE TEMPO ──
global = documentacao * 0.60 + estado * 0.40
  ≥ 80 → "4 a 8 semanas"    · "A sua casa está pronta a ir a mercado."
  ≥ 65 → "6 a 10 semanas"   · "Está quase: faltam ajustes pontuais."
  ≥ 50 → "2 a 4 meses"      · "Há pontos a resolver antes de anunciar."
  ≥ 35 → "4 a 6 meses"      · "Vários travões vão atrasar a venda."
  < 35 → "Mais de 6 meses"  · "Sem intervenção, a venda vai arrastar-se."
▸ SEMPRE uma janela, nunca um número exato — seria falso e
  legalmente imprudente.

── TRAVÕES (por gravidade, mostrar no máx. 3) ──
  falta certificado energético
    → "Falta o certificado energético: é obrigatório por lei para
       anunciar o imóvel"
  encargo Penhora
    → "Penhora sobre o imóvel: tem de ser levantada antes da escritura"
  Está arrendado
    → "Imóvel arrendado: reduz o número de compradores e afeta o preço"
  encargo Usufruto
    → "Usufruto ativo: o usufrutuário tem de consentir na venda"
  no mercado há mais de 6 meses
    → "Demasiado tempo no mercado: anúncio antigo transmite perceção
       de problema"
  já à venda em exclusivo
    → "Contrato de exclusividade ativo: só pode mudar de agência no
       fim do contrato"
  faltam ≥ 3 documentos
    → "Faltam N documentos: reunir tudo pode levar semanas, comece já"


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 6 — PÁGINA DE RESULTADO                                ║
╚══════════════════════════════════════════════════════════════╝

Narrativa: veredicto → diagnóstico → o que está mal → o que fazer →
falar connosco.

1. CABEÇALHO (cor principal): logo + "O seu diagnóstico · <1º nome>".
   A JANELA DE TEMPO em Fraunces grande. A nota curta por baixo.
   Aviso: "Estimativa indicativa. Não substitui uma avaliação
   presencial."

2. "Os dois eixos do seu diagnóstico" — barras animadas
   (transition width ~1.1s), percentagem e cor por escalão:
   ≥70 verde #1a7a4a · ≥45 terracota #b85c38 · <45 vermelho.

3. "Checklist de documentos" — os 4 documentos com ✓ ou ✕, uma linha
   a dizer onde se pede cada um, e a etiqueta "BLOQUEIA O ANÚNCIO"
   no certificado energético quando falta.
   Subtítulo dinâmico: "Faltam-lhe N documentos" / "Tem tudo."

4. "O que está a travar a sua venda" — até 3 travões, numerados.
   Sem travões → caixa verde de confirmação.

5. "O que fazer a seguir" — passos ORDENADOS pelo caso concreto:
   • Obter o certificado energético
     "É obrigatório por lei para publicar o anúncio. Contacte um
      perito qualificado."                    ← se faltar
   • Reunir os restantes documentos
     "Peça a caderneta predial nas Finanças, a certidão permanente
      no Registo Predial e a licença de utilização na Câmara."
                                              ← se faltarem outros
   • Fazer uma avaliação profissional
     "O preço é o fator que mais determina o tempo de venda."
   • Definir estratégia com o inquilino
     "O inquilino tem direito de preferência e as visitas têm de ser
      combinadas."                            ← se arrendado
   • Preparar a casa para as visitas
     "Home staging: arrumação, pintura e fotografia profissional."
                                              ← sempre, no fim

6. CTA (cor principal):
   • WhatsApp (principal) — mensagem PRÉ-PREENCHIDA com o contexto
     real: janela de tempo, tipo, tipologia e localização.
   • Ligar agora (tel:)
   • Instagram (link discreto)


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 7 — ADAPTAR A OUTROS NICHOS                            ║
╚══════════════════════════════════════════════════════════════╝

A ideia central: em vez de dizer "és um bom lead", diz "isto é o que
te falta e isto é o que te vai custar em tempo". Para outro nicho,
mantém a ARQUITETURA e troca os dois eixos:

• Crédito habitação → Documentação | Capacidade de endividamento.
  Saída: "aprovação estimada em X semanas".
• Dentário/estética → Urgência clínica | Disponibilidade.
  Saída: "tratamento em X consultas".
• Automóvel → Documentação/retoma | Prazo.
  Saída: "entrega em X semanas".

REGRA: mantém 3 passos de qualificação + 1 de contacto, os 2 eixos,
a janela de tempo, a checklist e os travões. E mantém o BLOCO 3
INTACTO — o fluxo técnico não muda com o nicho.


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 8 — CHECKLIST DE QA (antes de publicar)                ║
╚══════════════════════════════════════════════════════════════╝

Testa SEMPRE no telemóvel antes de pôr anúncios a correr:

[ ] O hero cabe no ecrã a 390×844 (logo + título + botão).
[ ] O quiz avança e a validação bloqueia campos vazios/inválidos.
[ ] Condicionais: tipologia esconde com Terreno; tempo no mercado
    só aparece se já está à venda.
[ ] "Nenhum / não sei" nos documentos limpa as outras opções.
[ ] O banner de cookies aparece; "Recusar" NÃO carrega o pixel.
[ ] No fim, o redirect acontece (~0,8 s).
[ ] Abrir resultado.html diretamente → reencaminha para index.html
    E NÃO regista PageView (confirma no "Testar eventos").
[ ] Refresh no resultado NÃO conta segunda conversão.
[ ] No GHL o lead chega com telemóvel no campo Telefone (+351…),
    nome e email.   ← se vier vazio, é o Content-Type.
[ ] No Meta › Gestor de Eventos › "Testar eventos" aparece PageView
    e Lead em tempo real (depois de aceitar cookies).
[ ] O evento Lead NÃO traz value nem currency.
[ ] PIXEL_ID e WEBHOOK_URL são os DESTE cliente.
[ ] CHAVE_UNICA é diferente da dos outros simuladores.
    ▸ O GitHub Pages da organização é o MESMO domínio: duas
      instalações com a mesma chave partilham sessionStorage.


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 9 — CONFIGURAÇÃO NO META (gestor de tráfego)           ║
╚══════════════════════════════════════════════════════════════╝

CRIAR A CONVERSÃO PERSONALIZADA (medição principal):
Gestor de Eventos › Conversões personalizadas › Criar
  • Fonte de dados: Pixel DESTE cliente
  • Evento: "Tráfego completo do URL"
  • Regra: URL · contém · resultado   (mais robusto que "é igual a")
  • Categoria: Lead
  • Nome: Lead — <MARCA>

NA CAMPANHA:
  • Objetivo: Leads
  • Evento de conversão: a CONVERSÃO PERSONALIZADA acima,
    NÃO o evento padrão "Lead" vazio
  • Categoria especial de anúncios: "Habitação/Imobiliário"
    (obrigatório em PT)

Editar a campanha existente chega — não é preciso criar nova. Muda o
evento de conversão; isso reinicia a aprendizagem (normal) mas não
perde histórico.

NOTA SOBRE VOLUME: com banner de consentimento só medes quem aceita
cookies. Vais ver MENOS conversões do que num simulador sem banner —
não é bug, é a realidade legal. Para recuperar a medição de quem
recusa, o caminho é a Conversions API (server-side).


╔══════════════════════════════════════════════════════════════╗
║ BLOCO 10 — ENTREGA                                           ║
╚══════════════════════════════════════════════════════════════╝

DOIS ficheiros completos, prontos para GitHub Pages:
  • index.html     (hero + quiz 4 passos + banner + pixel + webhook
                    + finalizar())
  • resultado.html (guarda + pixel só PageView + 2 eixos + checklist
                    + travões + próximos passos + CTAs)

Requisitos:
• CSS e JS 100% inline. Sem "…resto do código aqui…". Código INTEIRO.
• Sem dependências externas além de Google Fonts e do Meta Pixel.
• Bloco de configuração no topo do <head>, com os nomes do BLOCO 2.
• Substituir TODOS os marcadores pelos valores do BLOCO 1.
• Se PIXEL_ID ou WEBHOOK_URL vierem com "AQUI", o simulador continua
  a abrir e a funcionar localmente (modo demo, console.log do payload).

═══════════════════════════════════════════════════════════════
FIM · v4.0 · base Feel Your Home
═══════════════════════════════════════════════════════════════
