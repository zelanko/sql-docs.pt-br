---
title: O que é o Azure Data Studio
titleSuffix: Azure Data Studio
description: O Azure Data Studio é uma ferramenta gratuita e leve que é executada no Windows, no macOS e no Linux para gerenciar o SQL Server, o Banco de Dados SQL do Azure e o SQL Data Warehouse do Azure.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: overview
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.openlocfilehash: 1dd66b432ff489b5576b9ce7f69c1860cb9240d5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958931"
---
# <a name="what-is-azure-data-studio"></a>O que é o Azure Data Studio?

O Azure Data Studio é uma ferramenta de banco de dados multiplataforma para profissionais de dados que usam a família Microsoft de plataformas de dados locais e na nuvem em Windows, MacOS e Linux.

Lançado anteriormente com o nome de versão prévia SQL Operations Studio, o Azure Data Studio oferece uma experiência moderna de editor com IntelliSense, snippets de código, integração de controle do código-fonte e um terminal integrado. Ele é projetado pensando no usuário da plataforma de dados, com plotagem de conjuntos de resultados de consulta e painéis personalizáveis internos.

**[Baixar e instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="sql-code-editor-with-intellisense"></a>Editor de código SQL com IntelliSense

O [!INCLUDE[name-sos](../includes/name-sos-short.md)] oferece uma experiência de codificação de SQL moderna, voltada ao teclado, que facilita tarefas diárias com recursos internos, como janelas de várias guias, um editor SQL avançado, IntelliSense, preenchimento de palavra-chave, snippets de código e navegação de código, além de integração de controle do código-fonte (Git). Execute consultas SQL sob demanda, exiba e salve resultados como texto, JSON ou Excel. Edite dados, organize suas conexões de banco de dados favoritas e procure objetos de banco de dados em uma experiência de navegação de objetos familiar. Para saber como usar o editor SQL, confira [Usar o editor SQL para criar objetos de banco de dados](tutorial-sql-editor.md).

## <a name="smart-sql-code-snippets"></a>Snippets de código SQL inteligentes

Os snippets de código SQL geram a sintaxe SQL adequada para criar bancos de dados, tabelas, exibições, procedimentos armazenados, usuários, logons, funções, entre outros, e para atualizar objetos de banco de dados existentes. Use snippets inteligentes para criar rapidamente cópias de seu banco de dados para fins de desenvolvimento ou teste e para gerar e executar scripts CREATE e INSERT.

O [!INCLUDE[name-sos](../includes/name-sos-short.md)] também fornece funcionalidade para criar snippets de código SQL personalizados. Para saber mais, confira [Criar e usar snippets de código](code-snippets.md).


## <a name="customizable-server-and-database-dashboards"></a>Dashboards personalizáveis de servidor e banco de dados

Crie painéis personalizáveis avançados para monitorar e solucionar rapidamente problemas de gargalos de desempenho em seus bancos de dados. Para saber mais sobre os widgets de insights e os painéis de banco de dados (e servidor), confira [Gerenciar servidores e bancos de dados com widgets de insight](insight-widgets.md).

## <a name="connection-management-server-groups"></a>Gerenciamento de conexões (grupos de servidores)

Grupos de servidores proporcionam uma maneira de organizar informações de conexões dos servidores e bancos de dados com que você trabalha. Para obter detalhes, confira [Grupos de servidores](server-groups.md).

## <a name="integrated-terminal"></a>Terminal Integrado

Use suas ferramentas de linha de comando favoritas (por exemplo, Bash, PowerShell, sqlcmd, bcp e SSH) na janela do Terminal Integrado dentro da interface do usuário do [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Para saber mais sobre o terminal integrado, confira [Terminal integrado](integrated-terminal.md).

## <a name="extensibility-and-extension-authoring"></a>Extensibilidade e criação de extensões

Aprimore a experiência do [!INCLUDE[name-sos](../includes/name-sos-short.md)] estendendo a funcionalidade da instalação básica. O [!INCLUDE[name-sos](../includes/name-sos-short.md)] fornece pontos de extensibilidade para atividades de gerenciamento de dados, bem como suporte para a criação de extensões.

Para saber mais sobre a extensibilidade no [!INCLUDE[name-sos](../includes/name-sos-short.md)], confira [Extensibilidade](extensibility.md).
Para saber mais sobre a criação de extensões, confira [Criação de extensões](extension-authoring.md).

## <a name="feature-comparison-with-sql-server-management-studio-ssms"></a>Comparação com recursos do SSMS (SQL Server Management Studio)

**Use o Azure Data Studio se você:**
- Precisa executar em macOS ou Linux
- Está se conectando a um cluster de Big Data do SQL Server 2019
- Passa a maior parte do tempo editando ou executando consultas
- Precisa traçar um gráfico e visualizar rapidamente conjuntos de resultados
- Pode executar a maioria das tarefas administrativas por meio do terminal integrado usando o sqlcmd ou o PowerShell
- Tem necessidade mínima de experiências com assistente
- Não precisa fazer uma configuração administrativa profunda

**Use o SQL Server Management Studio se você:**
- Passa a maior parte do tempo em tarefas de administração de banco de dados
- Está fazendo configuração administrativa profunda
- Está fazendo gerenciamento de segurança, incluindo gerenciamento de usuários, avaliação de vulnerabilidade e configuração de recursos de segurança
- Usa os Relatórios do Repositório de Consultas do SQL Server
- Precisa usar painéis e consultores de ajuste de desempenho
- Está fazendo a importação/exportação de DACPACs
- Precisa de acesso a Servidores Registrados e deseja controlar os serviços do SQL Server no Windows

### <a name="shell"></a>Shell

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Entrada no Azure|Sim|Sim|
|Painel|Sim||
|Extensões|Sim||
|Terminal Integrado|Sim||
|Pesquisador de Objetos|Sim|Sim|
|Script de Objeto|Sim|Sim|
|Sistema de Projeto|Sim||
|Selecionar de uma Tabela|Sim|Sim|
|Controle do Código-Fonte|Sim||
|Painel de Tarefas|Sim||
|Temas|Sim||
|Modo Escuro|Sim||
|Azure Resource Explorer|Visualização||
|Assistente para Gerar Scripts||Sim|
|Importar\Exportar DACPAC||Sim|
|Propriedades de objeto||Sim|
|Criador de Tabelas||Sim|


### <a name="query-editor"></a>Editor de Consultas

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Visualizador de Gráfico|Sim||
|Exportar Resultados para CSV, JSON, XLSX|Sim||
|IntelliSense|Sim|Sim|
|Snippets|Sim|Sim|
|Mostrar Plano|Visualização|Sim|
|Estatísticas do cliente||Sim|
|Estatísticas de Consulta Dinâmica||Sim|
|Opções de consulta||Sim|
|Resultados em Arquivo||Sim|
|Resultados em Texto||Sim|
|Visualizador Espacial||Sim|
|SQLCMD||Sim|

### <a name="operating-system-support"></a>Suporte do sistema operacional

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Linux|Sim||
|macOS|Sim||
|Windows|Sim|Sim|

### <a name="data-engineering"></a>Engenharia de Dados

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Assistente Criar Tabela Externa|Visualização||
|Integração do HDFS|Visualização||
|Notebooks|Visualização||

### <a name="database-administration"></a>Administração de banco de dados

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Backup/Restauração|Sim|Sim|
|Importação de Arquivo Simples|Visualização|Sim|
|SQL Agent|Visualização|Sim|
|SQL Profiler|Visualização|Sim|
|Always On||Sim|
|Sempre Criptografado||Sim|
|Assistente para Copiar Dados||Sim|
|Orientador de Otimização de Dados||Sim|
|Visualizador de Log de Erros||Sim|
|Planos de manutenção||Sim|
|Consulta Multisservidor||Sim|
|Gerenciamento Baseado em Políticas||Sim|
|PolyBase||Sim|
|Repositório de Consultas||Sim|
|Servidores Registrados||Sim|
|Replicação||Sim|
|Gerenciamento de Segurança||Sim|
|Service Broker||Sim|
|SQL Mail||Sim|
|Explorador de Modelos||Sim|
|Avaliação de Vulnerabilidade||Sim|
|Gerenciamento de XEvent||Sim|

## <a name="next-steps"></a>Próximas etapas

- [Baixar e instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [Conectar e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar e consultar o Banco de Dados SQL do Azure](quickstart-sql-database.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
