---
title: Criar e executar rastreamentos usando procedimentos armazenados de Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: sql-trace
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 80347417-338d-4bea-8885-91fae5181cfe
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2adc911f7eab0fa07e4d227354c0e25e9664bba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-run-traces-using-transact-sql-stored-procedures"></a>Criar e executar rastreamentos usando procedimentos armazenados de Transact-SQL.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O processo de rastrear com o Rastreamento do SQL varia segundo se está criando e executando o rastreamento através do Microsoft [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ou de procedimentos armazenados de sistema.  
  
 Como alternativa ao [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você pode usar procedimentos armazenados de sistema [!INCLUDE[tsql](../../includes/tsql-md.md)] para criar e executar rastreamentos. O processo de rastrear usando procedimentos armazenados de sistema é o seguinte:  
  
1.  Crie um rastreamento usando **sp_trace_create**.  
  
2.  Adicione eventos com **sp_trace_setevent**.  
  
3.  (Opcional) Defina um filtro, com **sp_trace_setfilter**.  
  
4.  Inicie o rastreamento com **sp_trace_setstatus**.  
  
5.  Pare o rastreamento com **sp_trace_setstatus**.  
  
6.  Feche o rastreamento com **sp_trace_setstatus**.  
  
    > [!NOTE]  
    >  Usar procedimentos armazenados do sistema [!INCLUDE[tsql](../../includes/tsql-md.md)] cria um rastreamento no servidor, o que garante que nenhum evento se perca enquanto houver espaço no disco e não ocorrerem erros. Se o disco ficar cheio ou falhar, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] continuará em execução, mas o rastreamento será interrompido. Se **c2 audit mode** estiver definido e houver uma falha de gravação, o rastreamento será interrompido e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será encerrada. Para obter mais informações sobre a configuração **c2 audit mode** , veja [Opção c2 audit mode de configuração de servidor](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Otimizar o Rastreamento do SQL](../../relational-databases/sql-trace/optimize-sql-trace.md)|Contém informações sobre maneiras de reduzir os efeitos do rastreamento sobre o desempenho do sistema.|  
|[Filtrar um rastreamento](../../relational-databases/sql-trace/filter-a-trace.md)|Contém informações sobre como usar filtros em rastreamentos.|  
|[Limitar o tamanho de arquivos e tabelas de rastreamento](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md)|Contém informações sobre como limitar o tamanho dos arquivos e tabelas nos quais são gravados os dados do rastreamento. Observe que só o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] pode gravar informações de rastreamento em tabelas.|  
|[Agendar rastreamentos](../../relational-databases/sql-trace/schedule-traces.md)|Contém informações sobre como definir a hora de início e a hora de término de um rastreamento.|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
