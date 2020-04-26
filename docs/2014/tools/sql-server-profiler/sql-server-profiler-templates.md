---
title: Modelos de SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- default SQL Server Profiler templates
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- predefined templates [SQL Server Profiler]
- SQL Server Profiler, templates
ms.assetid: b674e491-dc58-47a1-acdd-7028e9a201fc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5cac924e926d03dffb9116e5ce7194bb784d45fe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68186147"
---
# <a name="sql-server-profiler-templates"></a>Modelos do SQL Server Profiler
  Você pode usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para criar modelos que definem as classes de evento e colunas de dados a serem incluídas em rastreamentos. Depois de definir e salvar o modelo, você pode executar um rastreamento que registre os dados de cada classe de evento selecionada. É possível usar um modelo em muitos rastreamentos; o modelo propriamente dito não é executado.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] oferece modelos de rastreamento predefinidos que permitem configurar facilmente as classes de evento de que, muito provavelmente, você necessitará para rastreamentos específicos. O modelo Standard, por exemplo, ajuda a criar um rastreamento genérico para registrar logons, logoffs, lotes concluídos e informações de conexão. Esse modelo pode ser usado para executar rastreamentos sem modificação ou como ponto de partida para outros modelos com configurações de evento diferentes.  
  
> [!NOTE]  
>  Além de rastreamentos a partir de modelos predefinidos, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] também lhe permite criar rastreamentos de um modelo em branco, que, por padrão, não contêm nenhuma classe de evento. Usar o modelo de rastreamento em branco pode ser útil quando um rastreamento planejado não se assemelha às configurações de nenhum dos modelos predefinidos.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] pode rastrear diversos tipos de servidor. Por exemplo, você pode rastrear [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Porém, as classes de evento que podem ser incluídas não são as mesmas para cada tipo de servidor. Por isso, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] mantém modelos diferentes para servidores diferentes, disponibilizando o modelo específico correspondente ao tipo de servidor selecionado.  
  
## <a name="predefined-templates"></a>Modelos predefinidos  
 Além do modelo Standard (padrão), o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] contém vários modelos predefinidos para monitorar certos tipos de evento. A tabela a seguir lista os modelos predefinidos, suas finalidades e as classes de evento para as quais capturam informações.  
  
|Nome do modelo|Finalidade do modelo|Classes de evento|  
|-------------------|----------------------|-------------------|  
|SP_Counts|Captura o comportamento de execução de procedimentos armazenados no decorrer do tempo.|**SP:Starting**|  
|Standard|Ponto de partida genérico para a criação de um rastreamento. Captura todos os procedimentos armazenados e lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] que são executados. Use para monitorar atividade geral de servidor de banco de dados.|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Completed**<br /><br /> **SQL:BatchCompleted**<br /><br /> **SQL:BatchStarting**|  
|TSQL|Captura todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por clientes e a hora em que foram emitidas. Use para depurar aplicativos cliente.|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SQL:BatchStarting**|  
|TSQL_Duration|Captura todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por clientes e seus tempos de execução (em milissegundos), agrupando-as segundo a duração. Use para identificar consultas lentas.|**RPC:Completed**<br /><br /> **SQL:BatchCompleted**|  
|TSQL_Grouped|Captura todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a hora em que foram emitidas. Agrupa as informações pelo usuário ou cliente que enviou a instrução. Use para investigar consultas de um cliente ou usuário em particular.|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SQL:BatchStarting**|  
|TSQL_Locks|Captura todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por intermédio de clientes juntamente com eventos de bloqueio excepcionais. Use para solucionar problemas com deadlocks, tempo limite de bloqueio e eventos escalonamento de bloqueio.|**Blocked Process Report**<br /><br /> **SP:StmtCompleted**<br /><br /> **SP:StmtStarting**<br /><br /> **SQL:StmtCompleted**<br /><br /> **SQL:StmtStarting**<br /><br /> **Deadlock Graph**<br /><br /> **Lock:Cancel**<br /><br /> **Lock:Deadlock**<br /><br /> **Lock:Deadlock Chain**<br /><br /> **Lock:Escalation**<br /><br /> **Lock:Timeout (timeout>0)**|  
|TSQL_Replay|Captura informações detalhadas sobre as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que serão necessárias se o rastreamento for reproduzido. Use para executar ajuste iterativo, como testes de avaliação de desempenho.|**CursorClose**<br /><br /> **CursorExecute**<br /><br /> **CursorOpen**<br /><br /> **CursorPrepare**<br /><br /> **CursorUnprepare**<br /><br /> **Audit Login**<br /><br /> **Audit Logout**<br /><br /> **Existing Connection**<br /><br /> **RPC Output Parameter**<br /><br /> **RPC:Completed**<br /><br /> **RPC:Starting**<br /><br /> **Exec Prepared SQL**<br /><br /> **Prepare SQL**<br /><br /> **SQL:BatchCompleted**<br /><br /> **SQL:BatchStarting**|  
|TSQL_SPs|Captura informações detalhadas sobre todos os procedimentos armazenados em execução. Use para analisar as etapas de componentes dos procedimentos armazenados. Adicione o evento **SP:Recompile** caso suspeite que esteja havendo recompilação de procedimentos.|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SP:Completed**<br /><br /> **SP:Starting**<br /><br /> **SP:StmtStarting**<br /><br /> **SQL:BatchStarting**|  
|Ajuste|Captura informações sobre procedimentos armazenados e execução [!INCLUDE[tsql](../../includes/tsql-md.md)] em lote. Use para produzir saída de rastreamento que o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] possa utilizar como carga de trabalho para ajustar bancos de dados.|**RPC:Completed**<br /><br /> **SP:StmtCompleted**<br /><br /> **SQL:BatchCompleted**|  
  
 Para obter mais informações sobre classes de evento, veja [Referência de classes de evento do SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
## <a name="default-template"></a>Modelo padrão  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] designa automaticamente o modelo **Standard** como padrão aplicado a novos rastreamentos. Porém, você pode alterar o modelo padrão para qualquer outro modelo predefinido ou definido pelo usuário. Para alterar o modelo padrão, marque a caixa de seleção **Usar como modelo padrão para o tipo de servidor selecionado** ao criar ou editar um modelo, usando a guia **Geral** da caixa de diálogo **Propriedades do Modelo de Rastreamento** .  
  
 Para navegar até a caixa de diálogo **Propriedades do Modelo de Rastreamento**, no menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]Arquivo**do**, escolha **Modelos** e clique em **Novo Modelo** ou em **Editar Modelo**.  
  
> [!NOTE]  
>  O modelo padrão é específico a cada tipo de servidor. Alterar o padrão para um tipo de servidor não influi no modelo padrão de qualquer outro tipo de servidor. Para obter mais informações sobre como definir um modelo padrão para um servidor específico, veja [Definir padrões de definição de rastreamento &#40;SQL Server Profiler&#41;](set-trace-definition-defaults-sql-server-profiler.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um modelo de rastreamento &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)   
 [Modificar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../database-engine/modify-a-trace-template-sql-server-profiler.md)   
 [Exportar um modelo de rastreamento &#40;SQL Server Profiler&#41;](export-a-trace-template-sql-server-profiler.md)   
 [Importar um modelo de rastreamento &#40;SQL Server Profiler&#41;](import-a-trace-template-sql-server-profiler.md)  
  
  
