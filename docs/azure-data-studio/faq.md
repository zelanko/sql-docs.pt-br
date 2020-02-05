---
title: Perguntas frequentes
titleSuffix: Azure Data Studio
description: Perguntas frequentes sobre o Azure Data Studio.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 1916a10a468fdc44c021e410eb1521cb7c219d58
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67959542"
---
# <a name="includeazure-data-studioincludesname-sosmd-faq"></a>[!INCLUDE[Azure Data Studio](../includes/name-sos.md)] Perguntas frequentes

## <a name="what-is-azure-data-studio"></a>O que é o Azure Data Studio?

O Azure Data Studio é um novo ambiente de desktop multiplataforma de software livre para profissionais de dados que usam a família Azure Data de plataformas de dados locais e na nuvem em Windows, MacOS e Linux. Lançado anteriormente sob o nome da versão prévia SQL Operations Studio, o Azure Data Studio oferece uma experiência moderna de editor com IntelliSense extremamente rápido, snippets de código, integração de controle do código-fonte e um terminal integrado. Ele é projetado pensando no usuário da plataforma de dados, com plotagem de conjuntos de resultados de consulta e painéis personalizáveis internos.

Pesquisas mostraram que os usuários passam muito mais tempo trabalhando em edição de consulta do que em qualquer outra tarefa com o SQL Server Management Studio. Por esse motivo, o Azure Data Studio foi projetado para concentrar-se profundamente na funcionalidade mais usada, disponibilizando experiências extras como extensões opcionais para o produto. Isso permite que cada usuário personalize seu ambiente para os fluxos de trabalho que ele mais usa.


## <a name="how-much-does-azure-data-studio-cost"></a>Quanto custa o Azure Data Studio?

O Azure Data Studio é gratuito para uso privado ou comercial.

## <a name="who-should-use-azure-data-studio"></a>Quem deve usar o Azure Data Studio

Qualquer pessoa pode usar o Azure Data Studio. No entanto, ele foi projetado para simplificar as tarefas executadas por desenvolvedores de banco de dados, administradores de banco de dados, administradores de sistema e fornecedores de software independentes.

## <a name="what-can-i-do-with-azure-data-studio"></a>O que posso fazer com Azure Data Studio?

O Azure Data Studio é criado com base no Visual Studio Code e oferece uma experiência leve de fluxo de trabalho de código moderna focada em teclado ao trabalhar com SQL Server, Banco de Dados SQL do Azure e SQL DW do Azure. O Azure Data Studio torna simples e fáceis as principais experiências que você utiliza em todos os dias com recursos internos, como janelas de várias guias, um editor SQL avançado, IntelliSense, preenchimento de palavra-chave, snippets de código e navegação de código, além de integração de controle do código-fonte (Git e TFS). Você pode executar consultas sob demanda, exibir e salvar resultados como texto, JSON ou Excel, editar dados, organizar e gerenciar suas conexões de banco de dados favoritas e procurar objetos de banco de dados em uma experiência de navegação de objeto familiar.

Use suas ferramentas de linha de comando favoritas (por exemplo, Bash, PowerShell, sqlcmd, bcp, psql e SSH) na janela do Terminal Integrado dentro da interface do usuário do Azure Data Studio. Gere e execute facilmente scripts CREATE e INSERT para seus objetos de banco de dados para criar cópias de seu banco de dados para desenvolvimento ou teste. Aumente sua produtividade com snippets de código inteligentes e experiências gráficas avançadas que criam novos bancos de dados e objetos de banco de dados (como tabelas, exibições, procedimentos armazenados, usuários, logons, funções etc.) ou atualizam objetos de banco de dados existentes. Use painéis personalizáveis avançados para monitorar e solucionar rapidamente problemas de gargalos de desempenho em seus bancos de dados locais, no Azure ou em qualquer nuvem.

