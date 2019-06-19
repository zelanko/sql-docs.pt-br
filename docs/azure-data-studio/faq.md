---
title: PERGUNTAS FREQUENTES
titleSuffix: Azure Data Studio
description: Perguntas frequentes (FAQ) sobre o Studio de dados do Azure.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 7bd6c42882c9adc938904621b7939bea1b0e68de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800750"
---
# <a name="includeazure-data-studioincludesname-sosmd-faq"></a>[!INCLUDE[Azure Data Studio](../includes/name-sos.md)] PERGUNTAS FREQÜENTES

## <a name="what-is-azure-data-studio"></a>O que é o Studio de dados do Azure?

O estúdio de dados do Azure é uma nova abertura de origem, ambiente de área de trabalho de plataforma cruzada para profissionais de dados usando a família de dados do Azure de locais e na nuvem de plataformas de dados no Windows, MacOS e Linux. Lançada anteriormente sob o nome de visualização do SQL Operations Studio, ofertas Studio do Azure Data um editor modernos experiência com muito mais rápido IntelliSense, trechos de código, integração de controle do código-fonte e um terminal integrado. Ele foi desenvolvido com o usuário de plataforma de dados em mente, com criado no gráfico de conjuntos de resultados de consulta e painéis personalizáveis.

Pesquisa mostrou que os usuários gastam em uma ordem de magnitude mais tempo trabalhando na edição de consulta que em qualquer outra tarefa com o SQL Server Management Studio. Por esse motivo, Azure Data Studio foi projetado para focar profundamente na funcionalidade que é usada o maior, com experiências adicionais disponibilizadas como as extensões opcionais ao produto. Isso permite que todos os usuários personalizem o ambiente para os fluxos de trabalho que eles usam com mais frequência.


## <a name="how-much-does-azure-data-studio-cost"></a>Quanto custa o Azure Data Studio?

O estúdio de dados do Azure é gratuito para uso comercial ou privado.

## <a name="who-should-use-azure-data-studio"></a>Quem deve usar o Studio de dados do Azure

Qualquer pessoa pode usar o Studio de dados do Azure. No entanto, ele foi projetado para simplificar tarefas executadas por desenvolvedores de banco de dados, os administradores de banco de dados, os administradores de sistemas e fornecedores independentes de software.

## <a name="what-can-i-do-with-azure-data-studio"></a>O que pode fazer com o Studio de dados do Azure?

O estúdio de dados do Azure é baseado no Visual Studio Code e oferece uma leve, com foco no teclado experiência de fluxo de trabalho de código moderno ao trabalhar com o SQL Server, banco de dados SQL Azure, Azure SQL DW. O estúdio de dados do Azure torna as experiências básicas que você pode confiar em todos os dias simples e fácil com recursos internos, como várias janelas de guia, um editor avançado do SQL, IntelliSense, preenchimento de palavra-chave, trechos de código e navegação de código e integração de controle do código-fonte (Git e o TFS). Você pode executar consultas sob demanda, exibir & Salvar resultados como texto, JSON ou Excel, editar dados, organizar e gerenciar suas conexões de banco de dados preferida e procurar objetos de banco de dados em um objeto familiar a experiência de navegação.

Use suas ferramentas favoritas de linha de comando (por exemplo, Bash, PowerShell, sqlcmd, bcp, psql e use o ssh) na janela do Terminal integrado diretamente na interface do usuário do Azure Data Studio. Gerar e executar criar facilmente e scripts de inserção para os objetos de banco de dados criar cópias de seu banco de dados para fins de teste ou desenvolvimento. Aumente sua produtividade com código inteligente trechos de código e rich gráficas experiências que criam novos bancos de dados e objetos de banco de dados (como tabelas, exibições, procedimentos armazenados, os usuários, logons, funções, etc.) ou atualizar os objetos de banco de dados existente. Use painéis personalizáveis avançados para monitorar e solucionar rapidamente os gargalos de desempenho em seus bancos de dados locais, no Azure ou em qualquer nuvem.

