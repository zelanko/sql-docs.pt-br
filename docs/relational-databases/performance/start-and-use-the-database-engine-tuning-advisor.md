---
title: Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.dta.workload.f1
- sql13.dta.general.f1
- sql13.dta.advancedtuningoptions.f1
- sql13.dta.tuningoptions.f1
- sql13.dta.progress.f1
- sql13.dta.options.f1
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], starting
ms.assetid: a4e3226a-3917-4ec8-bdf0-472879d231c9
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 898c59cab6038b7025066906ea74ffd5b9222815
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73983265"
---
# <a name="start-and-use-the-database-engine-tuning-advisor"></a>Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter informações sobre como exibir e trabalhar com os resultados depois que você ajustar um banco de dados, veja [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md).  
  
##  <a name="initialize-the-database-engine-tuning-advisor"></a><a name="Initialize"></a> Inicialize o Orientador de Otimização do Mecanismo de Banco de Dados  
 Ao usá-lo pela primeira vez, um usuário que seja membro da função de servidor fixa **sysadmin** deve inicializar o Orientador de Otimização do Mecanismo de Banco de Dados. Isso acontece porque devem ser criadas vários tabelas do sistema no banco de dados **msdb** para oferecer suporte a operações de ajuste. A inicialização também possibilita que os usuários membros da função de banco de dados fixa **db_owner** ajustem cargas de trabalho em tabelas em seus próprios bancos de dados.  
  
 Um usuário com permissões de administrador do sistema deve executar qualquer um das ações a seguir:  
  
