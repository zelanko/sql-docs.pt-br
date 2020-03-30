---
title: Repetir rastreamentos
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: da958d3c-7f3e-44c9-aecc-8a9493bea7c0
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 50ef296f7ce7198dc0e233aca08e33c5f1cf7af0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307468"
---
# <a name="replay-traces"></a>Repetir rastreamentos

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Reprodução é a capacidade para reproduzir a atividade que foi capturada em um rastreamento. Ao criar ou editar um rastreamento, você pode salvá-lo em um arquivo para reproduzi-lo posteriormente. Você pode usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para reproduzir a atividade de rastreamento de um único computador. Para cargas de trabalho grandes, use o Distributed Replay Utility para reproduzir dados de rastreamento de vários computadores.  
  
 Esta seção descreve como usar os recursos de reprodução do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Para obter mais informações sobre o Distributed Replay Utility, consulte [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] apresenta um mecanismo de repetição multi-threaded que consegue simular as conexões de usuário e a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A repetição é útil para solucionar problemas de aplicativos ou processos. Tendo identificado o problema e implementado correções, execute o rastreamento que encontrou o problema potencial contra o aplicativo ou processo corrigido. Em seguida, repita o rastreamento original e compare os resultados.  
  
 A repetição de rastreamentos é compatível com a depuração por meio das opções **Alternar Ponto de Interrupção** e **Executar até o Cursor** do menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Reproduzir** menu. Essas opções melhoram, em especial, a análise de scripts longos, pois elas podem dividir a repetição do rastreamento em segmentos curtos que podem ser analisados incrementalmente.  
  
 Para obter informações sobre as permissões necessárias para reproduzir rastreamentos, consulte [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Requisitos para reprodução](../../tools/sql-server-profiler/replay-requirements.md)|Descreve os eventos que devem ser incluídos na definição de um rastreamento para que ele possa ser reproduzido com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Opções de repetição &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-options-sql-server-profiler.md)|Descreve as opções que podem ser definidas na caixa de diálogo **Configuração de Reprodução** do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Considerações para reproduzir rastreamentos &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/considerations-for-replaying-traces-sql-server-profiler.md)|Descreve os eventos de rastreamento que não podem ser reproduzidos com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e os efeitos da reprodução de rastreamentos no desempenho do servidor.|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
