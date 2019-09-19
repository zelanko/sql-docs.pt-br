---
title: Notas sobre a versão do SSMS (SQL Server Management Studio) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 09/04/2019
ms.openlocfilehash: 7f9195b2ec4cfd80d16f37884ce27e920580463c
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874555"
---
# <a name="release-notes-for-sql-server-management-studio-ssms"></a>Notas sobre a versão do SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

Este artigo fornece detalhes sobre atualizações, aprimoramentos e correções de bug para as versões atuais e anteriores do SSMS.

<!--
The latest ## H2 section of this Release Notes article has been reformatted to match the new standard.
The new standard replaces the use of bullet lists with the 2-column markdown table format.
Please use the new 2-column table format going forward.
And please do include the final blank row of "| &nbsp;| &nbsp;|".

The ## H2 titles are also being shortened, by the removal of unnecessary repetitive strings.
In this case, "## SSMS 17.9" is being shortened to "## 17.9" (as one standard actual example).
Also, we are appending the 'Month yyyy.'

Also, this file has been renamed to the new standard, which calls for the file name to be with "release-notes-[techAreaName].md."
The old name for this file was 'sql-server-management-studio-changelog-ssms.md'.
But today the new file name is 'release-notes-ssms.md' (still in 'docs/ssms/').

Thank you.
GeneMi. 2019/04/02.
-->

## <a name="ssms-182"></a>SSMS 18.2

Baixar: [Baixar o SSMS 18.2](download-sql-server-management-studio-ssms.md)  
Número de build: 15.0.18142.0  
Data de lançamento: 25 de julho de 2019

O SSMS 18.2 é a versão mais recente de GA (disponibilidade geral) do SSMS. Se você precisar de uma versão anterior do SSMS, veja [versões anteriores do SSMS](release-notes-ssms.md#previous-ssms-releases).

A versão 18.2 é uma atualização da 18.1, com os seguintes itens novos e correções de bug.

## <a name="whats-new-in-182"></a>Novidades na versão 18.2

|  Novo item  |  Detalhes  |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Integration Services (SSIS) | Otimização de desempenho para o agendador de pacotes SSIS no Azure. |
| IntelliSense/editor | Adicionado suporte para classificação de dados. |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | Adicionado suporte ao IntelliSense. |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | Ativa uma otimização no mecanismo de banco de dados que ajuda a melhorar a taxa de transferência para inserções de alta simultaneidade em um índice. Essa opção destina-se a índices que estão sujeitos a contenção de inserção de última página, geralmente vista com os índices que têm uma chave sequencial, tal como uma coluna de identidade, uma sequência ou uma coluna de data/hora. Para obter mais detalhes, confira [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys). |
| Execução ou resultados de consulta | Adicionado um *tempo para conclusão* nas mensagens para acompanhar quando a execução de uma determinada consulta foi concluída. |
| Execução ou resultados de consulta | Permitem que mais dados sejam exibidos (resultado para texto) e armazenados em células (resultado para grade). O SSMS agora permite até 2 milhões de caracteres para esses formatos (limite que antigamente era de 256 mil e 64 mil, respectivamente). Isso também resolveu o problema dos usuários que não conseguiam obter mais de 43.680 caracteres das células da grade. |
| Plano de Execução | Adicionado um novo atributo no QueryPlan quando o [recurso de UDF escalar embutido](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining) está habilitado (ContainsInlineScalarTsqludfs). |
| SMO | Adicionado suporte para a *API de Avaliação do SQL*. Para obter mais informações, confira [API de Avaliação do SQL](https://docs.microsoft.com/sql/sql-assessment-api/sql-assessment-api-overview). |
|  |  |

## <a name="bug-fixes-in-182"></a>Correções de bugs na versão 18.2

|  Novo item  |  Detalhes  |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Acessibilidade | Atualização da interface do usuário do XEvent (a grade) para que seja classificável após o pressionamento de F3. |
| Always On | Corrigido um problema em que o SSMS estava gerando um erro ao tentar excluir um AG (grupo de disponibilidade) |
| Always On | Corrigido um problema em que o SSMS estava apresentando o assistente de failover errado quando as réplicas são configuradas como síncronas, ao usar AGs de escala de leitura (CLUSTER_TYPE=NONE). Agora, o SSMS apresenta o assistente para a opção Force_Failover_Allow_Data_Loss, que é o único permitido para disponibilidade com CLUSTER_TYPE=NONE |
| Always On | Corrigido um problema em que o assistente estava restringindo o número de sincronizações permitidas para três |
| Classificação de dados | Corrigido um problema em que o SSMS estava lançando um erro *O índice (baseado em zero) deve ser maior ou igual a zero* ao tentar exibir relatórios de classificação de dados em bancos de dados com CompatLevel menor que 150. |
| SSMS geral | Corrigido um problema em que o usuário não conseguia acessar o painel de resultados de rolagem horizontal usando o botão de rolagem do mouse. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/34145641) para obter mais detalhes. |
| SSMS geral | Atualizado o *Monitor de Atividade* para ignorar tipos de espera benignos SQLTRACE_WAIT_ENTRIES |
| SSMS geral | Corrigido um problema em que algumas opções de cores *(Editor de Texto > Guia Editor e Barra de Status)* não eram persistidas. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37924165)
| SSMS geral | Na caixa de diálogo de conexão, *Azure Active Directory – Universal com suporte de MFA* foi substituído por *Azure Active Directory – Universal com MFA* (a funcionalidade é a mesma, mas provavelmente menos complicada). |
| SSMS geral | Atualizado o SSMS para usar valores padrão corretos ao criar um Banco de Dados SQL do Azure. |
| SSMS geral | Corrigido um problema em que o usuário não era capaz de *iniciar o PowerShell* de um nó em [Registrar Servidores](register-servers/register-servers.md) quando o servidor é um [contêiner SQL do Linux](../linux/quickstart-install-connect-docker.md). |
| Importar arquivo simples | Corrigido um problema em que *Importar Arquivo Simples* não estava funcionando após a atualização do SSMS 18.0 para o 18.1. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37912636) |
| Importar arquivo simples | Corrigido um problema em que o *Assistente Importar Arquivo Simples estava relatando uma coluna inválida ou duplicada* em um arquivo .csv com cabeçalhos contendo caracteres Unicode. |
| Pesquisador de Objetos | Corrigido um problema em que alguns itens de menu (por exemplo, *Assistente de Importação e Exportação do SQL Server* do SQL Server) ficavam ausentes ou desabilitados quando conectados ao SQL Express. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37500016) para obter mais detalhes. |
| Pesquisador de Objetos | Correção de um problema que estava fazendo com que o SSMS falhasse quando um objeto era arrastado do Pesquisador de Objetos para o editor. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37887988) para obter mais detalhes. |
| Pesquisador de Objetos | Corrigido um problema em que a renomeação de bancos de dados estava fazendo com que nomes incorretos de banco fossem exibidos no Pesquisador de Objetos. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37638472) para obter mais detalhes. |
| Pesquisador de Objetos | Corrigido um problema pendente há muito tempo em que a tentativa de expandir o nó *Tabelas* no Pesquisador de Objetos para um banco de dados definido para usar um agrupamento que não era mais compatível com o Windows disparava um erro (e o usuário não podia expandir as tabelas dele). Um exemplo de agrupamento desse tipo seria Korean_Wansung_Unicode_CI_AS. |
| [Registrar servidores](register-servers/register-servers.md) | Corrigido um problema em que a tentativa de emitir uma consulta em vários servidores (em um *grupo* em servidores registrados) quando o servidor registrado usa *Active Directory – Integrado* ou *Azure Active Directory – Universal com MFA* não funcionava porque o SSMS falhava em se conectar. |
| [Registrar servidores](register-servers/register-servers.md) | Corrigido um problema em que a tentativa de emitir uma consulta em vários servidores (em um *grupo* em servidores registrados) quando o servidor registrado usa *Active Directory – Senha* ou *Autenticação SQL* e o usuário escolhia a opção de não lembrar a senha resultava em falha do SSMS. |
| Relatórios | Corrigido um problema nos relatórios de *uso do disco* em que o relatório falhava quando os arquivos de dados tinham um grande número de extensões. |
| Ferramentas de replicação | Corrigido um problema em que o Replication Monitor não funcionava com o BD do publicador em AG e com o distribuidor em AG (anteriormente corrigido no SSMS 17.x) |
| SQL Agent | Corrigido um problema que adicionar, inserir, editar ou remover etapas de trabalho causava a redefinição do foco para a primeira linha, em vez de para a linha ativa. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/38070892) para obter mais detalhes. |
| SMO/script | Corrigido um problema em que *CREATE OR ALTER* não estava criando scripts de objetos que continham propriedades estendidas. Confira [UserVoice](https://feedback.azure.com/forums/908035-sql-server/suggestions/37236748) para obter mais detalhes. |
| SMO/script | Corrigido um problema em que o SSMS não conseguia criar o script CREATE EXTERNAL LIBRARY corretamente. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37868089) para obter mais detalhes. |
| SMO/script |  Corrigido um problema em que a tentativa de executar *Gerar Scripts* em um banco de dados com alguns milhares de tabelas fazia com que a caixa de diálogo de progresso parecesse estar paralisada. |
| SMO/script | Corrigido um problema em que o script de *Tabela Externa* no SQL 2019 não funcionava. |
| SMO/script | Corrigido um problema em que o script de *Fonte de Dados Externa* no SQL 2019 não funcionava. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/34295080) para obter mais detalhes. |
| SMO/script | Corrigido um problema em que as *propriedades estendidas* nas colunas não eram inseridas no script quando destinadas ao BD SQL do Azure. Confira [stackoverflow](https://stackoverflow.com/questions/56952337/how-can-i-script-the-descriptions-of-columns-in-ms-sql-server-management-studio) para obter mais detalhes. |
| SMO/script | Inserção na última página: SMO – adicionar propriedade *Index.IsOptimizedForSequentialKey* |
|**Instalação do SSMS**| **Foi atenuado um problema em que a instalação do SSMS era bloqueada incorretamente, relatando idiomas incompatíveis. Isso pode ter sido um problema em algumas situações anormais, tais como uma instalação anulada ou uma desinstalação incorreta de uma versão anterior do SSMS. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37483594/) para obter mais detalhes.** |
| XEvent Profiler | Corrigida uma falha quando o visualizador estava sendo fechado. |