O estúdio de dados do Azure oferece uma experiência consistente para fazer backup e restaurar seus bancos de dados. Com o suporte planejado para grupos de disponibilidade do SQL Server Always-on, você pode facilmente configurar, monitorar e solucionar problemas de grupos de disponibilidade para seus bancos de dados do SQL Server críticos e rapidamente o failover para um banco de dados secundário durante um desastre. O estúdio de dados do Azure foi projetado para tornar você mais produtivo no ciclo de vida de DevOps de seus bancos de dados de escolha nos sistemas operacionais de sua escolha. Como resultado, você está sempre no controle, e você pode reduzir os riscos, resolver problemas mais rapidamente e fornecer continuamente um valor que excede as expectativas de clientes.

## <a name="is-azure-data-studio-open-source"></a>É um software livre do Studio de dados do Azure?

O código-fonte para o estúdio de dados do Azure e seus provedores de dados está disponível no GitHub. O código-fonte para o front-end Data Studio do Azure (que se baseia no Visual Studio Code) está disponível em um código-fonte EULA que fornece direitos para modificar e usar o software, mas não para redistribuí-lo ou hospedá-lo em um serviço de nuvem. O código-fonte para os provedores de dados está disponível sob a licença MIT no [ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-we-plan-to-open-source-ssms"></a>Estamos planejando software livre SSMS?

Não. No entanto, última geração ferramentas CLI e GUI para vários sistemas operacionais são software livre. Por exemplo, a extensão mssql para VS Code, scripter mssql e msql-CLI são software livre no GitHub. O código-fonte para o Studio de dados do Azure está disponível no GitHub.  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>Agora que há Studio de dados do Azure, Microsoft pretende preterir o SSMS e SSDT? 

Não. Os investimentos em ferramentas do Windows principal (SSMS, SSDT, PowerShell) continuará além da próxima geração de vários sistemas operacionais e ferramentas CLI e GUI de multi-DB. O objetivo é oferecer aos clientes a opção de usar as ferramentas que eles querem nas plataformas de sua preferência para seus cenários. O estúdio de dados do Azure mais rigidamente se concentra nas experiências em torno de edição de consulta e desenvolvimento de dados, que pesquisa tenha mostrado é o recurso mais intensamente usado no SQL Server Management Studio em uma ordem de magnitude. Recursos administrativos adicionais do alto valor, como backup, restauração, gerenciamento de trabalho do agente e a criação de perfil de servidor também estão disponíveis como extensões no estúdio de dados do Azure. O estúdio de dados do Azure também é multiplataforma, o que permite aos usuários trabalhar em sua plataforma de preferência. No entanto, SQL Server Management Studio ainda oferece uma gama mais ampla de funções administrativas e permanece a ferramenta principal para tarefas de gerenciamento da plataforma. 

## <a name="when-should-i-use-azure-data-studio-vs-sql-server-management-studio"></a>Quando devo usar o Azure Data Studio vs SQL Server Management Studio?

*Usar o Studio de dados do Azure se você:*

- Passam a maior parte do seu tempo editando ou executando consultas.
- Precisa ser capaz de gráfico e visualizar conjuntos de resultados rapidamente.
- Pode executar a maioria das tarefas administrativas por meio do terminal integrado usando sqlcmd ou o Powershell.
- Têm pouca necessidade de experiências do assistente.
- É necessário fazer deep administrativo ou configuração relacionados da plataforma.
- Você precisa executar no macOS ou Linux.

*Use o SQL Server Management Studio se você:*

- Passam a maior parte do seu tempo em tarefas de administração de banco de dados.
- Estão fazendo a configuração administrativa ou de plataforma complexa.
- Fazendo o gerenciamento de segurança, incluindo gerenciamento de usuário, a avaliação de vulnerabilidade e a configuração de recursos de segurança.
- Precisa fazer uso de painéis e consultores de ajuste de desempenho.
- Use diagramas de banco de dados e designers de tabela.
- Estão fazendo a importação/exportação de DACPACs.
- Precisa de acesso aos servidores registrados.
- Fazer uso do modo sqlcmd, em tempo real estatísticas de consulta ou estatísticas do cliente.

## <a name="feature-comparison"></a>Comparação de recursos

### <a name="shell-features"></a>Recursos do shell

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Entrar no Azure|Sim|Sim|
|Painel|Sim| |
|Extensões|Sim| |
|Terminal integrado|Sim||
|Pesquisador de Objetos|Sim|Sim|
|Script de Objeto|Sim|Sim|
|Sistema de projeto|Sim||
|Selecionar da tabela|Sim|Sim|
|Controle do código fonte|Sim||
|Painel de tarefas|Sim||
|Temas|Sim||
|Modo escuro|Sim||
|Gerenciador de recursos do Azure|Visualizar||
|Assistente para Gerar Scripts||Sim
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
|Depurador do T-SQL||Sim|

### <a name="operating-system-support"></a>Suporte do sistema operacional

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|Sim|Sim|
|macOS|Sim||
|Linux|Sim||

### <a name="data-engineering"></a>Engenharia de dados

|Recurso|Azure Data Studio|SSMS|
|:---|:---|:---|
|Assistente de dados externa|Visualizar||
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
|Diagramas de banco de dados||Sim|
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
|Avaliação de Vulnerabilidade||Sim|
|Gerenciamento de XEvent||Sim|


## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>O estúdio de dados do Azure não tem um recurso que está no SSMS para o SSDT. Você irá adicioná-lo?

Ele depende da necessidade de negócios/cliente & do cenário. Para ajudar a priorizar, uma sugestão de arquivo no [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>Entendo o que estúdio de dados do Azure e a extensão mssql para o VS Code são alimentadas por um novo serviço de ferramentas que usa APIs do SMO nos bastidores. SMO está disponível no Linux e macOS?

As APIs de SMO ainda não estão disponíveis no Linux ou macOS de uma forma consumível. Podemos portada um subconjunto das APIs do SMO para o .NET Core que precisávamos para o Studio de dados do Azure e estamos planejando expandir como parte do roteiro. O serviço de ferramentas do SQL está no GitHub: [ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>Você planeja o DACFx APIs e/ou sqlpackage.exe e/ou SSDT para Linux e macOS da porta?

Ele está no roteiro de longo prazo. Para ajudar a priorizar, uma sugestão de arquivo no [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>Cmdlets do PowerShell SQL estará disponível no Linux e macOS?

PowerShell do SQL está disponível hoje na Galeria do PowerShell e usá-lo no Windows para trabalhar com o SQL Server em execução em qualquer lugar, incluindo o SQL no Linux. Cmdlets no macOS e Linux oferecendo o SQL PowerShell está em nossos planos. Para ajudar a priorizar, uma sugestão de arquivo no [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="who-usually-uses-azure-data-studio"></a>Quem usa normalmente Studio de dados do Azure?

Os desenvolvedores e DBAs geralmente são os usuários do Studio de dados do Azure.

## <a name="does-azure-data-studio-integrate-with-azure-sql-data-warehouse"></a>Studio de dados do Azure se integram com o Azure SQL Data Warehouse?

Sim. Suporte de Data Studio do Azure SQL Data Warehouse do Azure está atualmente em visualização, junto com o banco de dados de instância gerenciada do SQL e SQL Server 2019 Big Data.

## <a name="why-is-azure-data-studio-important-for-the-new-version-of-sql-server"></a>Por que o estúdio de dados do Azure é importante para a nova versão do SQL Server?

Como o SQL Server estende sua capacidade para o espaço de Big Data, ele precisa de novas ferramentas para apoiar os casos de uso. Por esse motivo, o Studio do Azure Data hoje está enviando uma nova experiência de visualização de suporte para SQL Server Big Data, incluindo a primeira experiência de notebook nunca no conjunto de ferramentas do SQL Server e um novo Assistente de criar tabela externa que faz o acesso a dados do SQL remoto Instâncias de servidor e a Oracle fácil e rápidas.
