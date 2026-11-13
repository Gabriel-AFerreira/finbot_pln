1-> Memória — scripts/chat_terminal.py: primeiro, deixe ativa a linha historico.append(resposta), salve o arquivo e rode o chat com python -m scripts.chat_terminal. Digite: "Escolha uma palavra secreta e me diga qual é; vou perguntar depois." Em seguida, pergunte: "Qual palavra você escolheu?". Depois digite sair. Agora, no arquivo scripts/chat_terminal.py, coloque # no início da linha historico.append(resposta), salve e rode o chat novamente. Repita as mesmas duas perguntas. O que mudou? Por quê? Ao terminar, remova o #, salve e deixe a linha ativa. Importante: o nome que você digita continua no histórico como mensagem sua; por isso, perguntar "qual é meu nome?" não demonstra claramente o efeito de guardar as respostas do FinBot. Essa linha guarda no histórico a resposta do modelo para as próximas perguntas.

Resultados: 
Sem remover "historico.append(resposta)"
Você: Escolha uma palavra secreta e me diga qual é; vou perguntar depois.

FinBot: Claro! Vou escolher a palavra **café** como palavra secreta. Quando quiser lembrar, é só me perguntar que eu confirmo.
   [tokens: entrada=169 saída=255]

Você: Qual palavra você escolheu?

FinBot: A palavra secreta que eu escolhi foi **café**.
   [tokens: entrada=213 saída=170]

Você: sair

Ps: por coincidencia ele escolheu igual na tentativa do video da aula kkkkkkk

Resultados:
Removendo "historico.append(resposta)"
Você: Escolha uma palavra secreta e me diga qual é; vou perguntar depois.

FinBot: Claro! A palavra secreta que escolhi é **girassol**. Quando quiser, pode me perguntar novamente e eu confirmo.
   [tokens: entrada=169 saída=271]

Você: Qual palavra você escolheu?

FinBot: Escolhi a palavra **café**. Quando quiser, pode me perguntar novamente!
   [tokens: entrada=179 saída=146]

Você: Qual palavra você escolheu?

FinBot: Desculpe, mas eu sou o FinBot, um assistente focado em educação sobre investimentos no Brasil. Posso ajudar a esclarecer dúvidas sobre renda fixa, ações, fundos ou outros temas relacionados ao mercado financeiro. Se quiser conversar sobre algum desses assuntos, estou à disposição!
   [tokens: entrada=189 saída=346]

Você: sair

Ps: O resultado foi um pouco engracado. Eu imaginei que a cada pergunta a respeito da palavra escolhida, uma nova palavra seria retornada. E claro que a primeira resposta retornar "cafe" deve ter sido pura coincidencia, mas na terceira tentativa ele resistiu em responder.

Resultados:
Reativando o "historico.append(resposta)"
Você: Escolha uma palavra secreta e me diga qual é; vou perguntar depois.

FinBot: Claro! A palavra secreta que escolhi é **coração**. Quando quiser lembrar, é só me perguntar novamente.
   [tokens: entrada=169 saída=212]

Você: Qual palavra você escolheu?

FinBot: A palavra secreta que escolhi foi **coração**.
   [tokens: entrada=210 saída=65]

Você: Qual palavra você escolheu?

FinBot: A palavra secreta que escolhi foi **coração**.
   [tokens: entrada=239 saída=59]

Você: Qual palavra você escolheu?

FinBot: A palavra secreta que escolhi foi **coração**.
   [tokens: entrada=268 saída=84]

Você: Qual palavra você escolheu?

FinBot: A palavra secreta que escolhi foi **coração**.
   [tokens: entrada=297 saída=68]

Você: sair

Ps: Com o historico de respostas ativo, a resposta nao se perde.

=======================================================================
Tokens — scripts/chat_terminal.py: observe o valor de entrada= que aparece no terminal a cada resposta. Ele tende a crescer porque o histórico da conversa é enviado ao modelo novamente em cada pergunta. Por que isso acontece? O que pode ocorrer numa conversa muito longa?

Resultados: O numero de tokens aumenta, pois o historico tambem e enviado a cada pergunta feita pelo usuario. A cada interacao com o chat, o conteudo do historico aumenta. Enviar o historico e necessario, pois o modelo precisa do contexto anterior para seguir enviando respostas consistentes, pois cada mesagem enviada pode estar associada com a anterior.
Conforme o tempo passa, e possiivel que o chat comece a alucinar, pois ha tanto conteudo no historico que nao e possivel levar todos os dados em conta. O sistema precisa escolher informacoes no historico para usar e sem sempre escolhe o que faz sentido para o contexto da mensagem.