### <a name="known-issues-182"></a>Problemas conhecidos (18.2)

- O diagrama de banco de dados criado no SSMS em execução no computador A não pode ser modificado por meio do computador B (ele falharia em SSMS). Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37992649) para obter mais detalhes.

- Problemas do SSMS 18.0 em redesenhar ao alternar entre várias janelas de consulta. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37474042). Uma solução alternativa para esse problema é desabilitar a aceleração de hardware em **Ferramentas** > **Opões**.

- Há uma limitação sobre o tamanho dos dados que você vê dos resultados do SSMS mostrados na grade, no texto ou no arquivo.

- Há um problema com o recebimento de um erro ao excluir um Banco de Dados SQL do Azure no Pesquisador de Objetos, mas, na verdade, ele é bem-sucedido. A tarefa mostra uma mensagem de erro imprecisa.

- O idioma padrão para logons do SQL pode ser exibido como árabe na caixa de diálogo Propriedades de Logon, independentemente do idioma padrão real definido para o logon. Para exibir o idioma padrão real de um determinado logon, use o T-SQL para selecionar **default_language_name** do logon de **master.sys.server_principles**.

Você pode consultar [UserVoice](https://feedback.azure.com/forums/908035-sql-server) para conferir outros problemas conhecidos e fornecer comentários à equipe do produto.

## <a name="previous-ssms-releases"></a>Versões anteriores do SSMS

Baixe versões anteriores do SSMS clicando nos links de título nas seções a seguir:

## <a name="downloadssdtmediadownloadpng-ssms-181httpsgomicrosoftcomfwlinklinkid2094583"></a>![baixar](../ssdt/media/download.png) [SSMS 18.1](https://go.microsoft.com/fwlink/?linkid=2094583)

- Número da versão: 18.1  
- Número de build: 15.0.18131.0  
- Data de lançamento: 11 de junho de 2019  

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40a)

O SSMS 18.1 é a versão mais recente de GA (disponibilidade geral) do SSMS. Se você precisar de uma versão anterior do SSMS, veja [versões anteriores do SSMS](release-notes-ssms.md#previous-ssms-releases).

A versão 18.1 é uma pequena atualização da versão 18.0 com as seguintes itens novos e correções de bug.

## <a name="whats-new-in-181"></a>Novidades na versão 18.1

| Novo item| Detalhes|
| :-------| :------|
| Diagramas de banco de dados | [Os diagramas de banco de dados foram adicionados novamente ao SSMS](https://feedback.azure.com/forums/908035/suggestions/37507828).
| SSBDIAGNOSE.EXE |A ferramenta Diagnóstico do SQL Server (ferramenta de linha de comando) foi adicionada novamente ao pacote do SSMS.|
| Integration Services (SSIS) | Compatibilidade com o agendamento do pacote do SSIS, localizado no Catálogo do SSIS no Azure ou no Sistema de Arquivos no Azure. Há três entradas para iniciar a caixa de diálogo Novo agendamento, o item de menu *Novo agendamento…* mostrado ao clicar com o botão direito do mouse no pacote do Catálogo do SSIS no Azure; o item de menu *Agendar Pacote do SSIS no Azure* em *Migrar para o Azure* no item de menu *Ferramentas*; e "Agendar o SSIS no Azure", mostrado ao clicar com o botão direito do mouse na pasta Trabalhos no agente do SQL Server da instância gerenciada do Banco de Dados SQL do Azure.|

## <a name="bug-fixes-in-181"></a>Correções de bugs na versão 18.1

| Novo item | Detalhes |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Acessibilidade | Acessibilidade aprimorada da interface do usuário do Trabalho do Agente. |
| Acessibilidade | Acessibilidade aprimorada na página do Stretch Monitor ao adicionar um nome acessível ao botão *Atualização Automática* e um Nome Acessível inteligente que ajuda os usuários a saber não só qual é o botão, mas também o impacto de pressioná-lo. |
| Integração com o ADS| Corrigida uma possível falha no SSMS ao tentar usar os servidores registrados do ADS.|
| Designer de banco de dados | Compatibilidade com a ordenação Latin1_General_100_BIN2_UTF8 (disponível no SQL Server 2019 CTP 3.0) |
| Classificação de dados | Evitar o acréscimo de rótulo de confidencialidade às colunas na tabela de histórico, o que não é compatível. |
| Classificação de dados | Corrigido o problema relacionado com o tratamento incorreto do nível de compatibilidade (servidor x banco de dados). |
| Designer de banco de dados | Compatibilidade com a ordenação Latin1_General_100_BIN2_UTF8 (disponível no SQL 2019 CTP 3.0). |
| SSMS geral | Corrigido um problema em que o script das pseudocolunas em um índice estava incorreto. |
| SSMS geral | Corrigido um problema na página de propriedades Logon em que clicar no botão *Adicionar Credencial* poderia gerar uma Exceção de Referência Nula. |
| SSMS geral | Corrigida a exibição do tamanho da coluna money em uma página de propriedades do índice. |
| SSMS geral | Corrigido um problema em que o SSMS não respeitava as configurações de *Ferramentas/Opções* do Intellisense na janela do editor do SQL. |
| SSMS geral | Corrigido um problema em que o SSMS não respeitava as configurações de Ajuda (online x offline). |
| DPI alto | Corrigido o layout dos controles nas caixas de diálogo de erro de opções de consulta incompatíveis. |
| DPI alto | Corrigido o layout dos controles na página *Novo Grupo de Disponibilidade* em algumas versões localizadas do SSMS. |
| DPI alto | Corrigido o layout da página *Nova Agenda de Trabalho*. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37632094) para obter mais detalhes. |
| Importar arquivo simples | Corrigido um problema em que as linhas poderiam ser perdidas silenciosamente durante a importação.|
| IntelliSense/editor | Redução do tráfego de consultas baseado em SMO para os bancos de dados SQL do Azure para IntelliSense. |
| IntelliSense/editor | Corrigido o erro gramatical na dica de ferramenta exibida ao digitar T-SQL para criar um usuário. Além disso, a mensagem de erro para desambiguar entre usuários e logons foi corrigida. |
| Visualizador de log | Corrigido um problema em que o SSMS sempre abria o log do servidor (ou agente), mesmo se clicasse duas vezes em um arquivo mais antigo para entrar no Pesquisador de Objetos. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37633648) para obter mais detalhes. |
| Instalação do SSMS | Corrigido o problema que fazia com que a instalação do SSMS falhasse quando o caminho do log de instalação continha espaços. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37496110) para obter mais detalhes. |
| Instalação do SSMS | Corrigido um problema em que o SSMS saía imediatamente após mostrar a tela inicial. </br> Confira estes sites para obter mais detalhes: [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37502512), [SSMS recusa-se a iniciar](https://dba.stackexchange.com/questions/238609/ssms-refuses-to-start) e [Administradores de banco de dados](https://dba.stackexchange.com/questions/237086/sql-server-management-studio-18-wont-open-only-splash-screen-pops-up). |
| Pesquisador de Objetos | Eliminada a restrição de habilitar o *início do PowerShell* quando conectado ao SQL no Linux. |
| Pesquisador de Objetos | Corrigido um problema que fazia com que o SSMS falhasse ao tentar expandir o nó do Polybase/Grupo de Escala Horizontal (quando conectado com um nó de computação). |
| Pesquisador de Objetos | Corrigido um problema em que o item de menu *Desabilitado* ainda estava habilitado, mesmo após desabilitar um determinado Índice. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37735375) para obter mais detalhes. |
| Relatórios | Corrigido o relatório para exibir GrantedQueryMemory na base de dados (relatório do painel de desempenho do SQL). Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37167289) para obter mais detalhes. |
| Relatórios | Melhoria no rastreamento do bloco de logs em cenários Always On. |
| Plano de Execução | O novo elemento de plano de execução *SpillOccurred* foi adicionado ao esquema do plano de execução. |
| Plano de Execução | Adição de leituras remotas (*ActualPageServerReads*, *ActualPageServerReadAheads* *ActualLobPageServerReads*, *ActualLobPageServerReadAheads*) ao esquema do plano de execução. |
| SMO/script | Evitar restrições de borda de consulta durante o script de tabelas sem grafo. |
| SMO/script | Remoção da restrição de classificação de confidencialidade ao executar o script de colunas com *classificação de dados*. |
| SMO/script | Corrigido um problema em que "Gerar Script" em uma tabela de grafo falha ao gerar dados. Confira [UserVoice](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898466) para obter mais detalhes. |
| SMO/script | Corrigido um problema em que o método EnumObjects() não buscava o nome do esquema de um Sinônimo. |
| SMO/script | Corrigido um problema em UIConnectionInfo.LoadFromStream() em que a seção *AdvancedOptions* não era lida (quando a senha não era especificada). |
| SQL Agent | Corrigido um problema que fazia com que o SSMS falhasse ao trabalhar com uma janela Propriedades do Trabalho. Confira [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37164244) para obter mais detalhes. |
| SQL Agent | Corrigido um problema em que o botão "Exibir" nas *Propriedades da Etapa de Trabalho* nem sempre ficava habilitado, desse modo, evitando a exibição da saída de uma determinada etapa de trabalho. |
| Interface do usuário do XEvent | A coluna "Pacote" foi adicionada à lista do XEvents para remover a ambiguidade de eventos com nomes idênticos. |
| Interface do usuário do XEvent | O mapeamento do tipo de classe "EXTERNAL LIBRARY" ausente foi adicionado a XEventUI. |