-   Use a interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados para se conectar a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Iniciar o Orientador de Otimização do Mecanismo de Banco de Dados](#Start) posteriormente neste tópico.  
  
-   Use o utilitário **dta** para ajustar a primeira carga de trabalho. Para obter mais informações, consulte [Usar o utilitário dta](#dta) mais adiante neste tópico.  
  
##  <a name="start-the-database-engine-tuning-advisor"></a><a name="Start"></a> Iniciar o Orientador de Otimização do Mecanismo de Banco de Dados  
 Você pode iniciar a GUI (interface gráfica do usuário) do Orientador de Otimização do Mecanismo de Banco de Dados de diversas maneiras diferentes para dar suporte ao ajuste do banco de dados em diversos cenários. As diferentes maneiras de iniciar o Orientador de Otimização do Mecanismo de Banco de Dados incluem: a partir do menu **Iniciar** , a partir do menu **Ferramentas** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e a partir do menu **Ferramentas** no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Ao iniciar o Orientador de Otimização do Mecanismo de Banco de Dados pela primeira vez, o aplicativo exibe uma caixa de diálogo **Conectar ao Servidor** onde você poderá especificar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à qual deseja conecta-se.  
  
> [!WARNING]  
>  Não inicie o Orientador de Otimização do Mecanismo de Banco de Dados quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver executando no modo de usuário único. Se você tentar iniciá-lo enquanto o servidor estiver em modo de usuário único, aparecerá uma mensagem de erro e o Orientador de Otimização do Mecanismo de Banco de Dados não iniciará. Para obter mais informações sobre o modo de usuário único, veja [Iniciar o SQL Server no modo de usuário único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md).  
  
#### <a name="to-start-database-engine-tuning-advisor-from-the-windows-start-menu"></a>Para iniciar o Orientador de Otimização do Mecanismo de Banco de Dados a partir do menu Iniciar do Windows  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**, aponte para **Ferramentas de Desempenho**, e em seguida clique em **Orientador de Otimização do Mecanismo de Banco de Dados**.  
  
#### <a name="to-start-the-database-engine-tuning-advisor-in-sql-server-management-studio"></a>Para iniciar o Orientador de Otimização do Mecanismo de Banco de Dados no SQL Server Management Studio  
  
1.  No menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Ferramentas**, clique em **Orientador de Otimização do Mecanismo de Banco de Dados**.  
  
#### <a name="to-start-the-database-engine-tuning-advisor-from-the-sql-server-management-studio-query-editor"></a>Para iniciar o Orientador de Otimização do Mecanismo de Banco de Dados do Editor de Consultas do SQL Server Management Studio  
  
1.  Abra um arquivo de script do [!INCLUDE[tsql](../../includes/tsql-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, veja [Editores de Consultas e de Texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
2.  Selecione uma consulta no script do [!INCLUDE[tsql](../../includes/tsql-md.md)] ou selecione todo o script, clique com o botão direito do mouse na seleção e escolha **Analisar Consulta no Orientador de Otimização do Mecanismo de Banco de Dados**. A interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados abre e importa o script como uma carga de trabalho de arquivo XML. Você pode especificar um nome de sessão e opções de ajuste para ajustar as consultas selecionadas no [!INCLUDE[tsql](../../includes/tsql-md.md)] como sua carga de trabalho.  
  
#### <a name="to-start-the-database-engine-tuning-advisor-in-sql-server-profiler"></a>Para iniciar o Orientador de Otimização do Mecanismo de Banco de Dados no SQL Server Profiler  
  
1.  No menu **Ferramentas** do SQL Server Profiler, clique em **Orientador de Otimização do Mecanismo de Banco de Dados**.  
  
##  <a name="create-a-workload"></a><a name="Create"></a> Crie uma carga de trabalho  
 A carga de trabalho é um conjunto de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas em um ou mais bancos de dados a serem ajustados. O Orientador de Otimização do Mecanismo de Banco de Dados analisa essas cargas de trabalho para recomendar índices ou estratégias de particionamento que melhorarão o desempenho de consulta de seu servidor.  
  
 Você pode criar uma carga de trabalho usando um dos métodos a seguir.  
  
-   Use o [Repositório de Consultas](../../relational-databases/performance/how-query-store-collects-data.md) como uma carga de trabalho. Fazendo isso, você poderá evitar a criação de uma carga de trabalho manualmente. Para saber mais, veja [Ajustar o Banco de Dados usando cargas de trabalho do Repositório de Consultas](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md).  

      ||  
      |-|  
      |**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  

  
-   Use o cache de planos como uma carga de trabalho. Fazendo isso, você poderá evitar a criação de uma carga de trabalho manualmente. Para obter mais informações, consulte [Ajustar um banco de dados](#Tune) mais adiante neste tópico.  
  
-   Use o Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou seu editor de textos favorito para criar manualmente cargas de trabalho de script [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   Usar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para criar cargas de trabalho de arquivos ou tabelas de rastreamento  
  
    > [!NOTE]  
    >  Quando uma tabela de rastreamento é usada como uma carga de trabalho, ela deve existir no mesmo servidor em que o Orientador de Otimização do Mecanismo de Banco de Dados está ajustando. Se você criou a tabela de rastreamento em um servidor diferente, mova-a para o servidor em que o Orientador de Otimização do Mecanismo de Banco de Dados está ajustando.  
  
-   As cargas de trabalho também podem ser inseridas em um arquivo de entrada XML, no qual você também pode especificar um peso para cada evento. Para obter mais informações sobre como especificar cargas de trabalho inseridas, consulte [Criar um arquivo de entrada XML](#XMLInput) mais adiante neste tópico.  
  
###  <a name="to-create-transact-sql-script-workloads"></a><a name="SSMS"></a> Para criar cargas de trabalho de script do Transact-SQL  
  
1.  Inicie o Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, veja [Editores de Consultas e de Texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
2.  Digite seu script [!INCLUDE[tsql](../../includes/tsql-md.md)] no Editor de Consultas. Este script deve conter um conjunto de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que são executadas no banco ou bancos de dados que você quer ajustar.  
  
3.  Salve o arquivo com uma extensão **.sql** . A interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados e o utilitário de linha de comando **dta** podem usar esse script [!INCLUDE[tsql](../../includes/tsql-md.md)] como carga de trabalho.  
  
###  <a name="to-create-trace-file-and-trace-table-workloads"></a><a name="Profiler"></a> Para criar cargas de trabalho de arquivos e tabelas de rastreamento  
  
1.  Inicie o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] usando um dos seguintes métodos:  
  
    -   No menu **Iniciar** , aponte para **Todos os Programas**, **Microsoft SQL Server**, **Ferramentas de Desempenho**e clique em **SQL Server Profiler**.  
  
    -   No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique no menu **Ferramentas** e em **SQL Server Profiler**.  
  
2.  Crie um arquivo ou tabela de rastreamento, seguindo os procedimentos abaixo, que use o modelo de **Ajuste** do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]:  
  
    -   [Criar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
    -   [Salvar resultados de rastreamento em um arquivo &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
         O Orientador de Otimização do Mecanismo de Banco de Dados pressupõe que o arquivo de rastreamento de carga de trabalho seja um arquivo de substituição. Para obter mais informações sobre arquivos de substituição, consulte [Limit Trace File and Table Sizes](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md).  
  
    -   [Salvar resultados de rastreamento em uma tabela &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
         Verifique se o rastreamento terminou, antes de usar uma tabela de rastreamento como uma carga de trabalho.  
  
 Recomendamos que você use o modelo de Ajuste do SQL Server Profiler para capturar cargas de trabalho para o Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 Se desejar usar seu próprio modelo, verifique se estes eventos de rastreamento foram capturados:  
  
-   **RPC:Completed**  
  
-   **SQL:BatchCompleted**  
  
-   **SP:StmtCompleted**  
  
 Você também pode usar as versões **Iniciais** desses eventos de rastreamento. Por exemplo, **SQL:BatchStarting**. Contudo, as versões **Concluído** desses eventos de rastreamento incluem a coluna **Duração** , que permite que o Orientador de Otimização do Mecanismo de Banco de Dados ajuste a carga de trabalho de maneira mais eficaz. O Orientador de Otimização do Mecanismo de Banco de Dados não ajusta outros tipos de eventos de rastreamento. Para obter mais informações sobre esses eventos de rastreamento, consulte [Stored Procedures Event Category](../../relational-databases/event-classes/stored-procedures-event-category.md) e [TSQL Event Category](../../relational-databases/event-classes/tsql-event-category.md). Para obter informações sobre como usar os procedimentos armazenados do Rastreamento do SQL para criar uma carga de trabalho de arquivo de rastreamento, veja [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
### <a name="trace-file-or-trace-table-workloads-that-contain-the-loginname-data-column"></a>Cargas de trabalho de arquivo ou tabela de rastreamento que contêm a coluna de dados LoginName  
 O Orientador de Otimização do Mecanismo de Banco de Dados submete solicitações ao Plano de execução como parte do processo de ajuste. Quando uma tabela ou arquivo de rastreamento que contém a coluna de dados **LoginName** é consumida como carga de trabalho, o Orientador de Otimização do Mecanismo de Banco de Dados representa o usuário especificado no **LoginName**. Se esse usuário não recebeu a permissão SHOWPLAN, que permite que o usuário execute e crie Planos de execução para as instruções contidas no rastreamento, o Orientador de Otimização do Mecanismo de Banco de Dados não ajustará essas instruções.  
  
##### <a name="to-avoid-granting-the-showplan-permission-to-each-user-specified-in-the-loginname-column-of-the-trace"></a>Para evitar conceder a permissão SHOWPLAN a cada usuário especificado na coluna LoginName do rastreamento  
  
1.  Ajuste a carga de trabalho do arquivo ou tabela de rastreamento. Para obter mais informações, consulte [Ajustar um banco de dados](#Tune) mais adiante neste tópico.  
  
2.  Verifique o log de ajuste de instruções que não foram ajustadas devido a permissões inadequadas. Para obter mais informações, veja [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md).  
  
3.  Crie uma nova carga de trabalho excluindo a coluna **LoginName** dos eventos que não foram ajustados e salve somente os eventos não ajustados em um novo arquivo ou tabela de rastreamento. Para obter mais informações sobre como excluir colunas de dados de um rastreamento, veja [Especificar eventos e colunas de dados para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md) ou [Modificar um rastreamento existente &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md).  
  
4.  Submeta novamente a nova carga de trabalho sem a coluna **LoginName** ao Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 O Orientador de Otimização do Mecanismo de Banco de Dados ajustará a nova carga de trabalho, pois as informações de logon não foram especificadas no rastreamento. Se não houver **LoginName** para uma instrução, o Orientador de Otimização do Mecanismo de Banco de Dados ajustará essa instrução representando o usuário que iniciou a sessão de ajuste (um membro da função de servidor fixa **sysadmin** ou de função de banco de dados fixa **db_owner** ).  
  
##  <a name="tune-a-database"></a><a name="Tune"></a> Ajustar um banco de dados  
 Para ajustar um banco de dados, você pode usar a GUI do Orientador de Otimização do Mecanismo de Banco de Dados ou o utilitário **dta** .  
  
> [!NOTE]  
>  Certifique-se de que o rastreamento tenha parado antes de usar uma tabela de rastreamento como carga de trabalho para o Orientador de Otimização do Mecanismo de Banco de Dados. O Orientador de Otimização do Mecanismo de Banco de Dados não suporta a utilização de uma tabela de rastreamento na qual os eventos de rastreamento ainda estejam sendo gravados como carga de trabalho.  
  
### <a name="use-the-database-engine-tuning-advisor-graphical-user-interface"></a>Use a interface gráfica do usuário do Orientador de Otimização do Mecanismo de Banco de Dados  
 Na GUI (interface gráfica do usuário) do Orientador de Otimização do Mecanismo de Banco de Dados, você pode ajustar um banco de dados usando o cache de planos, arquivos de carga de trabalho ou tabelas de carga de trabalho Você pode usar a GUI do Orientador de Otimização do Mecanismo de Banco de Dados para exibir facilmente os resultados de sua sessão de ajuste atual e os das sessões anteriores. Para obter mais informações sobre as opções da interface do usuário, consulte [Descrições da interface do usuário](#UI) posteriormente neste tópico. Para obter mais informações sobre como trabalhar com a saída depois que você ajustar um banco de dados, veja [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md).  

####  <a name="to-tune-a-database-by-using-the-query-store"></a><a name="PlanCache"></a> Ajustar um banco de dados usando o Repositório de Consultas
Consulte [Ajustar o Banco de Dados Usando Cargas de Trabalho do Repositório de Consulta](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md) para obter mais informações.
  
####  <a name="to-tune-a-database-by-using-the-plan-cache"></a><a name="PlanCache"></a> Para ajustar um banco de dados usando o cache de plano  
  
1.  Inicie o Orientador de Otimização do Mecanismo de Banco de Dados e faça logon em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Iniciar o Orientador de Otimização do Mecanismo de Banco de Dados](#Start) anteriormente neste tópico.  
  
2.  Na guia **Geral** , digite um nome em **Nome da sessão** para criar uma nova sessão de ajuste. Você deve configurar os campos na guia **Geral** antes de iniciar uma sessão de otimização. Não é necessário modificar as configurações da guia **Opções de Ajuste** antes de iniciar uma sessão de ajuste.  
  
3.  Selecione **Cache de Planos** como opção de carga de trabalho. O Orientador de Otimização do Mecanismo de Banco de Dados seleciona os primeiros 1.000 eventos no cache de planos para usar na análise.  
  
4.  Selecione o(s) banco(s) de dados que você deseja ajustar e, se desejar, em **Tabelas Selecionadas**, escolha uma ou mais tabelas de cada banco de dados. Para incluir entradas de cache para todos os bancos de dados, em **Opções de Ajuste**, clique em **Opções Avançadas** e verifique **Incluir eventos de cache de planos de todos os bancos de dados**.  
  
5.  Marque **Salvar log de ajuste** para salvar uma cópia do log de ajuste. Desmarque a caixa de seleção caso não queira salvar uma cópia do log de ajuste.  
  
     Você pode exibir o log de ajuste depois da análise abrindo a sessão e selecionando a guia **Progresso** .  
  
6.  Clique na guia **Opções de Ajuste** e selecione entre as opções listadas.  
  
7.  Clique em **Iniciar Análise**.  
  
     Se quiser parar a sessão de ajuste depois de iniciada, escolha uma das opções a seguir no menu **Ações** :  
  
    -   **Parar Análise (com Recomendações)** interrompe a sessão de ajuste e solicita se você quer que o Orientador de Otimização do Mecanismo de Banco de Dados gere recomendações com base na análise concluída até este ponto.  
  
    -   **Parar Análise** interrompe a sessão de ajuste sem gerar qualquer recomendação.  
  
> [!NOTE]  
>  Não há suporte para pausar o Orientador de Otimização do Mecanismo de Banco de Dados. Se você clicar no botão de barra de ferramentas **Iniciar Análise** depois de clicar no botão **Parar Análise** ou **Parar Análise (com Recomendações)** , o Orientador de Otimização do Mecanismo de Banco de Dados iniciará uma nova sessão de ajuste.  
  
##### <a name="to-tune-a-database-using-a-workload-file-or-table-as-input"></a>Para ajustar um banco de dados usando uma tabela ou arquivo de carga de trabalho como entrada  
  
1.  Determine os recursos de banco de dados (índices, exibições indexadas, particionamento) que o Orientador de Otimização do Mecanismo de Banco de Dados deve considerar para adição, remoção ou retenção durante a análise.  
  
2.  Crie uma carga de trabalho. Para obter mais informações, consulte [Criar uma carga de trabalho](#Create) anteriormente neste tópico.  
  
3.  Inicie o Orientador de Otimização do Mecanismo de Banco de Dados e faça logon em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Iniciar o Orientador de Otimização do Mecanismo de Banco de Dados](#Start) anteriormente neste tópico.  
  
4.  Na guia **Geral** , digite um nome em **Nome da sessão** para criar uma nova sessão de ajuste.  
  
5.  Escolha um **Arquivo de Carga de Trabalho** ou uma **Tabela** e digite o caminho do arquivo ou o nome da tabela na caixa de texto adjacente.  
  
     O formato para especificar uma tabela é  
  
    ```  
  
    database_name.schema_name.table_name  
    ```  
  
     Para procurar uma tabela ou um arquivo de carga de trabalho, clique em **Procurar**. O Orientador de Otimização do Mecanismo de Banco de Dados assume que os arquivos de carga de trabalho são arquivos de substituição. Para obter mais informações sobre arquivos de substituição, consulte [Limit Trace File and Table Sizes](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md).  
  
     Ao usar uma tabela de rastreamento como uma carga de trabalho, essa tabela deve existir no mesmo servidor em que o Orientador de Otimização do Mecanismo de Banco de Dados está ajustando. Se você criar a tabela de rastreamento em um servidor diferente, mova-a para o servidor que o Orientador de Otimização do Mecanismo de Banco de Dados está ajustando antes de usá-la como sua carga de trabalho.  
  
6.  Selecione os bancos de dados e as tabelas em que você deseja executar a carga de trabalho selecionada na etapa 5. Para selecionar as tabelas, clique na seta **Tabelas Selecionadas** .  
  
7.  Marque **Salvar log de ajuste** para salvar uma cópia do log de ajuste. Desmarque a caixa de seleção caso não queira salvar uma cópia do log de ajuste.  
  
     Você pode exibir o log de ajuste depois da análise abrindo a sessão e selecionando a guia **Progresso** .  
  
8.  Clique na guia **Opções de Ajuste** e selecione entre as opções listadas.  
  
9. Clique no botão **Iniciar Análise** na barra de ferramentas.  
  
     Se quiser parar a sessão de ajuste depois de iniciada, escolha uma das opções a seguir no menu **Ações** :  
  
    -   **Parar Análise (com Recomendações)** interrompe a sessão de ajuste e solicita se você quer que o Orientador de Otimização do Mecanismo de Banco de Dados gere recomendações com base na análise concluída até este ponto.  
  
    -   **Parar Análise** interrompe a sessão de ajuste sem gerar qualquer recomendação.  
  
> [!NOTE]  
>  Não há suporte para pausar o Orientador de Otimização do Mecanismo de Banco de Dados. Se você clicar no botão de barra de ferramentas **Iniciar Análise** depois de clicar no botão **Parar Análise** ou **Parar Análise (com Recomendações)** , o Orientador de Otimização do Mecanismo de Banco de Dados iniciará uma nova sessão de ajuste.  
  
###  <a name="use-the-dta-utility"></a><a name="dta"></a> Usar o utilitário dta  
 O utilitário [dta utility](../../tools/dta/dta-utility.md) fornece um arquivo executável de prompt de comando que pode ser usado para ajustar bancos de dados. Ele permite usar a funcionalidade do Orientador de Otimização do Mecanismo de Banco de Dados em scripts e arquivos em lote. O utilitário **dta** assume entradas de cache de plano, arquivos de rastreamento, tabelas de rastreamento e scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] como cargas de trabalho. Ele ainda aceita entrada XML compatível com o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados, que está disponível no [Microsoft Web site](https://go.microsoft.com/fwlink/?linkid=43100).  
  
 Antes de começar a ajustar uma carga de trabalho com o utilitário **dta** , considere o seguinte:  
  
-   Ao usar uma tabela de rastreamento como uma carga de trabalho, essa tabela deve existir no mesmo servidor em que o Orientador de Otimização do Mecanismo de Banco de Dados está ajustando. Se você criar a tabela de rastreamento em um servidor diferente, mova-a para o servidor em que o Orientador de Otimização do Mecanismo de Banco de Dados está fazendo o ajuste.  
  
-   Certifique-se de que o rastreamento tenha parado antes de usar uma tabela de rastreamento como carga de trabalho para o Orientador de Otimização do Mecanismo de Banco de Dados. O Orientador de Otimização do Mecanismo de Banco de Dados não suporta a utilização de uma tabela de rastreamento na qual os eventos de rastreamento ainda estejam sendo gravados como carga de trabalho.  
  
-   Se uma sessão de ajuste continuar em execução por mais tempo que o esperado, pressione CTRL+C para parar a sessão de ajuste e gerar recomendações baseadas na análise do que o **dta** completou até esse ponto. Você será solicitado a indicar se deseja ou não gerar recomendações. Pressione CTRL+C novamente para parar a sessão de ajuste sem gerar recomendações.  
  
 Para obter mais informações sobre sintaxe e exemplos do utilitário **dta** , consulte [dta Utility](../../tools/dta/dta-utility.md).  
  
##### <a name="to-tune-a-database-by-using-the-plan-cache"></a>Para ajustar um banco de dados usando o cache de plano  
  
1.  Especifique a opção **-ip** . Os primeiros 1.000 eventos de cache de plano para bancos de dados selecionados são analisados.  
  
     Em um prompt de comando, digite o seguinte:  
  
    ```  
    dta -E -D DatabaseName -ip -s SessionName  
    ```  
  
2.  Para modificar o número de eventos a serem usados para análise, especifique a opção **-n**. O exemplo a seguir aumenta o número de entradas de cache para 2.000.  
  
    ```  
    dta -E -D DatabaseName -ip -n 2000-s SessionName1  
    ```  
  
3.  Para analisar eventos para todos os bancos de dados na instância, especifique a opção **-ipf** .  
  
    ```  
    dta -E -D DatabaseName -ip -ipf -n 2000 -s SessionName2  
    ```  
  
##### <a name="to-tune-a-database-by-using-a-workload-and-dta-utility-default-settings"></a>Para ajustar um banco de dados usando uma carga de trabalho e configurações padrão do utilitário dta  
  
1.  Determine os recursos de banco de dados (índices, exibições indexadas, particionamento) que o Orientador de Otimização do Mecanismo de Banco de Dados deve considerar para adição, remoção ou retenção durante a análise.  
  
2.  Crie uma carga de trabalho. Para obter mais informações, consulte [Criar uma carga de trabalho](#Create) anteriormente neste tópico.  
  
3.  Em um prompt de comando, digite o seguinte:  
  
    ```  
    dta -E -D DatabaseName -if WorkloadFile -s SessionName  
    ```  
  
     em que `-E` especifica que sua sessão de ajuste usa uma conexão confiável (em vez de ID e senha de logon), `-D` especifica o nome do banco de dados que você quer ajustar. Por padrão, o utilitário conecta a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador local. (Use a opção `-S` para especificar um banco de dados remoto, como mostrado no procedimento a seguir, ou para especificar uma instância nomeada.) A opção `-if` especifica o nome e o caminho de um arquivo de carga de trabalho (que pode ser um script [!INCLUDE[tsql](../../includes/tsql-md.md)] ou um arquivo de rastreamento), e `-s` especifica um nome para a sua sessão de ajuste.  
  
     As quatro opções mostradas aqui (nome de banco de dados, carga de trabalho, tipo de conexão e nome de sessão) são obrigatórias.  
  
##### <a name="to-tune-a-remote-database-or-a-named-instance-for-a-specific-duration"></a>Para ajustar um banco de dados remoto ou uma instância nomeada para uma duração específica  
  
1.  Determine os recursos de banco de dados (índices, exibições indexadas, particionamento) que o Orientador de Otimização do Mecanismo de Banco de Dados deve considerar para adição, remoção ou retenção durante a análise.  
  
2.  Crie uma carga de trabalho. Para obter mais informações, consulte [Criar uma carga de trabalho](#Create) anteriormente neste tópico.  
  
3.  Em um prompt de comando, digite o seguinte:  
  
    ```  
    dta -S ServerName\Instance -D DatabaseName -it WorkloadTableName   
    -U LoginID -P Password -s SessionName -A TuningTimeInMinutes  
    ```  
  
     em que `-S` especifica uma instância e um nome de servidor remoto (ou uma instância nomeada no servidor local), e `-D` especifica o nome do banco de dados que você deseja ajustar. A opção `-it` especifica o nome da tabela de carga de trabalho, `-U` e `-P` especificam a ID e a senha de logon para o banco de dados remoto, `-s` especifica o nome da sessão de ajuste e `-A` especifica a duração da sessão de ajuste em minutos. Por padrão, o utilitário **dta** usa uma duração de ajuste de 8 horas. Se quiser que o Orientador de Otimização do Mecanismo de Banco de Dados ajuste uma carga de trabalho por tempo ilimitado, especifique **0** (zero) na opção `-A` .  
  
##### <a name="to-tune-a-database-using-an-xml-input-file"></a>Para ajustar um banco de dados que usa um arquivo de entrada XML  
  
1.  Determine os recursos de banco de dados (índices, exibições indexadas, particionamento) que o Orientador de Otimização do Mecanismo de Banco de Dados deve considerar para adição, remoção ou retenção durante a análise.  
  
2.  Crie uma carga de trabalho. Para obter mais informações, consulte [Criar uma carga de trabalho](#Create) anteriormente neste tópico.  
  
3.  Crie um arquivo de entrada XML. Para obter mais informações, consulte [Criar arquivos de entrada XML](#XMLInput) , posteriormente neste tópico.  
  
4.  Em um prompt de comando, digite o seguinte:  
  
    ```  
    dta -E -S ServerName\Instance -s SessionName -ix PathToXMLInputFile  
    ```  
  
     em que `-E` especifica uma conexão confiável, `-S` especifica uma instância e servidor remoto, ou uma instância nomeada no servidor local, `-s` especifica o nome da sessão de ajuste e `-ix` especifica o arquivo de entrada XML a ser usado pela sessão de ajuste.  
  
5.  Depois que o utilitário terminar de ajustar a carga de trabalho, você pode exibir os resultados das sessões de ajuste com a GUI do Orientador de Otimização do Mecanismo de Banco de Dados. Como alternativa, também é possível especificar que as recomendações de ajuste sejam gravadas em um arquivo XML na opção **-ox** . Para obter mais informações, consulte [dta Utility](../../tools/dta/dta-utility.md).  
  
##  <a name="create-an-xml-input-file"></a><a name="XMLInput"></a> Criar um arquivo de entrada XML  
 Se você for um desenvolvedor de XML experiente, poderá criar arquivos formatados em XML que podem ser usados pelo Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para ajustar cargas de trabalho. Para criar estes arquivos XML, use suas ferramentas de XML favoritas para editar um arquivo de exemplo ou gerar uma instância do esquema XML do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 O esquema XML do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está disponível na instalação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na seguinte localização:  
  
 C:\Arquivos de Programas\Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd  
  
 O esquema XML do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] também está disponível online neste [site da Microsoft](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
 Esse URL abre uma página em que estão disponíveis vários esquemas XML do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Role a página para baixo até atingir a linha do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
#### <a name="to-create-an-xml-input-file-to-tune-workloads"></a>Para criar um arquivo de entrada XML para ajustar cargas de trabalho  
  
1.  Crie uma carga de trabalho. Você pode usar um arquivo ou tabela de rastreamento usando o modelo de ajuste no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]ou criar um script [!INCLUDE[tsql](../../includes/tsql-md.md)] que reproduza uma carga de trabalho representativa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Criar uma carga de trabalho](#Create) anteriormente neste tópico.  
  
2.  Crie um arquivo de entrada XML por meio de um dos seguintes métodos:  
  
    -   Copie e cole uma das [Amostras de arquivos de entrada XML &#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md) em seu editor XML favorito. Altere os valores para especificar os argumentos corretos para sua instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e salve o arquivo XML.  
  
    -   Usando sua ferramenta XML favorita, gere uma instância a partir do esquema XML do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
3.  Depois de criar o arquivo de entrada XML, use-o como entrada para o utilitário de linha de comando **dta** para ajustar a carga de trabalho. Para obter informações sobre como usar arquivos de entrada de XML com este utilitário, consulte a seção [Usar o utilitário dta](#dta) anteriormente neste tópico.  
  
> [!NOTE]  
>  Se quiser usar uma carga de trabalho embutida, que é uma carga de trabalho especificada diretamente no arquivo de entrada XML, use a [Amostra do arquivo de entrada XML com carga de trabalho embutida &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
##  <a name="user-interface-descriptions"></a><a name="UI"></a> Descrições da interface do usuário  
  
### <a name="tools-menuoptions-page"></a>Página de Menu/Opções de Ferramentas  
 Use essa caixa de diálogo para especificar parâmetros de configuração gerais para o Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 **Na inicialização**  
 Especifica o que Orientador de Otimização do Mecanismo de Banco de Dados deve fazer ao ser iniciado: abrir sem uma conexão de banco de dados, exibir uma caixa de diálogo **Nova Conexão** , exibir uma sessão nova ou carregar a última sessão carregada.  
  
 **Alterar fonte**  
 Especifica a fonte de monitor usada pelas tabelas do Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 **Número de itens em listas usadas mais recentemente**  
 Especifica o número de sessões ou arquivos a serem exibidos em **Sessões Recentes** ou **Arquivos Recentes** no menu **Arquivo** .  
  
 **Lembrar minhas últimas opções de ajuste**  
 Retém opções de ajuste entre sessões. Selecionadas por padrão. Desmarque essa caixa de seleção para iniciar sempre com os padrões do Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 **Perguntar antes de excluir sessões permanentemente**  
 Exibe uma caixa de diálogo de confirmação antes de excluir sessões.  
  
 **Perguntar antes de parar a análise da sessão**  
 Exibe uma caixa de diálogo de confirmação antes de parar a análise de uma carga de trabalho.  
  
#### <a name="general-tab-options"></a>Opções da guia Geral  
 Você deve configurar os campos na guia **Geral** antes de iniciar uma sessão de otimização. Você não precisa modificar as configurações da guia **Opções de Ajuste** antes de iniciar uma sessão de ajuste.  
  
 **Nome da sessão**  
 Especifique um nome para a sessão. O nome de sessão associa um nome a uma sessão de otimização. Você pode consultar esse nome para revisar a sessão de otimização posteriormente.  
  
 **Arquivo**  
 Especifique um script .sql ou arquivo de rastreamento para uma carga de trabalho. Especifique o caminho e o nome de arquivo na caixa de texto associada. O Orientador de Otimização do Mecanismo de Banco de Dados pressupõe que o arquivo de rastreamento de carga de trabalho seja um arquivo de substituição. Para obter mais informações sobre arquivos de substituição, consulte [Limit Trace File and Table Sizes](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md).  
  
 **Table**  
 Especifique uma tabela de rastreamento para uma carga de trabalho. Especifique o nome totalmente qualificado da tabela de rastreamento na caixa de texto associada, como a seguir:  
  
```  
database_name.owner_name.table_name  
```  
  
-   Verifique se o rastreamento terminou, antes de usar uma tabela de rastreamento como uma carga de trabalho.  
  
-   A tabela de rastreamento deve existir no mesmo servidor em que o Orientador de Otimização do Mecanismo de Banco de Dados está otimizando. Se você criar a tabela de rastreamento em um servidor diferente, mova-a para o servidor em que o Orientador de Otimização do Mecanismo de Banco de Dados está fazendo o ajuste.  
  
 **Cache de Planos**  
 Especifique o cache de planos como uma carga de trabalho. Fazendo isso, você poderá evitar a criação de uma carga de trabalho manualmente. O Orientador de Otimização do Mecanismo de Banco de Dados seleciona os primeiros 1.000 eventos a serem usados para análise.  
  
 **Xml**  
 Só será exibido se você importar uma consulta de carga de trabalho do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Para importar uma consulta de carga de trabalho do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
1.  Digite uma consulta no Editor de Consultas e realce-a.  
  
2.  Clique com o botão direito do mouse na consulta realçada e clique em **Analisar Consulta no Orientador de Otimização do Mecanismo de Banco de Dados**.  
  
 **Procurar uma carga de trabalho [arquivo ou tabela]**  
 Quando **Arquivo** ou **Tabela** for selecionado como fonte de carga de trabalho, use esse botão Procurar para selecionar o destino.  
  
 **Visualizar a carga de trabalho XML**  
 Exiba uma carga de trabalho formatada em XML importada do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Banco de dados para análise de carga de trabalho**  
 Especifique o primeiro banco de dados ao qual se conecta o Orientador de Otimização do Mecanismo de Banco de Dados quando ajusta uma carga de trabalho. Depois que a otimização começa, o Orientador de Otimização do Mecanismo de Banco de Dados se conecta aos bancos de dados especificados pelas instruções `USE DATABASE` contidas na carga de trabalho.  
  
 **Selecionar bancos de dados e tabelas a otimizar**  
 Especifique os bancos de dados e tabelas a serem otimizados. Para especificar todos os bancos de dados, marque a caixa de seleção no cabeçalho da coluna **Nome** . Para especificar alguns bancos de dados, marque a caixa de seleção ao lado do nome do banco de dados. Por padrão, todas as tabelas dos bancos de dados selecionados são automaticamente incluídas na sessão de ajuste. Para excluir tabelas, clique na seta na coluna **Tabelas Selecionadas** e desmarque as caixas de seleção ao lado das tabelas que não desejar ajustar.  
  
 Seta para baixo das**Tabelas Selecionadas**  
 Expanda a lista de tabelas para permitir a seleção de tabelas individuais para ajuste.  
  
 **Salvar log de ajuste**  
 Crie um log e registre erros durante a sessão.  
  
> [!NOTE]  
>  O Orientador de Otimização do Mecanismo de Banco de Dados não atualiza automaticamente as informações das linhas das tabelas exibidas na guia **Geral** . Em vez disso, ele se baseia nos metadados do banco de dados. Se você suspeitar que as informações das linhas estão desatualizadas, execute o comando DBCC UPDATEUSAGE para os objetos relevantes.  
  
##### <a name="tuning-tab-options"></a>Opções da guia Ajuste  
 Use a guia **Opções de Ajuste** para modificar configurações padrão de opções de ajuste gerais. Você não precisa modificar as configurações da guia **Opções de Ajuste** antes de iniciar uma sessão de ajuste.  
  
 **Limitar tempo de ajuste**  
 Limita o tempo para a sessão de ajuste atual. Fornecer mais tempo para o ajuste melhora a qualidade das recomendações. Para garantir as melhores recomendações, não selecione essa opção.  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)] consome recursos do sistema durante a análise. Use **Limitar tempo de ajuste** para parar o ajuste antes de períodos de carga de trabalho pesada antecipada no servidor que está sendo ajustado.  
  
 **Opções Avançadas**  
 Use a caixa de diálogo **Opções de Ajuste Avançado** para configurar o espaço de máximo, o máximo de colunas de chave e recomendações de índice online.  
  
 **Definir espaço máximo para recomendações (MB)**  
 Digite o valor do espaço máximo a ser usado pelas estruturas de design físico recomendadas pelo Orientador de Otimização do Mecanismo de Banco de Dados.  
  
 Se nenhum valor for digitado, o Orientador de Otimização do Mecanismo de Banco de Dados assumirá o menor dos seguintes limites de espaço:  
  
-   Três vezes o tamanho de dados brutos atuais, o que inclui o tamanho total de heaps e índices cluster em tabelas no banco de dados.  
  
-   Os espaços livres em todas as unidades de disco anexas mais o tamanho dos dados brutos.  
  
 **Incluir eventos de cache de planos de todos os bancos de dados**  
 Especifique que são analisados eventos de cache de plano de todos os bancos de dados.  
  
 **Máximo de colunas por índice**  
 Especifica o número máximo de colunas para incluir em qualquer índice. O padrão é 1023.  
  
 **Todas as recomendações são offline**  
 Gera as melhores recomendações possíveis, mas não recomenda que qualquer estrutura de design físico seja criada online.  
  
 **Gerar recomendações online quando possível**  
 Ao criar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para implementar as recomendações, escolha métodos que possam ser implementados com o servidor online, mesmo se um método offline mais rápido estiver disponível.  
  
 **Gerar apenas recomendações online**  
 Só faça recomendações que permitam que o servidor permaneça online.  
  
 **Pare em**  
 Forneça a data e hora em que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve parar.  
  
 **Índices e exibições indexadas**  
 Marque essa caixa para incluir recomendações para somar índices clusterizados, índices não clusterizados e exibições indexadas.  
  
 **Exibições indexadas**  
 Inclua apenas recomendações para adicionar exibições indexadas. Índices clusterizados e não clusterizados  não serão recomendados.  
  
 **Incluir índices filtrados**  
 Inclua recomendações para adicionar índices filtrados. Essa opção estará disponível se você selecionar uma destas estruturas de design físico: **índices e exibições indexadas**, **índices** ou **índices não clusterizados**.  
  
 **Índices**  
 Inclua apenas recomendações para adicionar índices clusterizados e não clusterizados. Não serão recomendadas exibições indexadas.  
  
 **Índices não clusterizados**  
 Inclua recomendações só para índices não clusterizados. Índices clusterizados e exibições indexadas não serão recomendados.  
  
 **Avaliar a utilização apenas dos PDS existentes**  
 Avalie a efetividade dos índices atuais mas não recomende índices adicionais nem exibições indexadas.  
  
 **Nenhum particionamento**  
 Não recomende particionamento.  
  
 **Particionamento completo**  
 Inclua recomendações para particionamento.  
  
 **Particionamento alinhado**  
 As novas partições recomendadas serão alinhadas para facilitar a manutenção das partições.  
  
 **Não manter nenhuma PDS existente**  
 Recomende descartar índices, exibições e particionamentos existentes desnecessários. Se uma PDS (estrutura de design física) existente for útil para a carga de trabalho, o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não recomendará o seu descarte.  
  
 **Manter apenas índices**  
 Mantenha todos os índices existentes mas recomende descartar exibições indexadas e particionamentos desnecessários.  
  
 **Manter todas as PDS existentes**  
 Mantenha todos os índices, exibições indexadas e particionamentos existentes.  
  
 **Manter apenas índices cluster**  
 Mantenha todos os índices clusterizados existentes mas recomende descartar exibições indexadas, partições e índices não clusterizados desnecessários.  
  
 **Manter particionamento alinhado**  
 Mantenha estruturas de particionamento que estão atualmente alinhadas, mas recomende descartar exibições indexadas, índices e particionamento desalinhado desnecessários. Todo particionamento adicional recomendado será alinhado com o esquema de particionamento atual.  
  
###### <a name="progress-tab-options"></a>Opções da guia Progresso  
 A guia **Progresso** do Orientador de Otimização do Mecanismo de Banco de Dados aparece depois que o Orientador de Otimização do Mecanismo de Banco de Dados começar a analisar uma carga de trabalho.  
  
 Se quiser parar a sessão de ajuste depois de iniciada, escolha uma das opções a seguir no menu **Ações** :  
  
-   **Parar Análise (com Recomendações)** interrompe a sessão de ajuste e solicita se você quer que o Orientador de Otimização do Mecanismo de Banco de Dados gere recomendações com base na análise concluída até este ponto.  
  
-   **Parar Análise** interrompe a sessão de ajuste sem gerar qualquer recomendação.  
  
 **Progresso do Ajuste**  
 Indica o status atual do progresso. Contém o número de ações executadas e o número de mensagens de erro, de sucesso e de advertência recebidas.  
  
 **Detalhes**  
 Contém um ícone que indica o status.  
  
 **Ação**  
 Exibe as etapas que estão sendo executadas.  
  
 **Status**  
 Exibe o status da etapa de ação.  
  
 **Mensagem**  
 Contém mensagem retornada pelas etapas de ação.  
  
 **Log de Ajuste**  
 Contém informações relativas a esta sessão de ajuste. Para imprimir esse log, clique com o botão direito do mouse no log e clique em **Imprimir**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [Utilitário dta](../../tools/dta/dta-utility.md)  
  
  
