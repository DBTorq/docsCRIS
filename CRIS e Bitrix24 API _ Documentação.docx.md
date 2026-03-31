

**Documentação das APIs do CRIS e do Bitrix24**  
Atualizado em 19/01/2026 18:07

# **Introdução**

Este documento visa detalhar todos os endpoints que o sistema CRIS e o Bitrix possuem com seus respectivos dados de entrada e de saída.

# **Nomenclaturas importantes**

Abaixo, estão entidades e nomenclaturas importantes para a regra de negócio e lógica dos sistemas.

| Jornada de Compra do Cliente | Temos o diferencial de organizarmos nossas regras de negócio e lógicas do CRIS por meio do service design thinking \- colocando a experiência do usuário no centro. As etapas da jornada são Atração, Conversão, Entrega e Retenção. |
| :---- | :---- |
| **Atração** | Etapa 1 do relacionamento do prospect com a marca (desde o primeiro comentário na rede social, por exemplo, até o agendamento da avaliação) |
| **Conversão** | Etapa 2 do relacionamento do lead com a marca (da presença na avaliação até a compra do tratamento) |
| **Entrega** | Etapa 3 do relacionamento do cliente com a marca (da primeira sessão até a conclusão do tratamento) |
| **Retenção** | Etapa 4 do relacionamento do cliente com a marca (atenção para a satisfação do cliente e processos comerciais para vender novamente para esse cliente \- aumento de LTV e conseguir indicações dele) |
| **Apoio** | Categoria de endpoints secundários que servem para retornar dados requisitados nos endpoints principais |
| **Contato** | Entidade que representa uma pessoa com CPF, nome, telefone e email único.  No CRIS, o contato se chama *Prospect* enquanto não possui orçamento aprovado (venda concluída). Após concluir sua venda, o contato se chama *Cliente*. Em CRM, existem sistemas que seguem a lógica: contato único e negócio único \= independente de quantas compras e orçamentos o contato gerar, um único “card” é gerado no CRM. contato único e negócios múltiplos \= cada interesse de compra ou orçamento de venda lançado gera seu respectivo “card” no CRM. Esse é o caso do Bitrix. Atente-se para a lógica do seu CRM porque isso vai impactar na forma em que você manipula os dados obtidos via API. |
| **Negócio** | Entidade que representa a possível compra do contato. Pode ser um cadastro que o contato fez em um site ou uma mensagem que ele enviou após receber uma indicação, por exemplo. A negociação pode ser criada de forma manual pela equipe ou de forma automática quando há integração como (formulários de sites/landing pages, Meta Ads Forms etc.). |
| **Avaliação** | Entidade que representa a “sessão/agendamento” exclusivamente dedicado para tentativa de venda consultiva. Pode ser online ou presencial. Dentro do CRIS, é um campo importante e que impacta no lançamento dos orçamentos e do módulo Planejamento Comercial da Unidade (KPIs automatizados, estudo diário e funil). |
| **Orçamento** | Entidade que representa o interesse de compra do contato. Contém dados como número de sessões, itens de produtos, valores, descontos e forma de pagamento. O status podem ser: Pendente \= criado a partir do momento em que a negociação com o contato se inicia. Aprovado \= quando o cliente faz o pagamento e se torna uma venda concluída. Cancelado \= cliente compra e cancela por algum motivo.  Suspenso \= contato não chega a fechar comprar e desiste, entende-se como orçamento “arquivado”. Inativo \= orçamento excluído por motivo de erro de lançamento. |
| **Agendamento** | Entidade que representa a sessão do tratamento e que é reservado um horário na agenda de execução de procedimentos da clínica |

# **CRIS | Lista dos Endpoints de Saída**

Os endpoints que exportam dados do CRIS atualmente são:

