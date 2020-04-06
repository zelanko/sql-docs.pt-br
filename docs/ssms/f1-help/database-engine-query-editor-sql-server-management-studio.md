---
title: Editor de Consultas do Mecanismo de Banco de Dados
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/03/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a6298057dbc5d4dcb4dc71cedb166186a95cbddf
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/01/2020
ms.locfileid: "80530818"
---
# <a name="ssms-query-editor"></a>Editor de Consultas do SSMS

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

O Editor de Consultas do Mecanismo de Banco de Dados é um dos quatro editores implementados no SSMS (SQL Server Management Studio).

Use o Editor de Consultas para criar e executar scripts que contenham instruções Transact-SQL. O editor também dá suporte à execução de scripts que contêm comandos do **sqlcmd** .

Para obter uma descrição da funcionalidade implementada no Editor de Consultas e as tarefas principais que você pode executar usando o editor, confira [Editores de Consultas e de Texto](../scripting/query-and-text-editors-sql-server-management-studio.md)

![Nova Consulta](media/database-engine-query-editor-sql-server-management-studio/new-query.png)

## <a name="transact-sql-f1-help"></a>Ajuda F1 do Transact-SQL

O Editor de Consultas oferece suporte à vinculação ao tópico de referência de uma instrução Transact-SQL específica quando você seleciona F1. Para fazer isso, realce o nome de uma instrução Transact-SQL e selecione F1. O mecanismo de pesquisa de ajuda procura um tópico que tenha um atributo de ajuda F1 correspondente à cadeia de caracteres realçada.

Se o mecanismo de pesquisa de ajuda não localizar um tópico com uma palavra-chave de ajuda F1 que corresponda exatamente à cadeia de caracteres realçada, esse tópico será exibido. Nesse caso, existem duas abordagens para localizar a ajuda que você está procurando:

- Copie e cole a cadeia de caracteres do editor que você realçou na guia de pesquisa dos Manuais Online do SQL Server e faça uma pesquisa.

- Realce apenas a parte da instrução Transact-SQL que provavelmente corresponderá a uma palavra-chave de ajuda F1 aplicada a um tópico e selecione F1 novamente. O utilitário de pesquisa requer uma correspondência exata entre a cadeia de caracteres realçada e uma palavra-chave de ajuda F1 atribuída a um tópico. Se a cadeia de caracteres realçada contiver elementos exclusivos ao seu ambiente, como nomes de coluna ou de parâmetro, o mecanismo de pesquisa não obterá uma correspondência. Os exemplos das cadeias de caracteres a serem realçadas incluem:

  - O nome de uma instrução Transact-SQL, como SELECT, CREATE DATABASE ou BEGIN TRANSACTION.

  - O nome de uma função interna, como SERVERPROPERTY ou @@VERSION.

  - O nome de uma tabela de procedimento armazenado do sistema, ou exibição, como sys.data_spaces ou sp_tableoption.

## <a name="sql-editor-toolbar"></a>Barra de ferramentas do Editor SQL

Quando o Editor de Consultas está aberto, a barra de ferramentas do Editor SQL é exibida com os botões a seguir.

Você também pode adicionar a barra de ferramentas Editor de Consultas selecionando o menu **Exibir** , **Barras de Ferramentas**e, em seguida, **Editor SQL**. Se você adicionar a barra de ferramentas do SQL Editor quando nenhuma janela do Editor de Consultas estiver aberta, todos os botões ficarão indisponíveis.

![Barra de ferramentas do Editor](media/database-engine-query-editor-sql-server-management-studio/editor-toolbar.png)

### <a name="connect-using-the-editor-toolbar"></a>Conectar-se usando a barra de ferramentas do editor

Abra a caixa de diálogo **[Conectar ao Servidor](connect-to-server-database-engine.md)** . Use esta caixa de diálogo para estabelecer uma conexão a um servidor.

