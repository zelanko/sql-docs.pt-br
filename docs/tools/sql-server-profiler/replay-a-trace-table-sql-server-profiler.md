---
title: Reproduzir uma tabela de rastreamento
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 6a0ad817-3d8d-4495-889d-c66a7ef9e8bb
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 405f8b71730e2758b45c7ddeddf888498d701d20
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307506"
---
# <a name="replay-a-trace-table-sql-server-profiler"></a>Repetir uma tabela de rastreamento (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Repetição é a capacidade de abrir um rastreamento salvo e repeti-lo novamente. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] apresenta um mecanismo de repetição multi-threaded que consegue simular as conexões de usuário e a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A repetição é útil para solucionar problemas de aplicativos ou processos. Ao identificar o problema e implementar correções, execute o rastreamento que encontrou o problema potencial no aplicativo ou processo corrigido. Em seguida, repita o rastreamento original e compare os resultados.  
  
 Além de quaisquer outras classes de evento que desejar monitorar, devem ser capturadas classes de evento específicas para habilitar a repetição. Esses eventos serão capturados por padrão se você usar o modelo de rastreamento **TSQL_Replay** . Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
## <a name="to-replay-a-trace-table"></a>Para repetir uma tabela de rastreamento
  
1.  Abra uma tabela de rastreamento que contenha as classes de evento necessárias para a repetição.  
  
2.  No menu **Repetir** , clique em **Iniciar**e conecte à instância de servidor em que deseja repetir o rastreamento.  
  
3.  Na caixa de diálogo **Configuração de Repetição** , na guia **Opções de Repetição Básicas** , especifique o **Servidor de repetição**. Clique em **Alterar** para alterar o servidor exibido na caixa **Servidor de repetição** .  
  
4.  Opcionalmente, selecione um dos seguintes destinos nos quais salvar a repetição:  
  
    -   **Salvar em arquivo** , que especifica um arquivo no qual salvar a reprodução.  
  
    -   **Salvar em tabela**, que especifica uma tabela de banco de dados na qual salvar a repetição.  
  
5.  Escolha **Reproduzir eventos na oudem em que fouam rastreados**ou **Reproduzir eventos usando vários threads**. A tabela a seguir explica a diferença entre essas configurações.  
  
    |Opção|DESCRIÇÃO|  
    |------------|-----------------|  
    |**Repetir eventos na ordem em que foram rastreados**|Repete os eventos na ordem em que foram registrados. Essa opção habilita a depuração.|  
    |**Reproduzir eventos usando vários threads**|Essa opção usa vários threads para repetir cada evento, não importando a sequência. Essa opção otimiza o desempenho.|  
  
6.  Selecione **Exibir resultados da repetição** para visualizar a repetição enquanto ela ocorre.  
  
7.  Opcionalmente, clique na guia **Opções de Reprodução Avançadas**para especificar as seguintes opções:  
  
    -   Para reproduzir todas as SPIDs (IDs de processo do servidor), selecione **Reproduzir SPIDs do sistema**.  
  
    -   Para limitar a repetição aos processos pertencentes a um SPID específico, selecione **Repetir somente um SPID**. Na caixa **SPID a serem reproduzidas**, digite a SPID.  
  
    -   Para repetir eventos ocorridos durante um intervalo de tempo específico, selecione **Limitar repetição por data e hora**. Selecione uma data e hora para **Hora de início**e **Hora de término**para especificar o intervalo de tempo a incluir na reprodução.  
  
    -   Para controlar como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerencia os processos durante a repetição, configure as **Opções do Health Monitor**.  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)   
 [Repetir rastreamentos](../../tools/sql-server-profiler/replay-traces.md)   
 [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