### <a name="known-issues-181"></a>Problemas conhecidos (18.1)

- Os usuários podem ver um erro ao arrastar um objeto de tabela no Pesquisador de Objetos no Editor de Consultas. Estamos cientes do problema e a correção está planejada para a próxima versão.

- As opções de cores das *Conexões em grupo* e *Conexões de servidor único* em Opções -> Editor de texto -> Guia Editor e Barra de Status -> Layout da Barra de Status e Cores não permanecem após o fechamento do SSMS 18.1. Depois que você reabrir o SSMS, a opção Cores e Layout da Barra de Status serão revertidos para o padrão (branco).

- Há uma limitação quanto ao tamanho dos dados que você vê nos resultados do SSMS mostrados na grade, no texto ou no arquivo

## <a name="downloadssdtmediadownloadpng-ssms-180httpsgomicrosoftcomfwlinklinkid2088649"></a>![baixar o](../ssdt/media/download.png) [SSMS 18.0](https://go.microsoft.com/fwlink/?linkid=2088649)

- Número da versão: 18.0  
- Número de build: 15.0.18118.0  
- Data de lançamento: 24 de abril de 2019

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x804)| [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x404)| [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x409)| [Francês](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40c)| [Alemão](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x410)| [Japonês](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x412)| [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x416)| [Russo](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x419)| [Espanhol](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40a)

### <a name="whats-new-in-180"></a>Novidades na versão 18.0