Você também pode se conectar ao seu banco de dados usando o [menu de contexto](#connection-using-the-context-menu).

### <a name="change-connection-using-the-editor-toolbar"></a>Alterar a conexão usando a barra de ferramentas do editor

Abra a caixa de diálogo **Conectar ao Servidor** . Use esta caixa de diálogo para estabelecer uma [conexão a um servidor diferente](f1-help-for-server-connections-sql-server-management-studio.md).

Você também pode alterar as conexões usando o [menu de contexto](#connection-using-the-context-menu).

### <a name="available-databases-using-the-editor-toolbar"></a>Bancos de dados disponíveis usando a barra de ferramentas do editor

Alteram a conexão com um banco de dados diferente do mesmo servidor.

### <a name="execute-using-the-editor-toolbar"></a>Executar usando a barra de ferramentas do editor

Executa o código selecionado ou, se nenhum código estiver selecionado, executa todo o código no Editor de Consultas.

Você também pode **Executar** uma consulta selecionando F5 ou no [menu de contexto](#execute-using-the-context-menu).

### <a name="cancel-executing-query-using-the-editor-toolbar"></a>Cancelar a execução da consulta usando a barra de ferramentas do editor

Envia uma solicitação de cancelamento ao servidor. Algumas consultas não podem ser canceladas imediatamente, mas precisam esperar por uma condição de cancelamento satisfatória. Quando transações são canceladas, podem ocorrer atrasos enquanto as transações são revertidas.

Você também pode cancelar uma consulta em execução selecionando Alt+Break.

### <a name="parse-using-the-editor-toolbar"></a>Analisar usando a barra de ferramentas do editor

Verifica a sintaxe do código selecionado. Se nenhum código for selecionado, essa opção verificará a sintaxe de todo o código na janela Editor de Consultas.

Você também pode verificar o código no Editor de Consultas selecionando Ctrl+F5.

### <a name="display-estimated-execution-plan-using-the-editor-toolbar"></a>Exibir o Plano de Execução Estimado usando a barra de ferramentas do editor

Solicita um plano de execução de consulta do processador de consultas sem executar realmente a consulta e exibe o plano na janela **Plano de execução** . Esse plano usa estatísticas de índice como uma estimativa do número de linhas que se espera que retornem durante cada parte da execução da consulta. O plano de consulta real que é usado pode ser diferente do plano de execução estimado. Isso pode ocorrer se o número de linhas retornadas for consideravelmente diferente da estimativa e o processador de consultas alterar o plano para torná-lo mais eficiente.

Você também pode exibir um plano de execução estimado selecionando Ctrl+L ou no [menu de contexto](#display-estimated-execution-plan-using-the-context-menu).

### <a name="query-options-using-the-editor-toolbar"></a>Opções de consulta usando a barra de ferramentas do editor

Abre a caixa de diálogo **Opções de Consulta** . Use esta caixa de diálogo para configurar as opções padrão para execução da consulta e para resultados da consulta.

Você também pode selecionar **Opções de Consulta** no [menu de contexto](#query-options-using-the-context-menu).

### <a name="intellisense-enabled-using-the-editor-toolbar"></a>Habilitar o IntelliSense usando a barra de ferramentas do editor

Especifica se a funcionalidade IntelliSense está disponível no Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Essa opção é definida por padrão.

Você também pode selecionar **IntelliSense Habilitado** selecionando Ctrl+B e, em seguida, Ctrl+I ou no [menu de contexto](#intellisense-enabled-using-the-context-menu).

### <a name="include-actual-execution-plan-using-the-editor-toolbar"></a>Incluir o Plano de Execução Real usando a barra de ferramentas do editor

Executa a consulta e retorna os resultados da consulta e o plano de execução usado para a consulta. Estes aparecem como um plano de consulta gráfica na janela **Plano de Execução** .

Você também pode selecionar **Incluir o Plano de Execução Real** selecionando Ctrl+M ou no [menu de contexto](#include-actual-execution-plan-using-the-context-menu).

### <a name="include-live-query-statistics-using-the-editor-toolbar"></a>Incluir Estatísticas de Consulta ao Vivo usando a barra de ferramentas do editor

Fornece informações em tempo real sobre o processo de execução da consulta, conforme os controles fluem de um operador de plano de consulta para outro.

Você também pode selecionar **Incluir Estatísticas de Consulta ao Vivo** no [menu de contexto](#include-live-query-statistics-using-the-context-menu).

### <a name="include-client-statistics-using-the-editor-toolbar"></a>Incluir Estatísticas do Cliente usando a barra de ferramentas do editor

Inclui a janela **Estatísticas do Cliente** com estatísticas sobre a consulta e sobre os pacotes de rede, além do tempo decorrido da consulta.

Você também pode selecionar **Incluir Estatísticas de Consulta ao Vivo** usando Shift+Alt+S ou no [menu de contexto](#include-client-statistics-using-the-context-menu).

### <a name="results-to-text-using-the-editor-toolbar"></a>Resultados em Texto usando a barra de ferramentas do editor

Retorna os resultados da consulta como texto na janela **Resultados** .

Você também pode retornar os resultados para texto selecionando Ctrl+T ou no [menu de contexto](#results-using-the-context-menu).

### <a name="results-to-grid-using-the-editor-toolbar"></a>Resultados em Grade usando a barra de ferramentas do editor

Retorna os resultados da consulta como uma ou mais grades na janela **Resultados** . Essa opção está normalmente habilitada por padrão.

Você também pode retornar os resultados para texto selecionando Ctrl+D ou no [menu de contexto](#results-using-the-context-menu).

### <a name="results-to-file-using-the-editor-toolbar"></a>Resultados em Arquivo usando a barra de ferramentas do editor

Quando a consulta é executada, a caixa de diálogo **Salvar Resultados** é exibida. Em **Salvar em**, selecione a pasta na qual você deseja salvar o arquivo. Em **Nome do arquivo**, digite o nome do arquivo e selecione **Salvar** para salvar os resultados da consulta como um arquivo de **Relatório** com a extensão .rpt. Para opções avançadas, clique na seta para baixo no botão **Salvar** e selecione **Salvar com Codificação**.

Você também pode retornar os resultados para texto selecionando Ctrl+Shift+F ou no [menu de contexto](#results-using-the-context-menu).

### <a name="comment-out-the-selected-lines-using-the-editor-toolbar"></a>Comentar as linhas selecionadas usando a barra de ferramentas do editor

Transforma a linha atual em um comentário adicionando um operador de comentário (--) no começo da linha.

Você também pode comentar uma linha selecionando Ctrl+K e, em seguida, Ctrl+C.

### <a name="uncomment-the-selected-lines-using-the-editor-toolbar"></a>Remover marca de comentário das linhas selecionadas usando a barra de ferramentas do editor

Transforma a linha atual em uma instrução de fonte ativa ao remover um operador de comentário (--) do começo da linha.

Você também pode remover a marca de comentário em uma linha selecionando Ctrl+K e, em seguida, Ctrl+U.

### <a name="decrease-indent-using-the-editor-toolbar"></a>Diminuir Recuo usando a barra de ferramentas do editor

Move o texto da linha para a esquerda ao remover espaços em branco no começo da linha.

### <a name="increase-line-indent-using-the-editor-toolbar"></a>Aumentar Recuo de Linha usando a barra de ferramentas do editor

Move o texto da linha para a direita ao adicionar espaços em branco no começo da linha.

### <a name="specify-values-for-template-parameters-using-the-editor-toolbar"></a>Especificar Valores para Parâmetros de Modelo usando a barra de ferramentas do editor

Abre uma caixa de diálogo que você pode usar para especificar valores para parâmetros em procedimentos e funções armazenados.

## <a name="context-menu"></a>Menu de contexto

Você pode acessar o menu de contexto *clicando com o botão direito do mouse* em qualquer lugar no editor de consultas. As opções no menu de contexto são semelhantes à Barra de Ferramentas do Editor SQL. Com o menu de contexto, você vê as mesmas opções que **Conectar** e **Executar**, mas também tem outras opções listadas como **Inserir Trecho** e **Envolver Com**.

![Opções do menu de contexto](media/database-engine-query-editor-sql-server-management-studio/context-menu.png)

### <a name="insert-snippet-using-the-context-menu"></a>Inserir Trecho usando o menu de contexto

Um snippet de código Transact-SQL é um modelo que você pode usar como um ponto de partida ao escrever novas instruções Transact-SQL no Editor de Consultas.

### <a name="surround-with-using-the-context-menu"></a>Envolver Com usando o menu de contexto

Um trecho envolver-com é um modelo que você pode usar como ponto de partida ao colocar um conjunto de instruções Transact-SQL em um bloco BEGIN, IF ou WHILE.

### <a name="connection-using-the-context-menu"></a>Conexão usando o menu de contexto

![Opções do menu de contexto](media/database-engine-query-editor-sql-server-management-studio/context-menu-connections.png)

Há mais opções de **Conexão** no menu de contexto em comparação com as opções da barra de ferramentas no SSMS.

- **Conectar** – abre a caixa de diálogo Conectar ao Servidor. Use esta caixa de diálogo para estabelecer uma conexão a um servidor.

- **Desconectar** – desconecta o Editor de Consultas atual do servidor.

- **Desconectar Todas as Consultas** – desconecta todas as conexões de consulta.

- **Alterar Conexão** – abre a caixa de diálogo Conectar ao Servidor. Use esta caixa de diálogo para estabelecer uma conexão a um servidor diferente.

### <a name="open-server-in-object-explorer-using-the-context-menu"></a>Abrir o Servidor no Pesquisador de Objetos usando o menu de contexto

O Pesquisador de Objetos fornece uma interface de usuário hierárquica e gerencia os objetos em cada instância do SQL Server. O painel de detalhes do Pesquisador de Objetos apresenta uma exibição tabular dos objetos de instância e a capacidade de procurar objetos específicos. Os recursos do Pesquisador de Objetos variam, dependendo ligeiramente do tipo de servidor, mas normalmente incluem recursos de desenvolvimento de bancos de dados e recursos de gerenciamento de todos os tipos de servidores.

### <a name="execute-using-the-context-menu"></a>Executar usando o menu de contexto

Executa o código selecionado ou, se nenhum código estiver selecionado, executa todo o código no Editor de Consultas.

### <a name="display-estimated-execution-plan-using-the-context-menu"></a>Exibir o Plano de Execução Estimado usando o menu de contexto

Solicita um plano de execução de consulta do processador de consultas sem executar realmente a consulta e exibe o plano na janela **Plano de execução** . Esse plano usa estatísticas de índice como uma estimativa do número de linhas que se espera que retornem durante cada parte da execução da consulta. O plano de consulta real que é usado pode ser diferente do plano de execução estimado. Isso pode ocorrer se o número de linhas retornadas for consideravelmente diferente da estimativa e o processador de consultas alterar o plano para torná-lo mais eficiente.

### <a name="intellisense-enabled-using-the-context-menu"></a>Habilitar o IntelliSense usando o menu de contexto

Especifica se a funcionalidade IntelliSense está disponível no Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Essa opção é definida por padrão.

### <a name="trace-query-in-sql-server-profiler-using-the-context-menu"></a>Rastrear consulta no SQL Server Profiler usando o menu de contexto

O SQL Server Profiler é uma interface para criar e gerenciar rastreamentos, além de analisar e reproduzir resultados de rastreamento. Os eventos são salvos em um arquivo de rastreamento que posteriormente pode ser analisado ou utilizado para reproduzir uma série específica de etapas na tentativa de diagnosticar um problema.

### <a name="analyze-query-in-database-engine-tuning-advisor-using-the-context-menu"></a>Analisar Consulta no Orientador de Otimização do Mecanismo de Banco de Dados usando o menu de contexto

O DTA (Orientador de Otimização do Mecanismo de Banco de Dados) da Microsoft analisa bancos de dados e faz recomendações que você pode usar para otimizar o desempenho de consultas. Você pode usar o Orientador de Otimização do Mecanismo de Banco de Dados para selecionar e criar um conjunto ideal de índices, exibições indexadas e partições de tabela sem precisar de conhecimentos avançados sobre a estrutura do banco de dados ou dos recursos internos do SQL Server. Com o DTA, é possível executar as tarefas a seguir.

### <a name="design-query-in-editor-using-the-context-menu"></a>Criar Consulta no Editor usando o menu de contexto

O Designer de Consulta e Exibição é aberto quando a definição de uma exibição é aberta; mostra os resultados de uma consulta ou exibição, ou cria ou abre uma consulta.

### <a name="include-actual-execution-plan-using-the-context-menu"></a>Incluir o Plano de Execução Real usando o menu de contexto

Executa a consulta e retorna os resultados da consulta e o plano de execução usado para a consulta. Estes aparecem como um plano de consulta gráfica na janela **Plano de Execução** .

### <a name="include-live-query-statistics-using-the-context-menu"></a>Incluir Estatísticas de Consulta ao Vivo usando o menu de contexto

Fornece informações em tempo real sobre o processo de execução da consulta, conforme os controles fluem de um operador de plano de consulta para outro.

### <a name="include-client-statistics-using-the-context-menu"></a>Incluir Estatísticas do Cliente usando o menu de contexto

Inclui a janela **Estatísticas do Cliente** com estatísticas sobre a consulta e sobre os pacotes de rede, além do tempo decorrido da consulta.

### <a name="results-using-the-context-menu"></a>Resultados usando o menu de contexto

![Opções de resultados](media/database-engine-query-editor-sql-server-management-studio/context-menu-results.png)

Você pode selecionar qualquer uma das opções desejadas de *Resultado* no menu de contexto.

- **Resultados em Texto** – Retorna os resultados da consulta como texto na janela **Resultados**.

- **Resultados em Grade** – Retorna os resultados da consulta como uma ou mais grades na janela **Resultados**.

- **Resultados em Arquivo** – Quando a consulta é executada, a caixa de diálogo **Salvar Resultados** é exibida. Em **Salvar em**, selecione a pasta na qual você deseja salvar o arquivo. Em **Nome do arquivo**, digite o nome do arquivo e selecione **Salvar** para salvar os resultados da consulta como um arquivo de **Relatório** com a extensão .rpt. Para opções avançadas, clique na seta para baixo no botão **Salvar** e selecione **Salvar com Codificação**.

### <a name="properties-window-using-the-context-menu"></a>Janela Propriedades usando o menu de contexto

A janela [Propriedades](../menu-help/properties-window-f1-help-management-studio.md) descreve o estado de um item no SQL Server Management Studio, tal como uma conexão ou um operador de plano de execução, bem como informações sobre objetos de banco de dados como tabelas, exibições e designers.

Você pode usar a janela Propriedades para exibir as propriedades da conexão atual. Muitas propriedades são somente leitura na janela Propriedades, mas podem ser alteradas em outros lugares no Management Studio. Por exemplo, a propriedade Database de uma consulta é somente leitura na janela Propriedades, mas pode ser alterada na barra de ferramentas.

### <a name="query-options-using-the-context-menu"></a>Opções de Consulta usando o menu de contexto

Abre a caixa de diálogo **Opções de Consulta** . Use esta caixa de diálogo para configurar as opções padrão para execução da consulta e para resultados da consulta.

## <a name="see-also"></a>Confira também

- [Personalizar menus e teclas de atalho](../customize-menus-and-shortcut-keys.md)

- [Atalhos de teclado do SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)
