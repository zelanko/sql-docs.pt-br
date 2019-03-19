---
title: Visão geral
titleSuffix: Azure Data Studio
description: O estúdio de dados do Azure é uma ferramenta gratuita, leve, que é executado no Windows, macOS e Linux, para o gerenciamento do SQL Server, banco de dados SQL e Azure SQL Data Warehouse.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: overview
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7369893be3cd42dab0e0c0cd870a52c639083b5
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161603"
---
# <a name="what-is-azure-data-studio"></a>O que é o Studio de dados do Azure?

O estúdio de dados do Azure é uma plataforma cruzada ferramenta de banco de dados para os profissionais de dados usando a família Microsoft de locais e na nuvem de plataformas de dados no Windows, MacOS e Linux.

Lançada anteriormente sob o nome de visualização do SQL Operations Studio, Studio do Azure Data oferece uma experiência de editor modernos com o Intellisense, trechos de código, integração de controle do código-fonte e um terminal integrado. Ele foi desenvolvido com o usuário de plataforma de dados em mente, com criado no gráfico de conjuntos de resultados de consulta e painéis personalizáveis.

**[Baixe e instale [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="sql-code-editor-with-intellisense"></a>Editor de códigos do SQL com o IntelliSense

[!INCLUDE[name-sos](../includes/name-sos-short.md)] oferece uma experiência que facilita as tarefas diárias com recursos internos, como várias janelas de guia, um editor avançado do SQL, IntelliSense, preenchimento de palavra-chave, trechos de código, navegação de código e controle de fonte de codificação do SQL moderno, com foco no teclado integração (Git). Executar consultas SQL e sob demanda, exibir e salvar os resultados como texto, JSON ou Excel. Editar dados, organizar suas conexões de banco de dados favoritas e procurar objetos de banco de dados em um objeto familiar a experiência de navegação. Para saber como usar o editor de SQL, consulte [usar o editor de SQL para criar objetos de banco de dados](tutorial-sql-editor.md).

## <a name="smart-sql-code-snippets"></a>Trechos de código inteligentes do SQL

Trechos de código SQL geram a sintaxe apropriada do SQL para criar bancos de dados, tabelas, exibições, procedimentos armazenados, os usuários, logons, funções, etc. e para atualizar os objetos de banco de dados existente. Use trechos de código inteligentes para rapidamente criar cópias de seu banco de dados para fins de teste ou desenvolvimento e para gerar e executar criar e inserir scripts.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] também fornece funcionalidade para criar trechos de código personalizados do SQL. Para obter mais informações, consulte [criar e usar trechos de código](code-snippets.md).


## <a name="customizable-server-and-database-dashboards"></a>Servidor personalizável e painéis de banco de dados

Crie painéis personalizáveis avançados para monitorar e solucionar rapidamente os gargalos de desempenho em seus bancos de dados. Para saber mais sobre o banco de dados (e servidor) de painéis e widgets de Insights, consulte [gerenciar servidores e bancos de dados com os widgets de Insights](insight-widgets.md).

## <a name="connection-management-server-groups"></a>Gerenciamento de Conexão (grupos de servidores)

Grupos de servidores fornecem uma maneira de organizar as informações de conexão para os servidores e trabalhar com os bancos de dados. Para obter detalhes, consulte [grupos de servidores](server-groups.md).

## <a name="integrated-terminal"></a>Terminal integrado

Use suas ferramentas favoritas de linha de comando (por exemplo, Bash, PowerShell, sqlcmd e bcp e use o ssh) na janela do Terminal integrado dentro de [!INCLUDE[name-sos](../includes/name-sos-short.md)] interface do usuário. Para saber mais sobre o terminal integrado, consulte [terminal integrado](integrated-terminal.md).

## <a name="extensibility-and-extension-authoring"></a>Extensibilidade e criação de extensão

Aprimorar o [!INCLUDE[name-sos](../includes/name-sos-short.md)] experiência, estendendo a funcionalidade da instalação base. [!INCLUDE[name-sos](../includes/name-sos-short.md)] fornece pontos de extensibilidade para atividades de gerenciamento de dados, bem como suporte para a criação de extensão.

Para saber mais sobre extensibilidade [!INCLUDE[name-sos](../includes/name-sos-short.md)], consulte [extensibilidade](extensibility.md).
Para saber mais sobre a criação de extensões, consulte [criação de extensão](extension-authoring.md).

## <a name="feature-comparison-with-sql-server-management-studio-ssms"></a>Comparação de recursos com o SQL Server Management Studio (SSMS)

**Usar o Studio de dados do Azure se você:**
- É preciso executar no macOS ou Linux
- Está se conectando a um cluster de big data do SQL Server de 2019
- Passam a maior parte do seu tempo editando ou executando consultas
- Precisa ser capaz de gráfico rapidamente e visualizar conjuntos de resultados
- Pode executar a maioria das tarefas administrativas por meio do terminal integrado usando sqlcmd ou o Powershell
- Têm pouca necessidade de experiências de Assistente
- Não é necessário fazer configuração administrativa profunda

**Use o SQL Server Management Studio se você:**
- Passam a maior parte do seu tempo em tarefas de administração de banco de dados
- Estão fazendo a configuração administrativa profunda
- Estão fazendo o gerenciamento de segurança, incluindo gerenciamento de usuário, a avaliação de vulnerabilidade e a configuração de recursos de segurança
- Fazer uso dos relatórios para SQL Server Query Store
- Precisa fazer uso de supervisores de ajuste de desempenho e painéis
- Estão fazendo a importação/exportação de DACPACs
- Precisa de acesso aos servidores registrados e deseja controle do SQL Server serviços no Windows

### <a name="shell"></a>Shell

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Entrar no Azure|Sim|Sim|
|Painel|Sim||
|Extensões|Sim||
|Terminal integrado|Sim||
|Pesquisador de Objetos|Sim|Sim|
|Script de objeto|Sim|Sim|
|Sistema de projeto|Sim||
|Selecionar da tabela|Sim|Sim|
|Controle do código fonte|Sim||
|Painel de tarefas|Sim||
|Temas|Sim||
|Modo escuro|Sim||
|Gerenciador de recursos do Azure|Visualizar||
|Assistente para Gerar Scripts||Sim|
|Importação \ exportação DACPAC||Sim|
|Propriedades de objeto||Sim|
|Criador de Tabelas||Sim|


### <a name="query-editor"></a>Editor de Consultas

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Visualizador de gráfico|Sim||
|Exportar resultados para o CSV, JSON, XLSX|Sim||
|IntelliSense|Sim|Sim|
|Trechos de código|Sim|Sim|
|Mostrar plano|Visualizar|Sim|
|Estatísticas do cliente||Sim|
|Estatísticas de consulta ao vivo||Sim|
|Opções de consulta||Sim|
|Resultados em Arquivo||Sim|
|Resultados em Texto||Sim|
|Visualizador espacial||Sim|
|SQLCMD||Sim|

### <a name="operating-system-support"></a>Suporte do sistema operacional

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Linux|Sim||
|macOS|Sim||
|Windows|Sim|Sim|

### <a name="data-engineering"></a>Engenharia de dados

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Criar Assistente de tabela externa|Visualizar||
|Integração do HDFS|Visualizar||
|Notebooks|Visualizar||

### <a name="database-administration"></a>Administração de banco de dados

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Backup / restauração|Sim|Sim|
|Importar arquivo simples|Visualizar|Sim|
|SQL Agent|Visualizar|Sim|
|SQL Profiler|Visualizar|Sim|
|Always On||Sim|
|Sempre Criptografado||Sim|
|Assistente para cópia de dados||Sim|
|Orientador de otimização de dados||Sim|
|Visualizador de Log de erro||Sim|
|Planos de manutenção||Sim|
|Consulta de vários servidor||Sim|
|Gerenciamento Baseado em Políticas||Sim|
|PolyBase||Sim|
|Repositório de Consultas||Sim|
|Servidores Registrados||Sim|
|Replicação||Sim|
|Gerenciamento de segurança||Sim|
|Service Broker||Sim|
|SQL Mail||Sim|
|Explorador de Modelos||Sim|
|Avaliação de vulnerabilidade||Sim|
|Gerenciamento de XEvent||Sim|



## <a name="next-steps"></a>Próximas etapas
- [Baixe e instale [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [Conectar e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar e consultar o banco de dados SQL](quickstart-sql-database.md)