O Azure Data Studio oferece uma experiência consistente para o backup e a restauração de seus bancos de dados. Com suporte planejado para Grupos de Disponibilidade Always On do SQL Server, você pode facilmente configurar, monitorar e solucionar problemas de AGs para seus bancos de dados do SQL Server mais críticos e fazer failover rápido para um banco de dados secundário durante um desastre. O Azure Data Studio foi projetado para tornar você mais produtivo no ciclo de vida de DevOps de seus bancos de dados preferidos nos sistemas operacionais de sua escolha. Como resultado, você está sempre no controle e pode reduzir os riscos, solucionar problemas mais rapidamente e fornecer continuamente valor que supere as expectativas dos clientes.

## <a name="is-azure-data-studio-open-source"></a>O é Azure Data Studio é um software livre?

O código-fonte para Azure Data Studio e seus provedores de dados estão disponíveis no GitHub. O código-fonte para o Azure Data Studio de front-end (que é baseado em Visual Studio Code) está disponível em um EULA de código-fonte que fornece direitos para modificar e usar o software, mas não para redistribuí-lo nem hospedá-lo em um serviço de nuvem. O código-fonte para os provedores de dados está disponível na licença do MIT em [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-we-plan-to-open-source-ssms"></a>Planejamos tornar o SSMS um software livre?

Não. No entanto, as ferramentas de GUI e CLI de vários sistemas operacionais da próxima geração são software livre. Por exemplo, a extensão mssql para VS Code, mssql-scripter e msql-CLI são todas software livre no GitHub. O código-fonte para o Azure Data Studio está disponível no GitHub.  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>Agora que há o Azure Data Studio, a Microsoft planeja preterir o SSMS e o SSDT? 

Não. Os investimentos nas principais ferramentas do Windows (SSMS, SSDT, PowerShell) continuarão de modo adicional à próxima geração de ferramentas de CLI e GUI de vários bancos de dados e vários OS. A meta é oferecer aos clientes a opção de usar as ferramentas que eles desejam nas plataformas que escolherem para seus cenários. O Azure Data Studio concentra-se mais nas experiências relacionadas à edição de consultas e ao desenvolvimento de dados, que pesquisas mostraram ser a funcionalidade mais usada no SQL Server Management Studio. Recursos administrativos de alto valor adicionais, como backup, restauração, gerenciamento de trabalho do agente e criação de perfil de servidor, também estão disponíveis como extensões no Azure Data Studio. O Azure Data Studio também é multiplataforma, permitindo que os usuários trabalhem na plataforma que preferirem. No entanto, o SQL Server Management Studio ainda oferece a mais ampla variedade de funções administrativas e continua sendo a principal ferramenta para tarefas de gerenciamento de plataforma. 

## <a name="when-should-i-use-azure-data-studio-vs-sql-server-management-studio"></a>Quando devo usar o Azure Data Studio vs. o SQL Server Management Studio?

*Use o Azure Data Studio se você:*

- Passa a maior parte do tempo editando ou executando consultas.
- Precisa fazer um gráfico e visualizar rapidamente os conjuntos de resultados.
- Pode executar a maioria das tarefas administrativas por meio do terminal integrado usando o sqlcmd ou o PowerShell.
- Tem necessidade mínima de experiências de assistente.
- Não precisa de configuração profunda administrativa ou relacionada à plataforma.
- Precisa executar em macOS ou Linux.

*Use o SQL Server Management Studio se você:*

- Passa a maior parte do tempo em tarefas de administração de banco de dados.
- Está fazendo uma configuração de plataforma ou administrativa complexa.
- Está fazendo gerenciamento de segurança, incluindo gerenciamento de usuários, avaliação de vulnerabilidade e configuração de recursos de segurança.
- Precisa usar painéis e consultores de ajuste de desempenho.
- Usa diagramas de banco de dados e designers de tabela.
- Está fazendo a importação/exportação de DACPACs.
- Precisa de acesso a Servidores Registrados.
- Usa o modo sqlcmd, estatísticas de consulta dinâmica ou estatísticas de cliente.

## <a name="feature-comparison"></a>Comparação de recursos

### <a name="shell-features"></a>Recursos do Shell

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Entrada no Azure|Sim|Sim|
|Painel|Sim| |
|Extensões|Sim| |
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
|Assistente para Gerar Scripts||Sim
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
|Depurador do T-SQL||Sim|

### <a name="operating-system-support"></a>Suporte do sistema operacional

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|Sim|Sim|
|macOS|Sim||
|Linux|Sim||

### <a name="data-engineering"></a>Engenharia de Dados

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Assistente de Dados Externos|Visualização||
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
|Always Encrypted||Sim|
|Assistente para Copiar Dados||Sim|
|Orientador de Otimização de Dados||Sim|
|Diagramas de banco de dados||Sim|
|Visualizador de Log de Erros||Sim|
|Planos de manutenção||Sim|
|Consulta Multisservidor||Sim|
|Gerenciamento Baseado em Políticas||Sim|
|PolyBase||Sim|
|Repositório de Consultas||Sim|
|Servidores Registrados||Sim|
|Replicação||Sim|
|Gerenciamento de Segurança||Sim|
|Agente de Serviço||Sim|
|SQL Mail||Sim|
|Explorador de Modelos||Sim|
|Avaliação de Vulnerabilidade||Sim|
|Gerenciamento de XEvent||Sim|


## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>O Azure Data Studio está sem um recurso que está no SSMS/SSDT. Vocês vão adicioná-lo?

Isso depende do cenário e da necessidade da empresa/do cliente. Para ajudar a priorizar, registre uma sugestão no [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>Compreendo que o Azure Data Studio e a extensão mssql para o VS Code são desenvolvidos com um novo serviço de ferramentas que usa APIs do SMO nos bastidores. O SMO está disponível no Linux e no macOS?

As APIs do SMO ainda não estão disponíveis no Linux ou no macOS de uma maneira consumível. Realizamos a portabilidade um subconjunto das APIs do SMO para o .NET Core de que precisávamos para o Azure Data Studio e planejamos expandir como parte do roteiro. O Serviço de Ferramentas SQL está no GitHub: [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>Vocês planejam realizar a portabilidade das APIs DACFx e/ou sqlpackage.exe e/ou SSDT para Linux e macOS?

Isso está no roteiro de longo prazo. Para ajudar a priorizar, registre uma sugestão no [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>Os cmdlets do SQL PowerShell estarão disponíveis no Linux e no macOS?

O SQL PowerShell está disponível atualmente na galeria do PowerShell e você pode usá-lo no Windows para trabalhar com SQL Server em execução em qualquer lugar, incluindo SQL no Linux. A oferta de cmdlets do SQL PowerShell no Linux e no macOS está no roteiro. Para ajudar a priorizar, registre uma sugestão no [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="who-usually-uses-azure-data-studio"></a>Quem geralmente usa o Azure Data Studio?

Os desenvolvedores e os DBAs geralmente são os usuários do Azure Data Studio.

## <a name="does-azure-data-studio-integrate-with-azure-sql-data-warehouse"></a>O Azure Data Studio integra-se com o SQL Data Warehouse do Azure?

Sim. O suporte do Azure Data Studio para SQL Data Warehouse do Azure está atualmente em versão prévia, junto com a Instância Gerenciada do Banco de Dados SQL do Azure e o Big Data do SQL Server 2019.

## <a name="why-is-azure-data-studio-important-for-the-new-version-of-sql-server"></a>Por que o Azure Data Studio é importante para a nova versão do SQL Server?

Uma vez que o SQL Server estende suas funcionalidades para o espaço de Big Data, ele precisa de novas ferramentas para dar suporte a esses casos de uso. Por esse motivo, o Azure Data Studio está atualmente lançando uma nova experiência de versão prévia de suporte para o SQL Server Big Data, incluindo a primeira experiência de notebook no conjunto de ferramentas SQL Server e um novo assistente para Criar Tabela Externa que torna o acesso a dados do SQL Server remoto e Instâncias do Oracle fácil e rápido.