| Novo item| Detalhes|
| :-------| :------|
|Suporte para SQL Server 2019|O SSMS 18.0 é a primeira versão com *reconhecimento* total do SQL Server 2019 (nível de compatibilidade do 150).|
|Suporte para SQL Server 2019|Suporte para "BATCH_STARTED_GROUP" e "BATCH_COMPLETED_GROUP" no SQL Server 2019 e na instância gerenciada do SQL.|
|Suporte para SQL Server 2019|SMO: Suporte adicionado para Inlining do UDF.|
|Suporte para SQL Server 2019|GraphDB: Adicionar sinalizador no plano de execução para a Sequência de TC do Graph.|
|Suporte para SQL Server 2019|Always Encrypted: suporte adicionado para AEv2/Enclave.|
|Suporte para SQL Server 2019|Always Encrypted: a caixa de diálogo Conexão tem uma nova guia "Always Encrypted" quando o usuário clica no botão "Opções" para habilitar/configurar o suporte de Enclave.|
|Tamanho de download do SSMS menor| O tamanho atual é de aproximadamente 500 MB, cerca de metade do pacote SSMS 17.x.
|O SSMS é baseado no Shell Isolado do Visual Studio 2017|O novo shell (SSMS é baseado no Visual Studio 2017 15.9.11) desbloqueia todas as correções de acessibilidade que entraram no SSMS e no Visual Studio e inclui as correções de segurança mais recentes.|
|Melhorias de acessibilidade do SSMS| Foi trabalhoso solucionar problemas de acessibilidade em todas as ferramentas (SSMS, DTA e Profiler)|
|O SSMS agora pode ser instalado em uma pasta personalizada| Essa opção está disponível na linha de comando (útil para a instalação autônoma) e na interface do usuário de configuração. Na linha de comando, passe esse argumento extra para SSMS-Setup-ENU.exe:   SSMSInstallRoot=C:\MySSMS18 Por padrão, o novo local de instalação do SSMS é: %ProgramFiles(x86)%\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe.  Isso não significa que o SSMS tem várias instâncias.|
|O SSMS permite a instalação em um idioma diferente do idioma do SO|O bloqueio na configuração de idiomas mistos foi removido. Você pode, por exemplo, instalar o SSMS alemão em um Windows francês. Se o idioma do sistema operacional não coincidir com o idioma do SSMS, o usuário precisará alterar o idioma em **Ferramentas** > **Opções** > **Configurações Internacionais**, caso contrário, o SSMS mostrará a interface do usuário em inglês.|
|O SSMS não mais compartilha componentes com o Mecanismo do SQL|Empenhamos muito esforço para evitar o compartilhamento de componentes do mecanismo de SQL, que frequentemente resultava em problemas de facilidade de manutenção (um substituindo arquivos instalados pelo outro).|
|SSMS requer o NetFx 4.7.2 ou superior|Atualizamos nosso requisito mínimo do NetFx4.6.1 para NetFx4.7.2: isso permite tirar proveito das novas funcionalidades expostas pela nova estrutura.|
|Capacidade de migrar as configurações do SSMS| Quando SSMS 18 é iniciado pela primeira vez, o usuário é solicitado a migrar as configurações da versão 17.x. Agora, os arquivos de configuração do usuário são armazenados como um arquivo XML simples, melhorando a portabilidade e, possivelmente, permitindo a edição.|
|Suporte para DPI alto| DPI alto agora está habilitado por padrão.|
|O SSMS é enviado com o driver do Microsoft OLE DB| Para detalhes, veja [Baixar o Driver do Microsoft OLE DB para SQL Server](https://docs.microsoft.com/sql/connect/oledb/download-oledb-driver-for-sql-server).|
|Não há suporte para o SSMS no Windows 8. Windows 10 e Windows Server 2016 exigem a versão 1607 (10.0.14393) ou posterior|Devido à nova dependência no NetFx 4.7.2, o SSMS 18.0 não é instalado no Windows 8 e nas versões mais antigas do Windows 10 e do Windows Server 2016. A instalação do SSMS bloqueia esses sistemas. Ainda há suporte para o Windows 8.1.|
|O SSMS não é mais adicionado à variável de ambiente PATH|O caminho para SSMS.EXE (e ferramentas em geral) não é mais adicionado ao caminho. Os usuários podem adicioná-lo manualmente ou, se estiverem em um computador moderno do Windows, usar no menu Iniciar.|
|IDs de pacote não são mais necessárias para desenvolver Extensões do SSMS| No passado, o SSMS carregava seletivamente apenas os pacotes conhecidos, exigindo, assim, que os desenvolvedores registrassem o próprio pacote. Esse não é mais o caso.|
|SSMS geral|Expor a opção de configuração AUTOGROW_ALL_FILES para grupos de arquivos no SSMS.|
|SSMS geral|As opções arriscadas "lightweight pooling" e "aumento de prioridade" foram removidas da GUI do SSMS. Para obter detalhes, veja [Detalhes de aumento de prioridade – e por que não é recomendado](https://blogs.msdn.microsoft.com/arvindsh/2010/01/26/priority-boost-details-and-why-its-not-recommended/).
|SSMS geral|Novo menu e associações de teclas para criar arquivos: **CTRL+ALT+N**. **CTRL+N** continua a criar uma nova consulta.|
|SSMS geral|A caixa de diálogo **Nova Regra de Firewall** agora permite que o usuário especifique um nome de regra, em vez de gerar automaticamente um em nome do usuário.|
|SSMS geral|IntelliSense aperfeiçoado no Editor, especialmente para v140+ T-SQL.|
|SSMS geral|Adicionado suporte na interface do usuário do SSMS para UTF-8 na caixa de diálogo de ordenação.|
|SSMS geral|Alterado para "Gerenciador de credenciais do Windows" para senhas MRU da caixa de diálogo de conexão. Isso resolve um problema antigo em que a persistência de senhas nem sempre era confiável.|
|SSMS geral|Suporte aprimorado para sistemas com vários monitores, garantindo que cada vez mais caixas de diálogo e janelas sejam exibidas no monitor esperado.|
|SSMS geral|A configuração do servidor "padrão de soma de verificação de backup" foi exposta na nova página de configurações do banco de dados da caixa de diálogo Propriedades do Servidor. Para saber detalhes, veja [https://feedback.azure.com/forums/08035-sql-server/suggestions/34634974](https://feedback.azure.com/forums/08035-sql-server/suggestions/34634974).|
|SSMS geral|O "tamanho máximo para arquivos de log de erros" foi exposto em "Configurar os logs de erro do SQL Server". Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/33624115](https://feedback.azure.com/forums/908035/suggestions/33624115).|
|SSMS geral|Adicionado "Migrar para o Azure" no menu Ferramentas – integramos o Assistente de Migração de Banco de Dados e o Serviço de Migração de Banco de Dados do Azure para fornecer acesso rápido e fácil para ajudar a acelerar suas migrações para o Azure.|
|SSMS geral|Adicionada lógica para solicitar ao usuário a confirmação das transações abertas quando "Alterar a conexão" for usado.|
|Integração do Azure Data Studio|Item de menu adicionado para iniciar/baixar o Azure Data Studio.|
|Integração do Azure Data Studio|Item de menu "Iniciar o Azure Data Studio" adicionado ao Pesquisador de Objetos.|
|Integração do Azure Data Studio|Ao clicar com o botão direito do mouse em um nó de banco de dados em OE, o usuário é apresentado com menus de contexto para executar uma consulta ou para criar um notebook no Azure Data Studio.|
|Suporte para o Azure SQL| Agora, as propriedades de banco de dados de SLO/edição/MaxSize aceitam nomes personalizados, facilitando o suporte a edições futuras do banco de dados SQL do Azure.|
|Suporte para o Azure SQL| Suporte adicionado para SKUs do vCore (Uso Geral e Comercialmente Crítico): Gen4_24 e todo o Gen5.|
|Instância Gerenciada do SQL do Azure|Adicionado novos "Logons do AAD" como um novo tipo de logon do SMO e SSMS quando conectado a uma Instância Gerenciada do SQL do Azure.|
|Always On|RTO de nova operação de hash (tempo de recuperação estimado) e RPO (perda de dados estimada) no painel Always On do SSMS. Veja a documentação atualizada em [https://docs.microsoft.com/sql/database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups](../database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups.md).|
|Always Encrypted| A caixa de seleção Habilitar Always Encrypted na nova guia Always Encrypted na caixa de diálogo Conectar-se ao Servidor agora oferece uma maneira fácil de habilitar/desabilitar o Always Encrypted para uma conexão de banco de dados.|
|Always Encrypted com enclaves seguros| Várias melhorias foram feitas para dar suporte ao Always Encrypted com enclaves seguros na versão prévia do SQL Server 2019:  Um campo de texto para especificar a URL de atestado de enclave na caixa de diálogo Conectar ao Servidor (a nova guia Always Encrypted).  A nova caixa de seleção na caixa de diálogo Nova Chave Mestra da Coluna para controlar se uma nova chave mestra da coluna permite cálculos de enclave.  Outras caixas de diálogo de gerenciamento de chaves do Always Encrypted agora expõem as informações sobre quais chaves mestras da coluna permitem cálculos de enclave.|
|Arquivos de Auditoria|O método de autenticação foi alterado de Chave de Conta de Armazenamento para a autenticação baseada no Azure AD.|
|Classificação de dados| Menu de tarefas de classificação de dados reorganizado: adicionado um submenu ao menu de tarefas do banco de dados e uma opção para abrir o relatório usando o menu sem primeiro abrir a janela de dados de classificar.|
|Classificação de dados|Adicionado o novo recurso 'Classificação de dados' para o SMO. O objeto Column expõe novas propriedades: SensitivityLabelName, SensitivityLabelId, SensitivityInformationTypeName, SensitivityInformationTypeId e IsClassified (somente leitura). Para obter mais informações, veja [ADICIONAR CLASSIFICAÇÃO DE SENSIBILIDADE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/add-sensitivity-classification-transact-sql)|
|Classificação de dados|Adicionado o item de menu "Relatório de Classificação" ao menu "Classificação de Dados".|
|Classificação de dados| Recomendações atualizadas.|
|Atualização do modo de compatibilidade do banco de dados|Uma nova opção foi adicionada em ***Nome do banco de dados*** > ***Tarefas*** > ***Atualização do Banco de Dados***. Isso inicia o novo **QTA (Assistente de Ajuste de Consulta)** para orientar o usuário no processo de: Coleta de uma linha de base de desempenho antes de atualizar o nível de compatibilidade do banco de dados. Atualização para o nível de compatibilidade do banco de dados desejado.  Coleta de uma segunda passagem de dados de desempenho sobre a mesma carga de trabalho. Detectar regressões de carga de trabalho e fornecer recomendações testadas para melhorar o desempenho da carga de trabalho.  Isso está perto do processo de atualização de banco de dados documentado em [cenários de uso do repositório de consultas](https://docs.microsoft.com/sql/relational-databases/performance/query-store-usage-scenarios#CEUpgrade), exceto pela última etapa, em que o QTA não se baseia em um estado anterior sabidamente válido para gerar recomendações.|
|Assistente de Aplicativo da Camada de Dados|Adicionado suporte para importar/exportar aplicativo da camada de dados com tabelas de grafo.|
|Assistente de Importação de Arquivo Simples|Adicionada lógica para notificar o usuário de que uma importação pode ter resultado em uma renomeação das colunas.|
|Integration Services (SSIS)|Suporte adicionado para permitir aos clientes agendar pacotes do SSIS nos Azure-SSIS IRs que estão na nuvem do Azure Governamental.|
|Integration Services (SSIS)|Quando você usa o SQL Agent da instância gerenciada do SQL do Azure via SSMS, pode configurar o gerenciador de conexão e o parâmetro na etapa de trabalho de agente do SSIS.|
|Integration Services (SSIS)|Ao se conectar ao BD SQL do Azure ou à instância gerenciada do BD SQL do Azure, você pode se conectar a ele com *padrão* como banco de dados inicial.|
|Integration Services (SSIS)|Adicionado um novo item de entrada **Experimentar o SSIS no Azure Data Factory** sob o nó Catálogos do Integration Services, que pode ser usado para iniciar o Assistente de criação do Integration Runtime e criar o Azure-SSIS Integration Runtime rapidamente.
|Integration Services (SSIS)|Adicionado um botão **Criar SSIS IR** em "Assistente de Criação de Catálogo", que pode ser usado para iniciar o Assistente de criação do Integration Runtime e criar o Azure-SSIS Integration Runtime rapidamente.|
|Integration Services (SSIS)|O ISDeploymentWizard agora dá suporte à autenticação do SQL, à Autenticação Integrada do Azure Active Directory e à Autenticação de Senha do Azure Active Directory no modo de linha de comando.|
|Integration Services (SSIS)|O Assistente de Implantação agora dá suporte para a criação e a implantação para SSIS Integration Runtime do Azure Data Factory.|
|Script de Objeto|Novos itens de menu foram adicionados para "CRIAR OU ALTERAR" ao gerar script de objetos.|
|Repositório de Consultas|A usabilidade de alguns relatórios (consumos gerais de recursos) foi aprimorada, adicionando um separador de milhar a números a serem exibidos no eixo y dos gráficos.|
|Repositório de Consultas|Um novo relatório de estatísticas de espera de consulta foi adicionado.|
|Repositório de Consultas|Métrica de "Contagem de Execução" adicionada à exibição "Consulta Rastreadas".|
|Ferramentas de replicação|Adicionado suporte para o recurso de especificação de porta não padrão no Replication Monitor e no SSMS.|
|Plano de Execução|Adicionado tempo real decorrido, linhas reais versus estimativa no nó do operador ShowPlan se elas estiverem disponíveis. Isso faz com que o plano real pareça consistente com o plano de Estatísticas de Consulta ao Vivo.|
|Plano de Execução|Dica de ferramenta modificada e comentário adicionado ao clicar no botão Editar Consulta para um ShowPlan, para indicar ao usuário que o ShowPlan poderá ser truncado pelo mecanismo do SQL se a consulta tiver mais de 4.000 caracteres.|
|Plano de Execução|Adicionada lógica para exibir o "operador Materializer (seleção externa)".|
|Plano de Execução|Adicione o atributo BatchModeOnRowStoreUsed de plano de execução para identificar facilmente as consultas que estão usando o recurso "verificação de modo de lote em rowstores". Sempre que uma consulta executa a verificação de modo de lote em rowstores, um novo atributo (BatchModeOnRowStoreUsed="true") é adicionado ao elemento StmtSimple.|
|Plano de Execução|Adicionado suporte do plano de execução para LocalCube RelOp para DW ROLLUP e CUBE.|
|Plano de Execução|Novo operador LocalCube para o novo recurso de agregação de ROLLUP e CUBE no SQL Data Warehouse do Azure.|
|SMO| Estenda o suporte do SMO para a criação de índice retomável.|
|SMO| Adicionado novo evento em objetos SMO ("PropertyMissing") para ajudar os autores de aplicativos a detectar problemas de desempenho do SMO mais rapidamente.|
|SMO| A nova propriedade DefaultBackupChecksum foi exposta no objeto de configuração que mapeia para a configuração do servidor "padrão de soma de verificação de backup".|
|SMO| A nova propriedade ProductUpdateLevel foi exposta no objeto de servidor, que mapeia para o nível de manutenção para a versão do SQL em uso (por exemplo, CU12, RTM).|
|SMO| A nova propriedade LastGoodCheckDbTime foi exposta no objeto de banco de dados, que mapeia para a propriedade de banco de dados "lastgoodcheckdbtime". Se essa propriedade não estiver disponível, um valor padrão de 1/1/1900 12:00:00 AM será retornado.|
|SMO|Movida a localização para o arquivo RegSrvr.xml (arquivo de configuração do Servidor Registrado) para "%AppData%\Microsoft\SQL Server Management Studio" (sem controle de versão, assim, pode ser compartilhado entre as versões do SSMS).|
|SMO|Adicionada "Testemunha em Nuvem" como um novo tipo de quorum e como um novo tipo de recurso.|
|SMO|Adicionado suporte para "Restrições de borda" no SMO e no SSMS.|
|SMO|Adicionado suporte de exclusão em cascata para "Restrições de Borda" em SMO e SSMS.|
|SMO|Adicionado suporte para permissões de "leitura-gravação" de classificação de dados.|
|Avaliação de Vulnerabilidade| O menu de tarefas de avaliação de vulnerabilidades foi habilitado no SQL DW do Azure.|
|Avaliação de Vulnerabilidade|Alterado o conjunto de regras de avaliação de vulnerabilidade que são executadas em servidores de Instância Gerenciada do SQL do Azure, de modo que os resultados de varredura de "Avaliação de Vulnerabilidade" serão consistentes com aqueles no BD SQL do Azure.|
|Avaliação de Vulnerabilidade| A "Avaliação de Vulnerabilidades" agora dá suporte ao SQL DW do Azure.|
|Avaliação de Vulnerabilidade|Adicionado um novo recurso de exportação para exportar os resultados de varredura de avaliação de vulnerabilidade para o Excel.|
|Visualizador de XEvent|Visualizador de XEvent: habilitada a janela de plano de execução para mais XEvents.|

### <a name="bug-fixes-in-180"></a>Correções de bugs na versão 18.0

| Novo item| Detalhes|
| :-------| :------|
|Falhas e congelamentos|Corrigida uma fonte de panes comuns do SSMS relacionados a objetos GDI.|
|Falhas e congelamentos|Corrigida uma fonte comum de travamentos e desempenho ruim ao selecionar "Script como Criar/Atualizar/Soltar" (buscas desnecessárias removidas dos objetos SMO).|
|Falhas e congelamentos|Corrigido um travamento que ocorria ao se conectar a um BD SQL do Azure usando MFA enquanto rastreamentos ADAL estão habilitados.|
|Falhas e congelamentos|Corrigido um travamento (ou travamento percebido) nas Estatísticas de Consulta ao Vivo quando invocadas do Monitor de Atividade (o problema manifestado ao usar a autenticação do SQL Server com nenhum conjunto de "Informações de Persistência de Segurança").|
|Falhas e congelamentos|Corrigido um travamento ao selecionar "Relatórios" no Pesquisador de Objetos que pode se manifestar em conexões de alta latência ou não acessibilidade temporária dos recursos.|
|Falhas e congelamentos|Corrigida uma falha no SSMS ao tentar usar servidores SQL do Azure e do Servidor de Gerenciamento Central. Para obter detalhes, veja [Falha e erro de aplicativo SMSS 17.5 ao usar o Servidor de Gerenciamento Central](https://feedback.azure.com/forums/908035/suggestions/33374884).|
|Falhas e congelamentos|Corrigido um travamento no Pesquisador de Objetos ao otimizar a maneira como a propriedade IsFullTextEnabled é recuperada.|
|Falhas e congelamentos|Corrigido um travamento no "Assistente para Copiar Banco de Dados" evitando o build de consultas desnecessárias para recuperar propriedades de Banco de Dados.|
|Falhas e congelamentos|Corrigido um problema que estava fazendo com que o SSMS parasse de responder/falhasse durante a edição de T-SQL.|
|Falhas e congelamentos|Mitigado um problema em que o SSMS deixava de responder ao editar scripts do T-SQL grandes.|
|Falhas e congelamentos|Corrigido um problema que estava fazendo o SSMS ficar sem memória ao lidar com grandes conjuntos de dados retornados por consultas.|
|SSMS geral|Corrigido um problema em que "ApplicationIntent" não era passado em conexões em "Servidores Registrados".|
|SSMS geral|Corrigido um problema em que o formulário da "Nova Interface do Usuário do Assistente de Sessão XEvent" não era renderizado corretamente em monitores com alto DPI.|
|SSMS geral|Corrigido um problema ao tentar importar um arquivo bacpac.|
|SSMS geral|Corrigido um problema em que tentar exibir as propriedades de um banco de dados com (com FILEGROWTH > 2.048 GB) gerava um erro de estouro aritmético.|
|SSMS geral|Corrigido um problema em que o relatório do painel de desempenho reportava esperas de PAGEIOLATCH e PAGELATCH que não podiam ser encontradas em sub-relatórios.|
|SSMS geral|Outra rodada de correções para aprimorar o reconhecimento de vários monitores por parte do SSMS fazendo-o abrir a caixa de diálogo no monitor correto.|
|Analysis Services (AS)|Corrigido um problema em que as "Configurações Avançadas" na interface do usuário de AS XEvent eram cortadas.|
|Analysis Services (AS)|Corrigido um problema em que a análise de DAX gera uma exceção de o arquivo não encontrado.|
|Banco de dados SQL do Azure|Corrigido um problema em que a lista de banco de dados não era preenchida corretamente na janela de consulta do Banco de Dados SQL do Azure quando conectado a um banco de dados de usuário no BD SQL do Azure em vez de conectado ao mestre.|
|Banco de dados SQL do Azure|Corrigido um problema em que não era possível adicionar uma "Tabela Temporal" a um Banco de Dados SQL do Azure.|
|Banco de dados SQL do Azure|Habilitada a opção de submenu de propriedades Estatísticas no menu Estatísticas no Azure, já que tem suporte total já algum tempo agora.|
|Azure SQL – Suporte Geral|Problemas corrigidos em controle comum da interface do usuário do Azure que impedia o usuário de exibir as assinaturas do Azure (se houvesse mais de 50). Além disso, a classificação foi alterada para ser por nome em vez de usar ID de assinatura. O usuário pode usar essa opção ao tentar restaurar um backup de URL, por exemplo.|
|Azure SQL – Suporte Geral|Corrigido um problema no controle comum de interface do usuário do Azure ao enumerar as assinaturas que poderiam gerar um erro de "Índice fora do intervalo. Deve ser não negativo e menor que o tamanho da coleção." quando o usuário não tinha nenhuma assinatura em alguns locatários. O usuário pode usar essa opção ao tentar restaurar um backup de URL, por exemplo.|
|Azure SQL – Suporte Geral|Corrigido um problema em que os Objetivos de Nível de Serviço eram embutidos em código, tornando mais difícil para o SSMS dar suporte a SLOs do SQL do Azure mais recentes. Agora o usuário pode entrar no Azure e permitir que o SSMS recupere todos os dados de SLO aplicáveis (Edição e Tamanho Máximo)|
|Suporte para Instância Gerenciada do BD SQL do Azure|Melhoria no suporte para Instâncias Gerenciadas: opções sem suporte desabilitadas na interface do usuário e uma correção na opção Exibir Logs de Auditoria para lidar com o destino de auditoria da URL.|
|Suporte para Instância Gerenciada do BD SQL do Azure|O assistente "Gerar e publicar scripts" executa scripts de cláusulas CREATE DATABASE sem suporte.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Habilite Estatísticas de Consulta Ativa para Instâncias Gerenciadas.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Propriedades de banco de dados -> Arquivos estava executando incorretamente scripts ALTER DB ADD FILE.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Corrigida a regressão com o agendador do SQL Agent em que o agendamento ONIDLE era escolhido, mesmo quando algum outro tipo de agendamento era escolhido.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Ajuste de MAXTRANSFERRATE, MAXBLOCKSIZE para fazer backups no Armazenamento do Azure.|
|Suporte para Instância Gerenciada do BD SQL do Azure|O problema em que o backup da parte final do log de transações é inserido no script antes da operação RESTORE (não há compatibilidade no CL).|
|Suporte para Instância Gerenciada do BD SQL do Azure|O Assistente para Criar Banco de Dados não executava script corretamente da instrução CREATE DATABASE.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Tratamento especial de pacotes do SSIS no SSMS quando conectado a Instâncias Gerenciadas.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Corrigido um problema em que um erro era exibido durante a tentativa de usar o "Monitor de Atividade" quando conectado a Instâncias Gerenciadas.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Suporte aprimorado para logons do AAD (no Gerenciador do SSMS).|
|Suporte para Instância Gerenciada do BD SQL do Azure|Geração de script aprimorada para objetos de grupos de arquivos do SQL Server Management Objects.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Interface do usuário aprimorada para credenciais.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Suporte adicionado à replicação lógica.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Corrigido um problema que fazia com que o clique com o botão direito do mouse em um banco de dados e a seleção de "Importar aplicativo da camada de dados" falhasse.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Corrigido um problema que fazia com que clicar com o botão direito do mouse em um "TempDB" mostrasse erros.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Corrigido um problema em que tentar realizar o script da instrução ALTER DB ADD FILE no SMO estava fazendo o script T-SQL gerado ficar vazio.|
|Suporte para Instância Gerenciada do BD SQL do Azure|Aprimoramento da exibição de propriedades específicas do servidor Instâncias Gerenciadas (geração de hardware, camada de serviço, armazenamento usado e reservado).|
|Suporte para Instância Gerenciada do BD SQL do Azure|Corrigido um problema em que criar o script de um banco de dados ("Script como Criar…") não estava criando o script de grupos de arquivos e arquivos extras. Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/37326799](https://feedback.azure.com/forums/908035/suggestions/37326799). |
|Fazer backup/restaurar/anexar/desanexar o banco de dados|Corrigido um problema em que o usuário não conseguia anexar um banco de dados quando o nome do arquivo físico do arquivo .mdf não coincide com o nome do arquivo original.|
|Fazer backup/restaurar/anexar/desanexar o banco de dados|Corrigido um problema em que o SSMS podia não encontrar um plano de restauração válido ou podia encontrar um abaixo do ideal. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752). |
|Fazer backup/restaurar/anexar/desanexar o banco de dados|Corrigido um problema em que o Assistente "Anexar Banco de Dados" não exibia arquivos secundários que eram renomeados. Agora, o arquivo é exibido e um comentário sobre ele é adicionado (por exemplo, "Não encontrado"). Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/32897434](https://feedback.azure.com/forums/908035/suggestions/32897434). |
|Assistente para Copiar Banco de Dados|Assistente para Gerar script/Transferência/Copiar Banco de Dados tenta criar uma tabela com uma memória na tabela, não forçar ansi_padding em.|
|Assistente para Copiar Banco de Dados|Assistente de Transferir tarefa do Banco de dados/Copiar Banco de Dados quebrado no SQL Server 2017 e SQL Server 2019.|
|Assistente para Copiar Banco de Dados|Criação da tabela de script do Assistente para Gerar scripts/Transferir/Copiar Banco de Dados antes da criação da fonte de dados externa associada.|
|Caixa de diálogo de conexão|Habilitada a remoção de nomes de usuário da lista anterior de nome de usuário quando é pressionada a tecla DEL. Para obter detalhes, veja [Permitir a exclusão de usuários de janela de logon do SSMS](https://feedback.azure.com/forums/908035/suggestions/32897632).|
|Assistente de Importação do DAC|Corrigido um problema em que o Assistente de Importação de DAC não estava funcionando quando conectado usando o AAD.|
|Classificação de dados|Corrigido um problema ao salvar as classificações no painel de classificação de dados com outros painéis de classificação de dados abertos em outros bancos de dados.|
|Assistente de Aplicativo da Camada de Dados|Corrigido um problema em que o usuário não conseguia importar um Aplicativo da Camada de Dados (.dacpac) devido ao acesso limitado ao servidor (por exemplo, sem acesso a todos os bancos de dados no mesmo servidor).|
|Assistente de Aplicativo da Camada de Dados|Corrigido um problema que fazia com que a importação ficasse extremamente lenta quando muitos bancos de dados eram hospedados no mesmo servidor SQL do Azure.|
|Tabelas Externas|Adicionado suporte para Rejected_Row_Location na grade de propriedade, no IntelliSense, no SMO e no modelo.|
|Assistente de Importação de Arquivo Simples|Corrigido um problema em que o "Assistente de Importação de Arquivo Simples" não estava manipulando as aspas duplas corretamente (ignorando). Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/32897998](https://feedback.azure.com/forums/908035/suggestions/32897998). |
|Assistente de Importação de Arquivo Simples|Corrigido um problema relacionado ao tratamento incorreto de tipos de ponto flutuante (em localidades que usam um delimitador diferente para pontos flutuantes).|
|Assistente de Importação de Arquivo Simples|Corrigido um problema relacionado à importação de bits quando os valores são 0 ou 1. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535). |
|Assistente de Importação de Arquivo Simples|Corrigido um problema em que *floats* eram inseridos como *nulos*.|
|Assistente de Importação de Arquivo Simples|Corrigido um problema em que o assistente de importação não era capaz de processar valores decimais negativos.|
|Assistente de Importação de Arquivo Simples|Corrigido um problema em que o assistente não era capaz de importar arquivos CSV de coluna única.|
|Assistente de Importação de Arquivo Simples|estará no SSMS 17.9] Corrigido o problema em que a importação de arquivo simples não permite alterar tabela de destino quando a tabela já existe. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186). |
|Visualizador da Ajuda|Melhoria da lógica referente a respeitar os modos online/offline (ainda pode haver alguns problemas que precisam ser resolvidos).|
|Visualizador da Ajuda|Corrigida a opção "Exibir Ajuda" para respeitar as configurações online/offline. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791). |
|HADR (Alta Disponibilidade e Recuperação de Desastre)<BR> AG (Grupos de Disponibilidade)|Corrigido um problema em que as funções no assistente de "Grupos de Disponibilidade de Failover" eram sempre exibidas como "Resolvendo".|
|HADR (Alta Disponibilidade e Recuperação de Desastre)<BR> AG (Grupos de Disponibilidade)|Corrigido um problema em que o SSMS mostrava avisos truncados no "Painel de AG".|
|Integration Services (IS)|Corrigido um problema SxS de que o assistente de implantação falhava em conectar-se ao SQL Server quando o SQL Server 2019 e o SSMS 18.0 estavam instalados no mesmo computador.|
|Integration Services (IS)|Corrigido um problema em que a tarefa do plano de manutenção não pode ser editada durante a criação do plano de manutenção.|
|Integration Services (IS)|Corrigido um problema em que o assistente de implantação ficava travado se o projeto de implantação era renomeado.|
|Integration Services (IS)|Configuração de ambiente habilitada no recurso de agendamento do Azure-SSIS IR.|
|Integration Services (IS)|Corrigido um problema em que o Assistente de Criação do SSIS Integration Runtime parava de responder quando a conta do cliente pertencia a mais de um locatário.|
|Monitor de Atividade do Trabalho|Falha corrigida ao usar o Monitor de Atividade do Trabalho (com filtros).|
|Pesquisador de Objetos|Corrigido um problema em que o SSMS gerava uma exceção como "Não foi possível converter o objeto de DBNull para outros tipos" ao tentar expandir o nó "Gerenciamento" no OE (DataCollector configurado incorretamente).|
|Pesquisador de Objetos|Corrigido um problema em que o OE não estava ignorando as aspas antes de invocar "Editar Top N…", causando confusão para o designer.|
|Pesquisador de Objetos|Corrigido um problema em que o assistente para "Importar Aplicativo da Camada de Dados" estava falhando ao iniciar da árvore de Armazenamento do Azure.|
|Pesquisador de Objetos|Corrigido um problema em "Configuração do Database Mail" em que o status da caixa de seleção SSL não era persistente. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541](https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541). |
|Pesquisador de Objetos|Corrigido um problema em que o SSMS esmaecia a opção para fechar conexões existentes ao tentar restaurar o banco de dados com is_auto_update_stats_async_on.|
|Pesquisador de Objetos|Corrigido um problema em que clicar com o botão direito do mouse em nós no Pesquisador de Objetos (por exemplo, em "Tabelas", e esperar para executar uma ação, como filtrar tabelas acessando Filtro > Configurações de Filtro, o formulário de configurações de filtro podia aparecer na outra tela, em vez de onde o SSMS está ativo no momento). Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106](https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106). |
|Pesquisador de Objetos|Corrigido um problema antigo em que a tecla DELETE não estava funcionando no OE ao tentar renomear um objeto. Para saber detalhes, confira [https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510](https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510), [https://feedback.azure.com/forums/908035/suggestions/32910247](https://feedback.azure.com/forums/908035/suggestions/32910247) e outras duplicatas.|
|Pesquisador de Objetos|Ao exibir as propriedades de arquivos de banco de dados existentes, o tamanho é exibido em uma coluna "Tamanho (MB)" em vez de "Tamanho inicial (MB)", que é o exibido durante a criação de um banco de dados. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024](https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024). |
|Pesquisador de Objetos|Item de menu de contexto "Design" desabilitado em "Tabelas de Grafo", pois não há suporte para essas tabelas na versão atual do SSMS.|
|Pesquisador de Objetos|Corrigido um problema em que a caixa de diálogo "Nova Agenda de Trabalho" não renderizava corretamente em monitores com alto DPI. Para saber detalhes, veja [https://feedback.azure.com/admin/v3/suggestions/35541262](https://feedback.azure.com/admin/v3/suggestions/35541262). |
|Pesquisador de Objetos|Corrigida/aprimorada a maneira como um problema em que um tamanho de banco de dados ("tamanho (MB)") é exibido nos detalhes do Pesquisador de Objetos: apenas 2 dígitos decimais e formatado usando o separador de milhares. Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/34379308](https://feedback.azure.com/forums/908035/suggestions/34379308).|
|Pesquisador de Objetos|Corrigido um problema que fazia com que a criação de um "índice espacial" falhasse com um erro como "Para realizar esta ação, defina a propriedade PartitionScheme".|
|Pesquisador de Objetos|Melhorias de desempenho secundárias no Pesquisador de Objetos para evitar a emissão de consultas extras, quando possível.|
|Pesquisador de Objetos|A lógica foi estendida para solicitar confirmação ao renomear um banco de dados para todos os objetos de esquema (a configuração pode ser definida).|
|Pesquisador de Objetos|Adicionado o escape adequado na filtragem do Pesquisador de Objetos. Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/36678803](https://feedback.azure.com/forums/908035/suggestions/36678803). |
|Pesquisador de Objetos|Corrigido/aprimorado o modo de exibição Detalhes do Pesquisador de Objetos para mostrar os números com os separadores adequados. Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/32900944](https://feedback.azure.com/forums/908035/suggestions/32900944). |
|Pesquisador de Objetos|Corrigido o menu de contexto no nó "Tabelas" quando conectado ao SQL Express, em que o submenu "Novo" estava ausente, tabelas de grafo eram listadas incorretamente e a tabela com a Versão do Sistema estava ausente. Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/37245529](https://feedback.azure.com/forums/908035/suggestions/37245529). |
|Script de Objeto|Em geral, melhorias de desempenho – gerar scripts de WideWorldImporters leva metade do tempo em comparação com o SSMS 17.7.|
|Script de Objeto|Ao executar o script de objetos, a configuração no escopo do banco de dados que tem valores padrão é omitida.|
|Script de Objeto|Não gere o T-SQL dinâmico ao executar o script. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391). |
|Script de Objeto|Omita a sintaxe de grafo "como borda" e "como nó" ao executar script de uma tabela no SQL Server 2016 e anteriores.|
|Script de Objeto|Corrigido um problema em que o script de objetos de banco de dados falhava ao se conectar a um BD SQL do Azure usando o AAD com MFA.|
|Script de Objeto|Corrigido um problema em que tentar usar script de um índice espacial com GEOMETRY_AUTO_GRID/GEOGRAPHY_AUTO_GRID em um BD SQL do Azure gerava um erro.|
|Script de Objeto|Corrigido um problema que fazia o script do banco de dados (de um Banco de Dados SQL do Azure) sempre ser direcionado a um SQL local, mesmo que as configurações de script do "Pesquisador de Objetos" estivessem definidas para corresponder à origem.|
|Script de Objeto|Corrigido um problema ao tentar criar o script de uma tabela em um banco de dados do SQL DW do Azure envolvendo índices clusterizados e não clusterizados que estavam gerando instruções T-SQL incorretas.|
|Script de Objeto|Corrigido um problema ao tentar criar scripts de uma tabela em um banco de dados do SQL DW tanto com "Índices Columnstore Clusterizados" quanto com "Índices Clusterizados" que estavam gerando instruções T-SQL incorretas (instruções duplicadas).|
|Script de Objeto|Corrigido script de tabela particionada sem valores de intervalo (bancos de dados do SQL DW).|
|Script de Objeto|Corrigido um problema em que o usuário não conseguia criar o script de uma auditoria/especificação de auditoria SERVER_PERMISSION_CHANGE_GROUP.|
|Script de Objeto|Corrigido um problema em que o usuário não conseguia criar o script de estatísticas do SQL DW. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897296](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897296). |
|Script de Objeto|Corrigido um problema em que o "Assistente para gerar script" mostra a tabela incorreta, tendo o erro de script quando "Continuar script se houver erro" é definido como false.|
|Script de Objeto|Geração de script aprimorada no SQL Server de 2019.|
|Profiler|Adicionado o evento de "Consulta de Regravação de Tabela Agregada" aos eventos do Profiler.|
|Repositório de Dados de Consultas|Corrigido um problema em que uma exceção "DocumentFrame (SQLEditors)" era gerada.|
|Repositório de Dados de Consultas|Corrigido um problema ao tentar definir um intervalo de tempo personalizado nos relatórios de Repositório de Consultas internos em que o usuário não conseguia selecionar AM ou PM no intervalo de início/término.|
|Grade de Resultados|Corrigido um problema que usava o modo de Alto Contraste (números de linha selecionada não visível).|
|Grade de Resultados|Corrigido um problema que resultou em uma exceção de "Índice fora do intervalo" ao clicar na grade.|
|Grade de Resultados|Corrigido um problema em que a cor da tela de fundo de resultado da grade estava sendo ignorada. Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/32895916](https://feedback.azure.com/forums/908035/suggestions/32895916). |
|Plano de Execução|Novas propriedades de operador de concessão de memória são exibidas incorretamente quando há mais de um thread.|
|Plano de Execução|Adicione os 4 atributos a seguir no RunTimeCountersPerThread do plano xml de execução propriamente dito: HpcRowCount (número de linhas processadas pelo dispositivo hpc), HpcKernelElapsedUs (tempo decorrido em espera pela execução do kernel em uso), HpcHostToDeviceBytes (bytes transferidos do host para o dispositivo) e HpcDeviceToHostBytes (bytes transferidos do dispositivo ao host).|
|Plano de Execução|Corrigido um problema em que os nós do plano semelhantes são realçados na posição incorreta.|
|SMO|Corrigido um problema em que o SMO/ServerConnection não tratava conexões baseadas em SqlCredential corretamente. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941](https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941). |
|SMO|Corrigido um problema em que um aplicativo escrito usando SMO encontrava um erro ao tentar enumerar bancos de dados do mesmo servidor em vários threads, mesmo usando instâncias separadas do SqlConnection em cada thread.|
|SMO|Corrigida a regressão de desempenho em Transferir de Tabelas Externas.|
|SMO|Problema corrigido no acesso thread-safe do ServerConnection que estava fazendo o SMO vazar instâncias de SqlConnection ao ter o Azure como destino.|
|SMO|Corrigido um problema que estava causando um StringBuilder.FormatError ao tentar restaurar um banco de dados que tinha chaves em seu nome.|
|SMO|Corrigido um problema em que os bancos de dados do Azure no SMO usavam por padrão a ordenação sem diferenciação de maiúsculas e minúsculas para todas as comparações de cadeias de caracteres em vez de usar a ordenação especificada para o banco de dados.|
|Editor do SSMS|Corrigido um problema na "Tabela do sistema SQL" em que restaurar as cores padrão estava mudando a cor para verde-limão, em vez de verde padrão, dificultando a leitura em uma tela de fundo branco. Para obter detalhes, veja [Restaurar a cor padrão incorreta para a Tabela do Sistema do SQL](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896906). O problema ainda persiste em versões que não em inglês do SSMS.|
|Editor do SSMS|Corrigido o problema em que o IntelliSense não funcionava quando conectado ao SQL DW do Azure usando a autenticação do AAD.|
|Editor do SSMS|IntelliSense corrigido no Azure quando o usuário não tem acesso ao banco de dados **mestre**.|
|Editor do SSMS|Correção de snippets de código para criar &quot;tabelas temporais&quot; que foram perdidas quando a ordenação do banco de dados de destino diferenciava maiúsculas de minúsculas.|
|Editor do SSMS|Nova função TRANSLATE agora reconhecida pelo IntelliSense. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430). |
|Editor do SSMS|IntelliSense aperfeiçoado na função interna FORMAT. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676). |
|Editor do SSMS|LAG e LEAD agora são reconhecidos como funções internas. Para saber detalhes, veja [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757). |
|Editor do SSMS|Corrigido um problema em que o IntelliSense gerava um aviso ao usar "ALTER TABLE...ADD CONSTRAINT...WITH(ONLINE=ON)".|
|Editor do SSMS|Corrigido um problema em que várias exibições do sistema e funções de valores de tabela não eram corretamente coloridas.|
|Editor do SSMS|Corrigido um problema em que clicar nas guias do editor podia fazer com que a guia fosse fechada, em vez de obter o foco. Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/37291114](https://feedback.azure.com/forums/908035/suggestions/37291114). |
|Opções do SSMS|Corrigido um problema em que a página **Ferramentas** > **Opções** > **Pesquisador de Objetos do SQL Server** > **Comandos** não era redimensionada corretamente.|
|Opções do SSMS|O SSMS agora desabilitará por padrão o download automático de DTD no editor de XMLA – o editor de script XMLA (que usa o serviço de linguagem XML) agora por padrão impedirá o download automático de DTD para arquivos XMLA potencialmente mal-intencionados. Isso é controlado desativando a configuração "Baixar DTDs e esquemas automaticamente" **Ferramentas** > **Opções** > **Ambiente** > **Editor de Texto** > **XML** > **Diversos**.|
|Opções do SSMS|Restaurado **CTRL+D** para ser o atalho como costumava ser na versão mais antiga do SSMS. Para saber detalhes, veja [https://feedback.azure.com/forums/908035/suggestions/35544754](https://feedback.azure.com/forums/908035/suggestions/35544754). |
|Criador de Tabelas|Corrigida uma falha em "Editar 200 linhas".|
|Criador de Tabelas|Corrigido um problema em que o designer permitia adicionar uma tabela quando conectado a um Banco de Dados SQL do Azure.|
|Avaliação de Vulnerabilidade|Corrigido um problema em que os resultados da verificação não eram carregados corretamente.|
|XEvent|Adicionadas duas colunas "action_name" e "class_type_desc" que mostram os campos de ID da ação e tipo de classe como cadeias de caracteres legíveis.|
|XEvent|Removido o limite de 1.000.000 eventos do Visualizador de XEvent do evento.|
|XEvent Profiler|Corrigido um problema em que o XEvent Profiler falhava ao iniciar quando conectado a um SQL Server de 96 núcleos.|
|Visualizador de XEvent|Corrigido um problema em que o Visualizador de XEvent falhava ao tentar agrupar os eventos usando as "Opções da Barra de ferramentas de Evento Estendido".|

### <a name="deprecated-and-removed-features-in-180"></a>Recursos preteridos e removidos na versão 18.0

Recursos preteridos/removidos
- Depurador do T-SQL
- Diagramas de banco de dados
- As ferramentas a seguir não são mais instaladas com o SSMS:
  - OSQL.EXE
  - DReplay.exe
  - SQLdiag.exe
  - SSBDiagnose.exe
  - bcp.exe
  - sqlcmd.exe
- Ferramentas do Configuration Manager:
  - O SQL Server Configuration Manager e o Reporting Server Configuration Manager não mais fazem parte da instalação do SSMS.
- Políticas padrão de DMF
  - As políticas não são mais instaladas com o SSMS. Elas serão movidas para o Git. Se desejarem, os usuários poderão contribuir e baixar/instalar as políticas.
- Opção de linha de comando -P do SSMS removida
  - Devido a questões de segurança, a opção para especificar senhas de texto não criptografado na linha de comando foi removida.
- Gerar scripts > Publicar no Serviço Web removido
  - Este recurso preterido foi removido da interface do usuário do SSMS.
- Nó "manutenção > Herdado" removido no Pesquisador de Objetos.
  - Os nós "Plano de manutenção de banco de dados" e "SQL Mail" realmente antigos não estarão mais acessíveis. Os nós "Database Mail" e "Planos de manutenção" modernos continuarão funcionando normalmente.

### <a name="known-issues-180"></a>Problemas conhecidos (18.0)

- Talvez você encontre um problema ao instalar a versão 18.0 em que não é possível executar o SQL Server Management Studio. Se você encontrar esse problema, siga as etapas do artigo [SSMS 2018 – Instalado, mas não é executado](https://feedback.azure.com/forums/908035-sql-server/suggestions/37502512-ssms2018-installed-but-will-not-run).

- Há uma limitação quanto ao tamanho dos dados que você vê nos resultados do SSMS mostrados na grade, no texto ou no arquivo

## <a name="downloadssdtmediadownloadpng-ssms-1791httpsgomicrosoftcomfwlinklinkid2043154clcid0x409"></a>![baixar](../ssdt/media/download.png) [SSMS 17.9.1](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)

- Número da versão: 17.9.1<br>
- Número de build: 14.0.17289.0<br>
- Data de lançamento: 21 de novembro de 2018

A versão 17.9.1 é uma pequena atualização da versão 17.9 com as seguintes correções de bug:

- Corrigido um problema em que ao usarem a autenticação do "Azure Active Directory – Universal com suporte MFA" com o editor de consultas SQL, a conexão é fechada e reaberta a cada invocação de consulta. Os efeitos colaterais do fechamento da conexão incluem tabelas temporárias globais que são descartadas inesperadamente e, às vezes, um novo SPID fornecido para a conexão.
- Corrigido um problema antigo em que o plano de restauração não localiza um plano de restauração ou gera um plano de restauração ineficiente em determinadas condições.
- Corrigido um problema no assistente "Importar Aplicativo da Camada de Dados", que poderia resultar em um erro quando conectado a um Banco de Dados SQL do Azure.

> [!NOTE]
> Versões do SSMS 17.x localizadas em idiomas diferentes do inglês exigem o [pacote de atualização de segurança KB 2862966](https://support.microsoft.com/kb/2862966) se instaladas em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2.

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x804)| [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x404)| [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)| [Francês](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40c)| [Alemão](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x410)| [Japonês](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x412)| [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x416)| [Russo](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x419)| [Espanhol](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40a)

## <a name="downloadssdtmediadownloadpng-ssms-1653httpsgomicrosoftcomfwlinklinkid840946"></a>![baixar](../ssdt/media/download.png) [SSMS 16.5.3](https://go.microsoft.com/fwlink/?LinkID=840946)
Disponibilidade geral | Número de build: 13.0.16106.4

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804)| [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404)| [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409)| [Francês](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)| [Alemão](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410)| [Japonês](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412)| [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416)| [Russo](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419)| [Espanhol](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)

Os seguintes problemas foram corrigidos nesta versão:

* Corrigido um problema introduzido no SSMS 16.5.2 que estava causando a expansão do nó 'Table' quando a tabela tinha mais de uma coluna esparsa.

* Os usuários podem implantar pacotes do SSIS contendo o Gerenciador de Conexões do OData, que se conectam a um recurso do Microsoft Dynamics AX/CRM Online para o catálogo do SSIS. Para obter informações mais detalhadas, confira [Gerenciador de Conexão do OData](../integration-services/connection-manager/odata-connection-manager.md).

* Configurar Always Encrypted para uma tabela existente falha com erros em objetos não relacionados. [ID de Conexão 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* Configurar Always Encrypted para um banco de dados com vários esquemas não funciona. [ID de Conexão 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* O assistente de coluna Always Encrypted, Encrypted falha devido a banco de dados contendo exibições que referenciam exibições de sistema. [ID de Conexão 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Ao criptografar usando Always Encrypted, erros de atualização de módulos após a criptografia são manipulados incorretamente.

* O menu *Abrir recente* não mostra arquivos salvos recentemente. [ID de Conexão 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* O SSMS está lento ao clicar com o botão direito do mouse em um índice para uma tabela (mais de uma conexão remota (Internet)). [ID de Conexão 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)

* Corrigido um problema com a barra de rolagem do Designer do SQL. [ID de Conexão 3114856](https://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* O menu de contexto para tabelas trava momentaneamente 
 
* Ocasionalmente, o SSMS lança exceções no Monitor de Atividade e falha. [ID de Conexão 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* O SSMS 2016 falha com o erro "O processo foi terminado devido a um erro interno no Tempo de Execução do .NET no IP 71AF8579 (71AE0000) com código de saída 80131506"


## <a name="uninstall-and-reinstall-ssms-17x"></a>Desinstalar e reinstalar o SSMS 17.x

Se a instalação do SSMS estiver tendo problemas e uma desinstalação e reinstalação padrão não os resolver, primeiro tente [reparar](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs) o IsoShell do Visual Studio 2015. Se reparar o IsoShell do Visual Studio 2015 não resolver o problema, as etapas a seguir poderão corrigir diversos problemas aleatórios:

1. Desinstale o SSMS da mesma forma que desinstala qualquer aplicativo (usando *Aplicativos e recursos*, *Programas e recursos*, dependendo da versão do Windows).

2. Desinstale o IsoShell do Visual Studio 2015 **de um prompt de comando com privilégios elevados**:

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```

    ```vs_isoshell.exe /Uninstall /Force /PromptRestart```

3. Desinstale o Pacote Redistribuível do Microsoft Visual C++ 2015 da mesma maneira que desinstala qualquer aplicativo. Desinstale a versão x86 e a x64 se estiverem no computador.

4. Reinstale o IsoShell do Visual Studio 2015 **de um prompt de comando com privilégios elevados**:  

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```  

    ```vs_isoshell.exe /PromptRestart```

5. Reinstale o SSMS.

6. Atualize para a [versão mais recente do Pacote Redistribuível do Visual C++ 2015](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) se você não estiver atualizado.

## <a name="additional-downloads"></a>Downloads adicionais

Para obter uma lista de todos os downloads do SQL Server Management Studio, veja o [Centro de Download da Microsoft](https://www.microsoft.com/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending).  
  
Para obter a versão mais recente do SQL Server Management Studio e detalhes, confira [Baixar o SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
