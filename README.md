# Trabalo_modelagem_conceitual
Trabalho para o T1 de modelagem conceitual para a disciplina Bando de Dados 1

https://app.brmodeloweb.com/#!/publicview/68c6ac5c0aee1f3e65bbddc4

ZONA DE PRATICAGEM

Deseja-se controlar as viagens dos navios em uma Zona de Praticagem.  
Cada VIAGEM é atendida por pelo menos um PRATICO, admitindo-se a participação de mais de um profissional quando as condições exigirem. A VIAGEM possui exatamente um TERMINAL SAÍDA e um TERMINAL DE CHEGADA, estabelecendo a derrota da faina de praticagem na área portuária. Existe mais de uma viagem entre os diversos pontos de saída e de chegada.
O PRATICO é identificado pelo seu CPF, nome, endereço, telefone. O PRATICO realiza as manobras em navios. das VIAGENS; um mesmo prático pode atuar em muitas viagens, conforme escala e disponibilidade operativa.

TERMINAL_SAI e TERMINAL_CHEGA guardam atributos como código, local, telefone e endereço, compondo o cadastro dos locais de interface com o navio.

O ARMADOR é cadastrado com CNPJ, nome, endereço e telefone, representando a pessoa jurídica responsável pela propriedade ou operação econômica dos navios.
Existe vínculo de propriedade entre ARMADOR e NAVIO: um armador pode possuir muitos navios, enquanto cada navio pertence a um único armador, garantindo responsabilidade clara sobre a embarcação.
A AGENCIA é registrada com CNPJ, nome_agencia, telefone, e-mail e endereço, atuando como representante operacional do navio perante a praticagem e demais entes portuários.
Cada VIAGEM possui data_hora_inicio e data_hora_fim e está sempre associada a um único NAVIO, materializando o evento operacional que demanda serviços de praticagem.
Uma AGENCIA solicita ou gerencia a VIAGEM de um NAVIO, podendo tratar muitas viagens ao longo do tempo, desde a requisição até a coordenação dos serviços envolvidos.
A EMPRESA_PRATICAGEM é identificada por CNPJ, com nome, endereço, telefone e, quando aplicável, e-mail, caracterizando a organização responsável pela prestação do serviço de praticagem.
A EMPRESA_PRATICAGEM possui muitos REBOCADORES, e cada REBOCADOR pertence a uma única empresa, garantindo rastreabilidade de recursos e responsabilidades.
O REBOCADOR possui atributos como nome e potência; quando aplicável, um identificador técnico (como o IMO do rebocador) pode ser utilizado para reforçar unicidade no cadastro.
O REBOCADOR assiste VIAGENS quando necessário; uma viagem pode receber assistência de zero ou mais rebocadores, de acordo com as condições de vento, corrente, calado e porte do navio.
Além disso, o REBOCADOR pode ajudar NAVIOS em manobras específicas, permitindo registrar apoio pontual mesmo fora do contexto de uma viagem formalizada.
A ATALAIA mantém nome, telefone e e-mail, centralizando a coordenação de tráfego, comunicações e despacho no âmbito da zona de praticagem.
A ATALAIA gerencia a operação em pontos e terminais definidos; cada ponto gerenciado está sob responsabilidade de uma única atalaia, preservando unidade de comando.
O PONTO_EMBARQUE possui código, local e nome, servindo como referência operacional para a transferência do prático entre a lancha de praticagem e o navio.
O relacionamento entre NAVIO e VIAGEM é de um-para-muitos: um navio pode realizar diversas viagens ao longo do tempo, mas cada viagem refere-se a um único navio.
Cada VIAGEM relaciona-se a um TERMINAL_SAI e a um TERMINAL_CHEGA coerentes com seu trajeto; o diagrama explicita o sentido (ida/volta) para diferenciar papéis de partida e chegada.
Os contatos (telefone, e-mail) de AGENCIA, EMPRESA_PRATICAGEM e ATALAIA são mantidos para assegurar comunicação contínua durante o planejamento, a execução e o encerramento das operações.
AGENCIA e ARMADOR mantêm vínculos claros com NAVIO e VIAGEM, assegurando representação legal, responsabilidades comerciais e propriedade ou operação econômica devidamente identificadas.
As cardinalidades (1,1) nos vínculos com terminais indicam unicidade do terminal de referência por VIAGEM no contexto de saída e no de chegada, evitando ambiguidades operacionais.
O relacionamento ATUA registra a participação do PRATICO na VIAGEM; quando houver múltiplos práticos na mesma viagem, todos ficam devidamente associados ao evento.
A coexistência de ASSISTE (rebocador–viagem) e AJUDA (rebocador–navio) reflete a realidade operacional, permitindo registrar tanto o apoio no evento quanto a assistência direta ao navio.
Atributos de localização, como local e endereço, em TERMINAL_SAI, TERMINAL_CHEGA e PONTO_EMBARQUE, definem com precisão onde a operação ocorre fisicamente.
Identificadores oficiais — IMO para NAVIO, CNPJ para entidades jurídicas e CPF para PRATICO — são tratados como chaves naturais, garantindo unicidade e integridade nos respectivos cadastros.
O modelo contempla a cadeia operacional completa: a AGENCIA coordena a VIAGEM do NAVIO do ARMADOR, atendida por PRATICO, com apoio de REBOCADOR, sob gestão da ATALAIA, envolvendo TERMINAL_SAI, TERMINAL_CHEGA e PONTO_EMBARQUE, cobrindo do planejamento à execução segura das manobras.

Aqui vão 10 funcionalidades simples, usando apenas os atributos que já existem no seu modelo (sem preço):

Cadastro e busca de NAVIO

Cadastrar e localizar navios por IMO (único) ou por nome_navio; listar também tonelagem_bruta e calado.

Relatório técnico do NAVIO

Gerar um resumo por navio com IMO, nome_navio, tonelagem_bruta, calado para apoio ao planejamento operacional.

Agenda de VIAGENS por período

Filtrar viagens por data_hora_inicio e data_hora_fim e exibir o NAVIO (IMO/nome) associado.

Mapa de VIAGEM por terminais

Para cada viagem, apresentar o TERMINAL_SAI e o TERMINAL_CHEGA com seus codigo, local, telefone, endereco.

Ficha da AGENCIA por VIAGEM

Ao abrir uma viagem, mostrar os contatos da AGENCIA responsável (cnpj, nome_agencia, telefone, email, endereco).

Cartão do PRATICO

Exibir dados do prático (cpf, nome) e listar as VIAGENS em que atuou num intervalo de tempo.

Catálogo de REBOCADOR

Listar rebocadores com nome e potencia e, quando aplicável, associá-los às VIAGENS que assistiram.

Cadastro do ARMADOR com frota

Manter dados do armador (cnpj, nome, endereco, telefone) e listar os NAVIOS que lhe pertencem (via IMO/nome_navio).

Catálogo de PONTO_EMBARQUE

Consultar pontos de embarque por codigo e local, exibindo também o nome para referência rápida em operações.

Validações básicas e deduplicação

Conferir obrigatoriedade e consistência: data_hora_fim > data_hora_inicio; impedir duplicidades por IMO (NAVIO), CPF (PRATICO) e CNPJ (AGENCIA/ARMADOR/EMPRESA_PRATICAGEM).