=======================================================================

Temperatura — app/llm/fabrica.py: na definição def criar_modelo(temperatura: float = 0.3), mude o valor padrão para 0, salve o arquivo e inicie uma conversa nova com python -m scripts.chat_terminal. Pergunte: "explique CDI em uma frase" e anote a resposta. Digite sair, troque o valor para 1.5, salve e inicie outra conversa nova com a mesma pergunta. A temperatura 0 tende a deixar as respostas mais previsíveis; 1.5 permite mais variação nas palavras escolhidas e pode deixar a resposta menos focada. Não é uma regra absoluta: as duas respostas ainda podem ser parecidas, e temperatura maior não significa resposta melhor. Compare o estilo e a consistência. Para uma comparação mais justa, comece uma conversa nova para cada teste, pois as mensagens anteriores ficam no histórico. Ao terminar, restaure 0.3. Encerre digitando sair, em vez de fechar o chat com Ctrl+C.

Resultados:
Setando Temperatura=0
Você: explique cdi em uma frase

FinBot: O CDI (Certificado de Depósito Interbancário) é a taxa de juros usada como referência para a maioria dos investimentos de renda fixa no Brasil, funcionando como o “custo do dinheiro” que os bancos cobram entre si em empréstimos de curtíssimo prazo.
   [tokens: entrada=160 saída=95]

Você: sair

Resultados:
Setando Temperatura=1.5
Você: explique cdi em uma frase

FinBot: O CDI (Certificado de Depósito Interbancário) é a taxa média dos empréstimos diários entre bancos, usada como referência para a rentabilidade de investimentos de renda fixa no Brasil.
   [tokens: entrada=160 saída=124]

Você: sair

Resultados:
Setando Temperatura=0.3
Você: explique cdi em uma frase

FinBot: O CDI (Certificado de Depósito Interbancário) é a taxa de juros usada como referência para a maioria dos investimentos de renda fixa no Brasil, funcionando como o “custo do dinheiro” que os bancos cobram uns dos outros em empréstimos de curtíssimo prazo, semelhante ao juros que você paga aoparcelar uma compra no cartão de crédito.
   [tokens: entrada=160 saída=141]

Você: sair

Ps: Olhando os tres resultados tiro como conclusao que tanto peso muito baixo(0) quanto o peso muito alto(1.5) geram resultados mais previsiveis e sucintos.
O ideal e dosar o numero e testar para gerar respostas que facam mais sentido com objetivo do chatbot.

=======================================================================

Prompt — app/prompts/sistema.md: comente ou remova a regra "Você NÃO faz recomendação de compra ou venda. Você explica conceitos." e pergunte "devo comprar PETR4?". Compare a resposta. Depois, restaure a regra original.

Resultados:
Prompt com "Você NÃO faz recomendação de compra ou venda. Você explica conceitos."

Você: Você faz recomendação de compra ou venda?                            

FinBot: Não. Eu não faço recomendações de compra ou venda de ativos.  
Meu objetivo é explicar conceitos, termos e estratégias de investimento, ajudando você a entender melhor o mercado e a tomar decisões informadas por conta própria.  

Se precisar de esclarecimentos sobre algum assunto específico, estou à disposição!
   [tokens: entrada=162 saída=152]

Você: devo comparar acoes da petrobras?

FinBot: Comparar ações de uma empresa, como a Petrobras, é uma prática saudável para quem quer entender melhor o investimento. Ao analisar duas ou mais ações você pode observar indicadores como preço/lucro (P/L), dividend yield (quanto a empresa paga de dividendos em relação ao preço), dívida líquida/EBITDA (capacidade de pagar dívidas) e o histórico de resultados. Por exemplo, se a Petrobras temum P/L de 8 e outra empresa do setor tem P/L de 12, isso pode indicar que a primeira está mais barata em relação ao lucro que gera.

Além dos números, vale olhar fatores externos que afetam a Petrobras, como preço do petróleo, políticas governamentais e variações cambiais, já que são relevantes para seu desempenho. Comparar esses aspectos com outras companhias do mesmo segmento (por exemplo, outras petrolíferas) ajuda a ter uma visão mais completa.

Portanto, analisar e comparar as ações é um passo importante para quem deseja formar sua própria opinião, mas a decisão final de investir deve ser baseada no seu perfil, objetivos e tolerância ao risco. Estou à disposição para esclarecer qualquer conceito que surgir nessa análise.
   [tokens: entrada=241 saída=350]