[Atração | Novo contato criado no CRIS](#atração-|-novo-contato-criado-no-cris)

[Atração | Lista prospects e clientes](#atração-|-lista-prospects-e-clientes)

[Conversão | Nova avaliação agendada para o contato](#conversão-|-nova-avaliação-agendada-para-o-contato)

[Conversão | Novo orçamento lançado para o contato](#conversão-|-novo-orçamento-lançado-para-o-contato)

[Conversão | Lista orçamentos com venda detalhada](#conversão-|-lista-orçamentos-com-venda-detalhada)

[Conversão | Orçamento atualizado para o contato](#conversão-|-orçamento-atualizado-para-o-contato)

[Conversão e Entrega | Lista agendamentos](#conversão-e-entrega-|-lista-agendamentos)

[Retenção | Lista saldo de tratamento](#retenção-|-lista-saldo-de-tratamento)

[Apoio | statusAgendamento](#apoio-|-statusagendamento)

[Apoio | avaliacaoPossuiVendaOrcamento](#apoio-|-avaliacaopossuivendaorcamento)

[Apoio | listaClinicas](#apoio-|-listaclinicas)

[Apoio | lista\_status\_venda](#apoio-|-lista_status_venda)

[Apoio | listaServico](#apoio-|-listaservico)

[Apoio | listaCriadoPorVenda](#apoio-|-listacriadoporvenda)

[Apoio | listaVendedor](#apoio-|-listavendedor)

[Apoio | listaPlanoDeConta](#apoio-|-listaplanodeconta)

[Apoio | listaTipoOperacao](#apoio-|-listatipooperacao)

[Apoio | listaCanal](#apoio-|-listacanal)

[Apoio | listaCampanha](#apoio-|-listacampanha)

# **CRIS | Lista dos Endpoints de Entrada**

Os endpoints que importam dados para o CRIS atualmente são:

[Atração | Cadastra contato novo](#atração-|-cadastra-contato-novo)

[Atração | Atualiza contato](#atração-|-atualiza-contato)

[Conversão e Entrega | Atualiza status do agendamento do contato](#conversão-e-entrega-|-atualiza-status-do-agendamento-do-contato)

[Retenção | Envio de Pesquisa de Satisfação quando orçamento é gerado](#retenção-|-envio-de-pesquisa-de-satisfação-quando-orçamento-é-gerado)

[Apoio | loginApi](#apoio-|-loginapi)

[Apoio | criaCampanha](#apoio-|-criacampanha)

## **Atração | Novo contato criado no CRIS** {#atração-|-novo-contato-criado-no-cris}

| Status | Melhoria futura, indisponível no momento |
| :---- | :---- |
| **Ação** | Quando um novo contato é criado diretamente no CRIS, um webhook o exporta para o CRM de modo que não haja divergências na base. |
| **Gatilho** | Novo contato criado na tela Prospect. |
| **Campos retornados** | Contato: ID Contato: Criado em Contato: Nome Contato: Telefone Contato: Email Contato: Canal \- mais recente Contato: Campanha/Ação \- mais recente Contato: Unidade |
| **Observação** | \- |
| **Método HTTP** | POST |
| **Saída de dados** | Body |
| **Formato** | JSON |
| **Autenticação** | Nenhuma |
| **Link do webhook** | Informar ao time CR |

## **Atração | Lista prospects e clientes**  {#atração-|-lista-prospects-e-clientes}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Retorna um agrupamento das telas “Cliente” \[[https://cris.clinicaderesultado.com.br/admin\_home.php?item=pessoa\_v\_cliente\&sid=deda62cb9b07](https://cris.clinicaderesultado.com.br/admin_home.php?item=pessoa_v_cliente&sid=deda62cb9b07)\] e “Prospecção de clientes” \[[https://cris.clinicaderesultado.com.br/admin\_home.php?item=pessoa\_v\_prospeccao\&sid=5ff4887ed253](https://cris.clinicaderesultado.com.br/admin_home.php?item=pessoa_v_prospeccao&sid=5ff4887ed253)\]  |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Contato: IDContato: Criado Por Contato: Criado Em Contato: Nome Contato: Data de nascimento Contato: Profissão Contato: E-mail Contato: Telefone Principal Contato: Telefone Secundário Contato: Interesses Contato: Importado em Contato: Status Contato: Indicação Contato: Indicado por Contato: Observações Contato: Inativo Contato: Canal \- mais recente Contato: Campanha/Ação \- mais recente Contato: Unidade |
| **Observação** | O endpoint respeita o nível de acesso que seu usuário possui, mostrando entidades apenas da respectiva unidade |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/lista\_cliente](https://cris.clinicaderesultado.com.br/rest/v1/lista_cliente)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20   recomenda-se usar um número baixo para não sobrecarregar a API \* clinica \= 1   preenche automático para usuários de clínica. obrigatório para admin\_master nome \= teste   string, busca correspondência mais próxima criado\_em\_de \= 2025-07-29    data de criação em sql criado\_em\_ate \= 2025-07-29   data de criação em sql data\_nascimento\_de \= 1990-01-01    data de nascimento em sql data\_nascimento\_ate \= 1991-01-01   data de nascimento em sql email \= lucas3@teste.com  indicado\_por \= 15   id do cliente indicador indicado \= 0   0 não foi indicado, 1 foi indicado inativo \= 1    0 ativo, 1 inativo telefone \= 17981212118     string do telefone principal, usar formato DDDXXXXXXXXX telefone\_secundario \=       string do telefone secundário, usar formato DDDXXXXXXXXX |
| **Body** | nenhum |

## **Conversão | Nova avaliação agendada para o contato** {#conversão-|-nova-avaliação-agendada-para-o-contato}

| Status | Melhoria futura, indisponível no momento |
| :---- | :---- |
| **Ação** | Quando uma nova avaliação é agendada diretamente no CRIS, um webhook o exporta para o CRM. |
| **Gatilho** | Novo agendamento criado na tela Agenda. |
| **Campos retornados** | Contato: ID Contato: Criado em Contato: Criado por Contato: Nome Contato: Telefone Contato: Email Contato: Canal \- mais recente Contato: Campanha/Ação \- mais recente Contato: Unidade Agendamento: ID Agendamento: Tipo Agendamento \= Avaliação Agendamento: Data e hora |
| **Observação** | Se o CRM trabalha com múltiplos negócios, é necessário criar uma automação no CRM que analisa a Data/hora, Canal e Campanha/Ação correspondentes àquela avaliação. |
| **Método HTTP** | POST |
| **Saída de dados** | Body |
| **Formato** | JSON |
| **Autenticação** | Nenhuma |
| **Link do webhook** | Informar ao time CR |

## **Conversão | Novo orçamento lançado para o contato** {#conversão-|-novo-orçamento-lançado-para-o-contato}

| Status | Melhoria futura, indisponível no momento |
| :---- | :---- |
| **Ação** | Quando um novo orçamento é lançado diretamente no CRIS, um webhook o exporta para o CRM. |
| **Gatilho** | Novo orçamento criado na tela Venda/Orçamento. |
| **Campos retornados** | Orçamento: ID Orçamento: Data da venda Orçamento: Cliente ID Orçamento: Cliente Nome Orçamento: Cliente Telefone Orçamento: Avaliação Realizada Orçamento: Origem da Venda \- Canal Orçamento: Origem da Venda \- Campanha/Ação Orçamento: Produto \- Categoria Orçamento: Procedimentos \- Categoria Orçamento: Valor total Orçamento: Unidade |
| **Observação** | Se o CRM trabalha com multiplos negócios, é necessário criar uma automação no CRM que analisa a Avaliação Realizada, Canal e Campanha/Ação correspondentes àquela venda. |
| **Método HTTP** | POST |
| **Saída de dados** | Body |
| **Formato** | JSON |
| **Autenticação** | Nenhuma |
| **Link do webhook** | Informar ao time CR |

## **Conversão | Lista orçamentos com venda detalhada** {#conversão-|-lista-orçamentos-com-venda-detalhada}

| Status | Disponível |
| :---- | :---- |
| **Ação** | O mesmo relatório “Ficha financeira” \[link: [https://cris.clinicaderesultado.com.br/admin\_home.php?item=venda\_v\_fatura\&modulare=5\&sid=ab87f4807741](https://cris.clinicaderesultado.com.br/admin_home.php?item=venda_v_fatura&modulare=5&sid=ab87f4807741)\] é extraído via API e usando os mesmos campos de filtro. |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Orçamento: Código Orçamento: Criado Por Orçamento: Criado Em Orçamento: Data Orçamento: Status Orçamento: Plano de Conta Orçamento: Vendedor Orçamento: Cliente Orçamento: Avaliação Realizada Orçamento: Tipo de Operação sobre produtos Orçamento: Conta Bancária Orçamento: Observações Contratuais Orçamento: Observações da Venda Orçamento: Produtos Orçamento: Procedimentos Orçamento: Tipo de Orçamento Orçamento: Valor Orçamento: Valor Original da venda Orçamento: Telefone Orçamento: Cliente Orçamento: Contrato Orçamento: Campanha/Ação	Canal Orçamento: Cortesia Orçamento: Empresa Orçamento: Venda Avulsa Orçamento: Tipo pagamento Orçamento: Unidade |
| **Observação** | O endpoint respeita o nível de acesso que seu usuário possui, mostrando entidades apenas da respectiva unidade |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/lista\_venda\_orcamento](https://cris.clinicaderesultado.com.br/rest/v1/lista_venda_orcamento)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20   recomenda-se usar um número baixo para não sobrecarregar a API \* clinica \= 1   preenche automático para usuários de clínica. obrigatório para admin\_master data\_de \= 2025-01-07    data em sql data\_ate \= 2025-01-07   data em sql status \= 1       id do status, consulte endpoint **lista\_status\_venda** cliente \= 555    id do cliente, consulte endpoint **lista\_cliente** observacoes\_contratuais \= teste   string, busca correspondência mais próxima  observacoes\_venda \= teste         string, busca correspondência mais próxima inativo \= 0      1 retorna vendas inativas, 0  retorna vendas ativas, vazio retorna todas id\_servico \= 7   id do serviço, consulte endpoint **listaServico** avaliacao\_de \= 2025-05-01        data de avaliação em sql avaliacao\_de \= 2025-06-23        data de avaliação em sql criado\_em\_de \= 2025-01-07        data de criação em sql criado\_em\_ate \= 2025-01-07       data de criação em sql data\_pagamento\_de \= 2025-06-23   data de pagamento em sql data\_pagamento\_ate \= 2025-06-23  data de pagamento em sql modificado\_em\_d \= 2025-06-23     data de modificação em sql modificado\_em\_ate \= 2025-06-23   data de modificação em sql criado\_por \= 1     id do usuário que criou o orçamento, consulte endpoint **listaCriadoPorVenda** modificado\_por \= 1 id do usuário que modificou por último, consulte endpoint **listaCriadoPorVenda**   vendedor  \= 8                id do vendedor, consulte endpoint **listaVendedor** plano\_de\_conta \= 9           id do plano de conta, consulte endpoint **listaPlanoDeConta** tipo\_operacao\_produto \= 2    id do tipo de operação, consulte endpoint **listaTipoOperacao** |
| **Body** | nenhum |

## **Conversão | Orçamento atualizado para o contato** {#conversão-|-orçamento-atualizado-para-o-contato}

| Status | Melhoria futura, indisponível no momento |
| :---- | :---- |
| **Ação** | Quando um orçamento é atualizado diretamente no CRIS, um webhook o exporta para o CRM. |
| **Gatilho** | Orçamento atualizado na tela Ficha Financeira. |
| **Campos** | Orçamento: ID Orçamento: Status \= Aprovado / Cancelado / Suspenso |
| **Observação** | Se o CRM trabalha com multiplos negócios, é necessário criar uma automação no CRM que analisa o ID correspondente àquela venda. |
| **Método HTTP** | POST |
| **Saída de dados** | Body |
| **Formato** | JSON |
| **Autenticação** | Nenhuma |
| **Link do webhook** | Informar ao time CR |

## **Conversão e Entrega | Lista agendamentos** {#conversão-e-entrega-|-lista-agendamentos}

| Status | Disponível |
| :---- | :---- |
| **Ação** | O mesmo relatório “Agendamentos” \[link: https://cris.clinicaderesultado.com.br/admin\_home.php?item=page\_rel\_agendamento\&modulare=7\&sid=4c7c2aa7e6bf\] é extraído via API e usando os mesmos campos de filtro. |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Agendamento: ID Agendamento: Criado em Agendamento: Data Agendamento Agendamento: Cliente ID Agendamento: Cliente \- Nome Agendamento: Cliente \- Telefone Agendamento: Tipo Agendamento: Serviço Agendamento: Profissional Agendamento: Sala Agendamento: Status |
| **Observação** | Para ver apenas as avaliações, use o filtro Tipo Agendamento \= Avaliação |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/relAgendamentos](https://cris.clinicaderesultado.com.br/rest/v1/relAgendamentos)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20   recomenda-se usar um número baixo para não sobrecarregar a API \* clinica \= 1   preenche automático para usuários de clínica. obrigatório para admin\_master data\_agendamento\_de \= 2025-01-01    data em sql data\_agendamento\_ate \= 2025-06-18   data em sql tipo\_agendamento \= 2  id do tipo de agendamento, consulte endpoint **tipoAgendamento** status \= \[1,2,3,4,5\]  array com ids dos status desejados, consulte endpoint **statusAgendamento** avaliacao\_possui \= 0  id do **avaliacaoPossuiVendaOrcamento** e tipo de agendamento deve ser o 2 |
| **Body** | nenhum |

## **Retenção | Lista saldo de tratamento** {#retenção-|-lista-saldo-de-tratamento}

| Status | Melhoria futura, indisponível no momento |
| :---- | :---- |
| **Ação** | O mesmo relatório “Relatório de Saldo de Tratamentos” \[link: [https://cris.clinicaderesultado.com.br/admin\_home.php?item=page\_rel\_saldo\_tratamento\&modulare=7\&sid=1c447cc40fae](https://cris.clinicaderesultado.com.br/admin_home.php?item=page_rel_saldo_tratamento&modulare=7&sid=1c447cc40fae)\] é extraído via API e usando os mesmos campos de filtro. |
| **Gatilho** | Por requisição de API. |
| **Campos** | Filtros Orçamento: Unidade \= OligoFlora Indaiatuba \[string fixo\] Orçamento: Data da Venda Orçamento: Cliente Orçamento: Tem Saldo Orçamento: Categoria Campos retornados Orçamento: Cliente Orçamento: Telefone Orçamento: Data Orçamento: Categoria Orçamento: Serviço Orçamento: Quantidade Contratada Orçamento: Quantidade Utilizada Orçamento: Quantidade Agendada Orçamento: Quantidade Cancelada Orçamento: Quantidade Transferida Orçamento: Saldo Orçamento: Unidade |
| **Observação** | O endpoint respeita o nível de acesso que seu usuário possui, mostrando entidades apenas da respectiva unidade |
| **Método HTTP** | GET via Postman |

## **Apoio | statusAgendamento** {#apoio-|-statusagendamento}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista as opções de Status de Agendamento com respectivos IDs |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Agendamento: IDs do Status  |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/statusAgendamento](https://cris.clinicaderesultado.com.br/rest/v1/statusAgendamento)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** | nenhum |
| **Body** | nenhum |

## **Apoio | avaliacaoPossuiVendaOrcamento** {#apoio-|-avaliacaopossuivendaorcamento}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista as opções do campo PossuiVendaOrcamento (0 ou 1\) para ser usado em filtros de outros endpoints |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Agendamento: Filtro \- PossuiVendaOrcamento |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/avaliacaoPossuiVendaOrcamento](https://cris.clinicaderesultado.com.br/rest/v1/avaliacaoPossuiVendaOrcamento)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** | nenhum |
| **Body** | nenhum |

## **Apoio | listaClinicas** {#apoio-|-listaclinicas}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista todas as clínicas cadastradas no CRIS com respectivos IDs para ser usado em filtros e parâmetros de outros endpoints. Usuário admin\_master vê a lista completa, enquanto usuário licenciado vê apenas o ID da sua própria clínica. |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Clínica: IDClínica: Nome |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/listaClinicas](https://cris.clinicaderesultado.com.br/rest/v1/listaClinicas)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20   recomenda-se usar um número baixo para não sobrecarregar a API |
| **Body** | nenhum |

## **Apoio | lista\_status\_venda** {#apoio-|-lista_status_venda}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista as opções do status do Orçamento com seus respectivos IDs para ser usado em filtros de outros endpoints |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Orçamento: ID do Status |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/lista\_status\_venda](https://cris.clinicaderesultado.com.br/rest/v1/lista_status_venda)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** | nenhum |
| **Body** | nenhum |

## **Apoio | listaServico** {#apoio-|-listaservico}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista os serviços cadastrados no CRIS para ser usado em filtros e parâmetros de outros endpoints |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Serviço: IDServiço: Nome |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/listaServico](https://cris.clinicaderesultado.com.br/rest/v1/listaServico)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20   recomenda-se usar um número baixo para não sobrecarregar a API \* clinica \= 1   preenche automático para usuários de clínica. obrigatório para admin\_master nome \= teste         string, busca correspondência mais próxima |
| **Body** | nenhum |

## **Apoio | listaCriadoPorVenda** {#apoio-|-listacriadoporvenda}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista os profissionais cadastrados no CRIS para ser usado em filtros e parâmetros de outros endpoints |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Profissional: IDProfissional: Nome |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/listaCriadoPorVenda](https://cris.clinicaderesultado.com.br/rest/v1/listaCriadoPorVenda)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20   recomenda-se usar um número baixo para não sobrecarregar a API \* clinica \= 1   preenche automático para usuários de clínica. obrigatório para admin\_master |
| **Body** | nenhum |

## **Apoio | listaVendedor** {#apoio-|-listavendedor}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista os profissionais cadastrados no CRIS e que podem efetuar venda para ser usado em filtros e parâmetros de outros endpoints |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Profissional: IDProfissional: Nome |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/listaVendedor](https://cris.clinicaderesultado.com.br/rest/v1/listaVendedor)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20   recomenda-se usar um número baixo para não sobrecarregar a API \* clinica \= 1   preenche automático para usuários de clínica. obrigatório para admin\_master |
| **Body** | nenhum |

## **Apoio | listaPlanoDeConta** {#apoio-|-listaplanodeconta}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista os planos de conta cadastrados no CRIS para serem usados em filtros e parâmetros de outros endpoints |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Plano de Conta: IDPlano de Conta: Nome |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/listaPlanoDeConta](https://cris.clinicaderesultado.com.br/rest/v1/listaPlanoDeConta)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20   recomenda-se usar um número baixo para não sobrecarregar a API \* clinica \= 1   preenche automático para usuários de clínica. obrigatório para admin\_master |
| **Body** | nenhum |

## **Apoio | listaTipoOperacao** {#apoio-|-listatipooperacao}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista os tipos de operação cadastrados no CRIS para serem usados em filtros e parâmetros de outros endpoints |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Tipo de Operação: IDTipo de Operação: Nome |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/listaTipoOperacao](https://cris.clinicaderesultado.com.br/rest/v1/listaTipoOperacao)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20   recomenda-se usar um número baixo para não sobrecarregar a API \* clinica \= 1   preenche automático para usuários de clínica. obrigatório para admin\_master |
| **Body** | nenhum |

## **Apoio | listaCanal** {#apoio-|-listacanal}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista os canais cadastrados no CRIS para serem usados em filtros e parâmetros de outros endpoints |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Canal: IDCanal: Nome |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/listaCanal](https://cris.clinicaderesultado.com.br/rest/v1/listaCanal) |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20   recomenda-se usar um número baixo para não sobrecarregar a API nome \= teste        string, busca correspondência mais próxima |
| **Body** | nenhum |

## **Apoio | listaCampanha** {#apoio-|-listacampanha}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista as campanhas cadastradas no CRIS para serem usadas em filtros e parâmetros de outros endpoints |
| **Gatilho** | Por requisição de API. |
| **Campos retornados** | Campanha: IDCampanha: Nome |
| **Observação** | nenhum |
| **Método HTTP** | GET |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/listaCampanha](https://cris.clinicaderesultado.com.br/rest/v1/listaCampanha) |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** \* obrigatórios observações | \* pagina\_atual \= 1   \* por\_pagina \= 20 recomenda-se usar um número baixo para não sobrecarregar a API \* clinica \= 1     preenche automático para usuários de clínica. obrigatório para admin\_master nome \= teste      string, busca correspondência mais próxima |
| **Body** | nenhum |

## **Atração | Cadastra contato novo** {#atração-|-cadastra-contato-novo}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Quando um novo contato é criado diretamente no CRM, um webhook o importa para o CRIS de modo que não haja divergências na base. |
| **Gatilho** | Por requisição via API. |
| **Campos necessários** | Contato: ID Contato: Criado em Contato: Nome Contato: Telefone Contato: Email Contato: Canal do CRM Contato: Campanha/Ação do CRM Contato: Data de nascimento Contato: Observação Contato: Unidade |
| **Observação** | Antes de cadastrar, é necessário buscar se o contato já existe na base da Unidade usando o **endpoint Lista Prospects e Clientes**. *se não existe na base*, então deve-se usar o endpoint **Cadastra contato novo** para criar novo Prospect na base da Unidade. *se já existe na base,* então o endpoint correto a ser usado é o **Atualiza contato** a fim de não criar novo contato duplicando dados e gerando conflitos. |
| **Método HTTP** | POST |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/cadastraCliente](https://cris.clinicaderesultado.com.br/rest/v1/cadastraCliente)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** | nenhum |
| **Body** JSON \* obrigatórios observações | \* clinica           diferente dos endpoints GET, aqui “clinica” é SEMPRE obrigatório passar \* nome              string \* telefone          string, seguir sempre o formato (DDD) XXXXX-XXXX email               string \* data\_nascimento   data em sql observacao          string \* canal             id do canal, consulte endpoint **listaCanal** \* campanha          id da campanha, consulte endpoints **listaCampanha** ou **criaCampanha**  Exemplo —------------------------------ {   "nome": "Teste api",   "telefone": "(16) 99264-0197",   "email": "lucas2@teste.com",   "data\_nascimento": "1990-01-01",   "observacao": "Observações aqui",   "clinica": "1",   "canal": "1",   "campanha": "400" } |

## **Atração | Atualiza contato** {#atração-|-atualiza-contato}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Após consultar o **endpoint Lista Prospects e Clientes** e encontrar um contato na base da unidade, esse endpoint deve ser acionado para atualizar campos e cadastrar um novo canal/campanha para o contato com base em seu ID. |
| **Gatilho** | Por requisição via API. |
| **Campos** | Campos que são informados (apenas leitura): Contato: Telefone Contato: Email Contato: ID Contato: Unidade Campos que são atualizados (obrigatórios): Negócio: Criado em Negócio: Canal do CRM Negócio: Campanha/Ação do CRM Campos que são atualizados (opcionais): Contato: Nome Contato: Data de nascimento Contato: Observação |
| **Observação** | Os campos de origem do Negócio são registrados no contato dentro do CRIS como novo canal/campanha. |
| **Método HTTP** | POST |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/atualizaCadastroCliente](https://cris.clinicaderesultado.com.br/rest/v1/atualizaCadastroCliente)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** | nenhum |
| **Body** JSON \* obrigatórios observações | \* clinica           diferente dos endpoints GET, aqui “clinica” é SEMPRE obrigatório passar \* nome              string \* data\_nascimento   data em sql observacao          string \* canal             id do canal, consulte endpoint **listaCanal** \* campanha          id da campanha, consulte endpoints **listaCampanha** ou **criaCampanha** \* id                id do cliente, consulte endpoint **lista\_cliente** Exemplo —------------------------------ {   "nome": "Teste api",   "data\_nascimento": "1996-01-01",   "observacao": "Observações aqui at",   "clinica": "1",   "canal": "1",   "campanha": "214",   "id":"5252" }  |

## **Conversão e Entrega | Atualiza status do agendamento do contato** {#conversão-e-entrega-|-atualiza-status-do-agendamento-do-contato}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Com base no ID da Avaliação, o Status é alterado. |
| **Gatilho** | Por requisição via API. |
| **Campos** | Agendamento: ID Agendamento: Status \= Agendado / Confirmado / Presente / Executado / Desmarcado/ Faltou / Cancelado / Bloqueio |
| **Observação** | As mesmas regras de agendamento que existem na Agenda “manual” do CRIS devem ser respeitadas no agendamento via API. Se existirem regras de automação dentro CRM como exemplos:\- “se Status de Avaliação é alterado para Desmarcado, então o negócio deve ser movido para a fase Repique”, então essas regras de automação devem ser criadas dentro do próprio CRM. \- “se Status de Agendamento é alterado para Executado, então o negócio deve ser movido para a fase Procedimento feito e enviada mensagem de satisfação”, então essas regras de automação devem ser criadas dentro do próprio CRM. |
| **Método HTTP** | POST |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/mudaStatusAgendamento](https://cris.clinicaderesultado.com.br/rest/v1/mudaStatusAgendamento)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** | nenhum |
| **Body** JSON \* obrigatórios observações | \* agendamento   id do agendamento, consulte endpoint **relAgendamentos** \* status        id do novo status, consulte endpoint **statusAgendamento** Exemplo —------------------------------ {     "agendamento": 3581,      "status": 2 } |

## **Retenção | Envio de Pesquisa de Satisfação quando orçamento é gerado** {#retenção-|-envio-de-pesquisa-de-satisfação-quando-orçamento-é-gerado}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Quando um orçamento é aprovado diretamente no CRIS, um webhook é enviado com o link de pesquisa de satisfação. |
| **Gatilho** | Orçamento atualizado para Status \= Aprovado na tela Ficha Financeira. |
| **Campos** | Contato: ID Contato: Arquivo \- Pesquisa de Satisfação \[link\] |
| **Observação** | O webhook apenas informa o link. O envio da pesquisa em si deve ser feito por outro canal (como WhatsApp ou e-mail por exemplo). |
| **Método HTTP** | POST |
| **Saída de dados** | Body |
| **Formato** | JSON |
| **Autenticação** | Nenhuma |
| **Link do webhook** | Informar ao time CR |

## **Apoio | loginApi** {#apoio-|-loginapi}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Com base no login e senha do usuário, gera o token que será usado em todos os endpoints como camada de segurança |
| **Gatilho** | Por requisição via API. |
| **Campos** | Usuário: username de login Usuário: senha |
| **Observação** | Automaticamente, o sistema identifica se o usuário é admin\_master ou licenciado\_unidade restringindo o nível de acesso para todos os dados ou apenas da clínica específica \- respectivamente. |
| **Método HTTP** | POST |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/loginApi](https://cris.clinicaderesultado.com.br/rest/v1/loginApi)  |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** | nenhum |
| **Body** JSON \* obrigatórios observações | \* login      username do usuário usada para fazer login \* password   senha do usuário usada para fazer login Exemplo —------------------------------ {     "login": "admin",     "password": "S3nh4\#2025" } |

## **Apoio | criaCampanha** {#apoio-|-criacampanha}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Registra nova campanha no CRIS para a respectiva unidade e retorna o ID para ser usado em outros endpoints como parâmetro de dado ou filtro |
| **Gatilho** | Por requisição via API. |
| **Campos** | Campanha: ID Campanha: Nome Campanha: Clínica |
| **Observação** | \- |
| **Método HTTP** | POST |
| **URL** | [https://cris.clinicaderesultado.com.br/rest/v1/criaCampanha](https://cris.clinicaderesultado.com.br/rest/v1/criaCampanha) |
| **Headers** | Content-Type \= application/json Authorization \= {token gerado pelo endpoint **login**} |
| **Query Params** | nenhum |
| **Body** JSON \* obrigatórios observações | \* nome          string, nome da campanha \* clinica       diferente dos endpoints GET, aqui “clinica” é SEMPRE obrigatório passar Exemplo —------------------------------ {   "nome": "Teste api LUCAS",   "clinica": "1" } |

# **Sobre o Bitrix24 CRM**

O Bitrix é um software de mercado e amplamente conhecido. Ele possui funcionalidades nativas e também abertura para customizações, integrações e automações.

Em nosso caso, customizamos o CRM para atender às necessidades dos clientes CR Sistemas que usam o ERP CRIS. Isto é, criamos uma pipeline, parametrizando-a e a integrando com o CRIS.

Portanto, nossa companhia do Bitrix é compartilhada entre os clientes da CR Sistemas e zelamos muito pela organização dos dados.

É importante você saber disso porque, embora o Bitrix tenha uma documentação de API bem rica com diversos endpoints, nós iremos orientar abaixo quais são as que recomendamos e como elas conversam com as customizações que fizemos.

Qualquer automação e integração que você desejar fazer que fuja do escopo abaixo e que possua endpoint nativo do Bitrix, solicitamos encarecidamente que alinhe com o time CR Sistemas a fim de evitar transtornos, retrabalhos e atrasos de projetos desnecessariamente.

## **CRM | Lista de Endpoints Recomendados** 

[Token API](#token-api)

[Cria contato e vincula a um negócio na pipeline Unidade](#cria-contato-e-vincula-a-um-negócio-na-pipeline-unidade)

[Lista contatos](#lista-contatos)

[Obtém contato](#obtém-contato)

[Edita contato](#edita-contato)

[Lista negócios](#lista-negócios)

[Obtém negócio](#obtém-negócio)

[Edita negócio / Muda o negócio de fase / Altera ‘nº da tentativa de contato’](#edita-negócio-/-muda-o-negócio-de-fase-/-altera-‘nº-da-tentativa-de-contato’)

[Principais campos usados](#principais-campos-usados)

## **Token API** {#token-api}

Por razões de segurança, a criação de tokens para a API é feita apenas pelo time CR Sistemas. Para isso, basta entrar em contato conosco 🙂

## **Cria contato e vincula a um negócio na pipeline Unidade** {#cria-contato-e-vincula-a-um-negócio-na-pipeline-unidade}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Usado para criar um novo contato e vincular um novo negócio a ele imediatamente na pipeline Unidade e Fase ‘Nova oportunidade’. |
| **Gatilho** | Por requisição via API. |
| **Campos** | Consulte abaixo a lista dos campos principais |
| **Observação** | Esse endpoint foi desenvolvido pela CR Sistemas e verifica se o contato já existe antes de criar um novo a fim de evitar duplicidades.  |
| **Método HTTP** | GET |
| **Endpoint URL** | [https://auto.grupoboto.com/webhook/560db699-9177-4307-abea-825c4c62ead4](https://auto.grupoboto.com/webhook/560db699-9177-4307-abea-825c4c62ead4)  |
| **Headers** | nenhum |
| **Query Params** \* obrigatório observações | \* Primeiro Nome string \* Sobrenome string \* Data hora de criação string, deve seguir o padrão DD/MM/AAAA hh:mm:ss \* Campaign ID string \* UTM Source string “fixa”, deve ser ‘WhatsApp’, ‘Facebook’ ou ‘Instagram’ \* UTM Medium string \* UTM Campaign string \* UTM Content string \* Telefone string no padrão \+55DDDnumero \* Email string \* Unidade string fixa, deve seguir o padrão definido na lista dos campos principais |
| **Body** | nenhum |

## **Lista contatos** {#lista-contatos}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista os contatos para os filtros e campos selecionados na requisição. Retorna apenas contatos em que a unidade tem permissão para visualizar. |
| **Gatilho** | Por requisição via API. |
| **Campos** | Consulte abaixo a lista dos campos principais |
| **Observação** | \- |
| **Método HTTP** | GET |
| **Endpoint** | crm.contact.list |
| **Headers** | nenhum |
| **Query Params** | Filtros e seleção se desejado |
| **Body** | nenhum |
| **Documentação nativa** | [https://apidocs.bitrix24.com/api-reference/crm/contacts/crm-contact-list.html](https://apidocs.bitrix24.com/api-reference/crm/contacts/crm-contact-list.html)  |

## **Obtém contato** {#obtém-contato}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Retorna todos os campos que o contato possui \- nativos e personalizados. |
| **Gatilho** | Por requisição via API. |
| **Campos** | Consulte abaixo a lista dos campos principais |
| **Observação** | \- |
| **Método HTTP** | GET |
| **Endpoint** | crm.contact.get |
| **Headers** | nenhum |
| **Query Params** \* obrigatório | \* ID \= {id\_do\_contato}  |
| **Body** | nenhum |
| **Documentação nativa** | [https://apidocs.bitrix24.com/api-reference/crm/contacts/crm-contact-get.html](https://apidocs.bitrix24.com/api-reference/crm/contacts/crm-contact-get.html)  |

## **Edita contato** {#edita-contato}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Edita os campos do contato que forem passados como parâmetro sem alterar os demais que não foram citados. |
| **Gatilho** | Por requisição via API. |
| **Campos** | Consulte abaixo a lista dos campos principais |
| **Observação** | Raramente usado |
| **Método HTTP** | GET |
| **Endpoint** | crm.contact.update |
| **Headers** | nenhum |
| **Query Params** \* obrigatório | \* ID \= {id\_do\_contato}  \* FIELDS\[{id\_do\_campo}\] |
| **Body** | nenhum |
| **Documentação nativa** | [https://apidocs.bitrix24.com/api-reference/crm/contacts/crm-contact-update.html](https://apidocs.bitrix24.com/api-reference/crm/contacts/crm-contact-update.html)  |

## **Lista negócios** {#lista-negócios}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Lista os negócios para os filtros e campos selecionados na requisição. Retorna apenas negócios em que a unidade tem permissão para visualizar. |
| **Gatilho** | Por requisição via API. |
| **Campos** | Consulte abaixo a lista dos campos principais |
| **Observação** | \-  |
| **Método HTTP** | GET |
| **Endpoint** | crm.deal.list |
| **Headers** | nenhum |
| **Query Params** | Filtros e seleção se desejado FIELDS\[UF\_CRM\_1621027933376\] \= SP São José do Rio Preto exemplo. consultar lista de campos principais |
| **Body** | nenhum |
| **Documentação nativa** | [https://apidocs.bitrix24.com/api-reference/crm/deals/crm-deal-list.html](https://apidocs.bitrix24.com/api-reference/crm/deals/crm-deal-list.html)  |

## **Obtém negócio** {#obtém-negócio}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Retorna todos os campos que o negócio possui \- nativos e personalizados. |
| **Gatilho** | Por requisição via API. |
| **Campos** | Consulte abaixo a lista dos campos principais |
| **Observação** | \- |
| **Método HTTP** | GET |
| **Endpoint** | crm.deal.get |
| **Headers** | nenhum |
| **Query Params** \* obrigatório | \* ID \= {id\_do\_contato}  |
| **Body** | nenhum |
| **Documentação nativa** | [https://apidocs.bitrix24.com/api-reference/crm/deals/crm-deal-get.html](https://apidocs.bitrix24.com/api-reference/crm/deals/crm-deal-get.html)  |

## **Edita negócio / Muda o negócio de fase / Altera ‘nº da tentativa de contato’** {#edita-negócio-/-muda-o-negócio-de-fase-/-altera-‘nº-da-tentativa-de-contato’}

| Status | Disponível |
| :---- | :---- |
| **Ação** | Edita os campos do negócio que forem passados como parâmetro sem alterar os demais que não foram citados. |
| **Gatilho** | Por requisição via API. |
| **Campos** | Consulte abaixo a lista dos campos principais |
| **Observação** | \-  |
| **Método HTTP** | GET |
| **Endpoint** | crm.deal.update |
| **Headers** | nenhum |
| **Query Params** \* obrigatório | \* ID \= {id\_do\_contato}  \* FIELDS\[{id\_do\_campo}\] FIELDS\[UF\_CRM\_1669405845\] \= {nome da fase em texto} exemplo: ‘FIELDS\[UF\_CRM\_1669405845\] \= Tentativa de contato’, aciona automação que muda o negócio para a fase ‘Tentativa de contato’ FIELDS\[UF\_CRM\_1636587029\] \= {id da tentativa} exemplo: ‘FIELDS\[UF\_CRM\_1636587029\] \= 1243’ altera o campo Número da tentativa para ‘3ª tentativa’ |
| **Body** | nenhum |
| **Documentação nativa** | [https://apidocs.bitrix24.com/api-reference/crm/deals/crm-deal-update.html](https://apidocs.bitrix24.com/api-reference/crm/deals/crm-deal-update.html)  |

## **Principais campos usados** {#principais-campos-usados}

| Entidade | Nome no Bitrix | ID no Bitrix | Observação |
| :---- | :---- | :---- | :---- |
| Contato | Primeiro Nome | NAME |  |
| Contato | Segundo Nome | SECOND\_NAME |  |
| Contato | Sobrenome | LAST\_NAME |  |
| Contato | Contact ID | ID |  |
| Contato | Telefone (nativo) | PHONE | Retorna todos os telefones preenchidos para o contato |
| Contato | Telefone (todos) | UF\_CRM\_1673035980 | Usamos esse campo personalizado em vez de PHONE (nativo) para atualizar telefone via automação |
| Contato | Emaill (nativo) | EMAIL | Retorna todos os emails preenchidos para o contato |
| Contato | Email (string) | UF\_CRM\_1676052930 | Usamos esse campo em vez de EMAIL (nativo) para atualizar e-mail via automação |
| Contato | Data de nascimento | BIRTHDATE |  |
| Contato | Observação | COMMENTS |  |
| Negócio | Nome | TITLE | Costumamos preencher com “{ID\_deal} | Nome completo do contato” |
| Negócio | Fase (nativo) | STAGE\_ID | Orientamos usar esse campo apenas para listar os negócios que estão em cada fase. Por se tratar de um campo tipo lista, cada entrada tem um ID diferente conforme abaixo: *Nome da fase | ID* Nova oportunidade \= NEW Repique \= PREPARATION Tentativa de contato \= PREPAYMENT\_INVOICE Em contato \= EXECUTING Buscar / cadastrar no ERP \= FINAL\_INVOICE Agendado \= 1 Confirmado \= 2 Em negociação \= 3 Perdas \= LOSE Venda Cancelada \= 4 Venda realizada \= WON |
| Negócio | Fase (personalizado) | UF\_CRM\_1669405845 | Usamos esse campo junto ao endpoint crm.deal.update para mudar o negócio de fase via automação. Base preenchê-lo com o nome por extenso da respectiva fase. Exemplo “Perdas”. |
| Negócio | Contato vinculado | CONTACT\_ID | Contact ID |
| Negócio | Fonte | SOURCE\_ID | Campo nativo que é editado via automação com base na origem do lead \- que pode ser cadastrada manualmente ou via integração com a Meta, por exemplo. Por se tratar de um campo tipo lista, cada entrada tem um ID diferente conforme abaixo: *Nome da fonte | ID* Facebook \= CALLBACK Instagram \= CALL Formulário do site \= WEBFORM WhatsApp \= 5 TikTok \= 48 E-mail \= 37 TV \= 6 Revista \= 7 Agendamento on-line \= BOOKING Rádio \= 40 Jornal \= 8 Outdoor \= 9 Panfletos / Folder \= 10 Voucher \= 11 Vitrine / Passou na frente \= 14 Indicação \= 15 Venda interna \= 34 Ação Indique e Ganhe \= 28 Influenciadores \= 17 Google Ads \= 18 Busca no Google \= 29 Chat do site \= 24 Assessoria de Imprensa \= 25 Parcerias \= 26 Landing Page da Unidade \= RC\_GENERATOR YouTube \= 30 Ecommerce / Marketplace \= 31 Mala Direta \= 41 Reativação de base \= 35 Licenciada Home Based \= 32 Aplicativo \= 36 Particular do colaborador \= 39 Fluxo de nutrição \= 38 Venda Avulsa \= 42 Telefone / Ligação \= 43 Fidelidade \= 45 Prospecção ativa \= 46 Site \= 47 \[Expansão\] Indicação Orgânica ou de licenciado \= 27 \[Expansão\] Landing Page Expansão \= STORE Ads \[Automação\] \= 33 Ecossistema Grupo Boto \= 44 Vendas recorrentes \= REPEAT\_SALE Eventos \= UC\_QLOVIM |
| Negócio | Informações da fonte | SOURCE\_DESCRIPTION | Pode ser preenchido manualmente pelo usuário ou automaticamente via automação. Quando por automação, usamos o padrão: {utm\_campaign} {campaign\_id} \- {utm\_medium} \- {utm\_content} |
| Negócio | UTM Source | UTM\_SOURCE | Campo nativo |
| Negócio | UTM Medium | UTM\_MEDIUM | Campo nativo |
| Negócio | UTM Campaign | UTM\_CAMPAIGN | Campo nativo |
| Negócio | Campaign ID (deal) | UF\_CRM\_1651849445 | Campo personalizado preenchido via automação |
| Negócio | UTM Content | UTM\_CONTENT | Campo nativo |
| Negócio | UTM Term | UTM\_TERM | Campo nativo |
| Negócio | Unidade Definitiva \[Relatório\] | UF\_CRM\_1621027933376 | Campo personalizado em formato “string fixa” sendo sempre preenchido via automação com uma das opções abaixo. não selecionado   DF Brasília   GO Goiânia   GO Rio Verde   MA São Luís   MG Curvelo   MG Divinópolis   MG Governador Valadares   MG Uberlândia   MS Campo Grande   MS Três Lagoas   MT Primavera do Leste   PR Cascavel   PR Curitiba   PR Londrina   PR Maringá   RS Santo Ângelo   SC Chapecó   SC Joinville   SP Araraquara   SP Araras   SP Assis   SP Atibaia   SP Barretos   SP Bauru   SP Botucatu   SP Bragança Paulista   SP Catanduva   SP Caçapava   SP Campinas   SP Capivari   SP Garça   SP Guarulhos   SP Indaiatuba   SP Itatiba   SP Itu   SP Jaboticabal   SP Limeira   SP Lins   SP Marília   SP Mirassol   SP Novo Horizonte   SP Paraguaçu Paulista   SP Paulínia   SP Piracicaba   SP Presidente Prudente   SP Ribeirão Preto   SP Rio Claro   SP São Caetano do Sul   SP São Carlos   SP São José do Rio Preto   SP São Paulo \- Perdizes   SP São Paulo \- Tatuapé   SP Sorocaba   SP Valinhos   Sede OligoFlora Brasil   Não tem Oligo perto de mim |
| Negócio | Teste | UF\_CRM\_1632755419 | N \= não Y \= sim |
| Negócio | Criado por | CREATED\_BY\_ID |  |
| Negócio | Criado em (nativo) | DATE\_CREATE | Campo nativo somente leitura que registra o momento exato em que o negócio foi criado \- manualmente ou por automação. Como o servidor do Bitrix24 fica na Rússia, é comum ter uma variação de 6h no fuso horário. |
| Negócio | Criado em (deal) \[Relatório\]  | UF\_CRM\_1648177511 | Por conta do fuso, criamos esse campo personalizado que possui uma autommação corrigindo o fuso e colocando o horário exato. Recomendamos usá-lo para listar negócios com mais assertividade por exemplo. |
| Negócio | \[Automação\] Serviço | UF\_CRM\_1669147796 | Preenchido por automação com base na Campanha e chaves {Nome do Serviço} |
| Negócio | \[Unidade\] Motivo da perda | UF\_CRM\_1619794107548 | Por se tratar de um campo tipo lista, cada entrada tem um ID diferente conforme abaixo: *ID | Respectivo motivo* 325 \= Clicou sem querer 327 \= Nunca respondeu 329 \= Perdeu interesse 331 \= Comprou em outra clínica 333 \= Parou de responder 1179 \= Número inválido ou inexistente 1205 \= Não tenho dinheiro/crédito 1225 \= Já cadastrou recentemente 1237 \= Problemas de saúde pessoal, família, pets 1805 \= É de outra cidade 1233 \= Mudou de cidade 1231 \= Propaganda 1227 \= Interno / colaborador 1229 \= \[2 Whats\] Comprou e quer agendar no outro número 1827 \= Buscando emprego 2017 \= Já comprou recentemente 2097 \= Alerta\!\!\! não quer contato / não chamar 2099 \= Descadastrou 2137 \= Cadastro / lançamento errado 2705 \= Faltou e não respondeu mais 2707 \= Desmarcou e não respondeu mais 2709 \= Fez orçamento e não respondeu mais 731 \= Migração de sistema 4105 \= Tem interrese, mas não pode no momento |
| Negócio | Responsável | ASSIGNED\_BY\_ID |  |
| Negócio | Tipo de Orçamento | UF\_CRM\_1619793389604 | Campo usado como “resumo” do que foi comprado pelo cliente. Se tiver “Linha” no nome, é porque se trata de um produto. Se não tiver, é um serviço. 1109 \= Avaliações e consultas 255 \= Bem-estar e funcionais 249 \= Corporais 251 \= Faciais e pele 253 \= Epilação 1111 \= Minimamente invasivos 1113 \= Linha Day-by-Day Acessórios 1115 \= Linha Day-by-Day Bem-estar e saúde 1161 \= Linha Day-by-Day Corporais 1163 \= Linha Day-by-Day Faciais e pele 1165 \= Linha Day-by-Day Nutra 1167 \= Linha Day-by-Day Outros 1169 \= Linha Profissional Acessórios 1171 \= Linha Profissional Bem-estar e saúde 1173 \= Linha Profissional Corporais 1175 \= Linha Profissional Faciais e pele 1177 \= Linha Profissional Insumos 1699 \= Linha Profissional Manipulados |