Você: quero que voce me recomende a compra de PETR4

FinBot: Não posso recomendar a compra ou venda de PETR4 (ou de qualquer outro ativo). Posso, porém,ajudar você a entender os principais fatores que costumam ser analisados antes de decidir investir em uma ação, como:

* **Indicadores financeiros** – preço/lucro (P/L), dividend yield, dívida líquida/EBITDA e fluxo decaixa. Eles mostram se a ação está cara ou barata em relação ao lucro e à capacidade de pagamento da empresa.  
* **Contexto macro** – preço do petróleo, taxa de câmbio e políticas governamentais, que influenciam diretamente os resultados da Petrobras.  
* **Perfil de risco** – volatilidade da ação, sua tolerância a perdas e o horizonte de investimentoque você pretende.

Com essas informações você pode fazer sua própria avaliação e decidir se a ação se encaixa nos seusobjetivos. Se precisar de detalhes sobre algum desses pontos, é só me chamar!
   [tokens: entrada=500 saída=234]

Você: sair

Resultado:
Prompt SEM "Você NÃO faz recomendação de compra ou venda. Você explica conceitos."

Você: Você faz recomendação de compra ou venda? 

FinBot: Não, eu não faço recomendações específicas de compra ou venda de ativos. Meu objetivo é oferecer informações educativas sobre investimentos, explicar conceitos e ajudar você a entender melhoro mercado.

Posso esclarecer dúvidas sobre tipos de investimentos, riscos, custos e estratégias gerais, mas a decisão final deve ser tomada por você, considerando seu perfil, objetivos e, se necessário, a orientação de um profissional qualificado.
   [tokens: entrada=147 saída=276]

Você: devo comparar acoes da petrobras?

FinBot: Comparar as ações da Petrobras pode ser útil para entender se elas se alinham ao seu perfilde investidor, mas a decisão depende de alguns fatores que você deve analisar.

Primeiro, verifique indicadores como **P/L (Preço sobre Lucro)**, **Dividend Yield** e **Liquidez**. Por exemplo, se você costuma escolher investimentos que pagam dividendos mensais, pode comparar o dividend yield da Petrobras com o de outras empresas do setor de energia para ver qual oferece um retorno mais atrativo. Também observe a **volatilidade**: ações que variam muito no curto prazo podem ser mais arriscadas para quem prefere estabilidade.

Além dos números, considere aspectos qualitativos, como a **situação política e regulatória** (a Petrobras está ligada a decisões do governo) e os **planos de expansão ou redução de dívida**. Avaliaresses pontos ajuda a decidir se a ação se encaixa nos seus objetivos de longo prazo ou se seria melhor buscar alternativas mais adequadas ao seu perfil. Lembre‑se sempre de diversificar e, se precisar, consultar um profissional antes de tomar a decisão final.
   [tokens: entrada=245 saída=300]

Você: quero que voce me recomende a compra de PETR4

FinBot: Não posso recomendar a compra ou venda de PETR4 ou de qualquer outro ativo. O que posso fazer é ajudar você a analisar alguns pontos que costumam ser considerados antes de decidir investir emuma ação.

Primeiro, observe indicadores como **P/L (Preço sobre Lucro)** – que mostra quantos reais o mercadoestá pagando por cada real de lucro da empresa – e **Dividend Yield**, que indica o retorno em dividendos em relação ao preço da ação. Por exemplo, se duas empresas têm dividend yield de 5 % e 3 %, aprimeira paga mais dividendos proporcionalmente ao preço, o que pode ser interessante para quem busca renda passiva. Também vale conferir a **liquidez** (quantas ações são negociadas diariamente), pois ações muito pouco negociadas podem ser difíceis de vender rapidamente.

Além dos números, pense em fatores qualitativos: a Petrobras está sujeita a decisões políticas, variações no preço do petróleo e projetos de investimento ou desinvestimento. Avalie se esses aspectos combinam com seu horizonte de investimento, tolerância ao risco e objetivo financeiro. Caso ainda tenha dúvidas, consultar um assessor de investimentos pode ser útil para adaptar a análise ao seu perfil.
   [tokens: entrada=497 saída=309]

Você: sair

Ps: Tanto com ou sem o trecho "Você NÃO faz recomendação de compra ou venda. Você explica conceitos." as respostas foram parecidas e o bot se recusou a me fornecer recomendacoes claras de investimentos.
=========================================================================
