---
title: Criar e executar rastreamentos usando procedimentos armazenados de Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80347417-338d-4bea-8885-91fae5181cfe
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7922638ed06f52740a3c34f6e66ff72dbb5bbd98
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62714803"
---
# <a name="create-and-run-traces-using-transact-sql-stored-procedures"></a>Criar e executar rastreamentos usando procedimentos armazenados de Transact-SQL.
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
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Otimizar o rastreamento do SQL](sql-trace.md)|Contém informações sobre maneiras de reduzir os efeitos do rastreamento sobre o desempenho do sistema.|  
|[Filtrar um rastreamento](filter-a-trace.md)|Contém informações sobre como usar filtros em rastreamentos.|  
|[Limitar o tamanho de arquivos e tabelas do rastreamento](limit-trace-file-and-table-sizes.md)|Contém informações sobre como limitar o tamanho dos arquivos e tabelas nos quais são gravados os dados do rastreamento. Observe que só o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] pode gravar informações de rastreamento em tabelas.|  
|[Agendar rastreamentos](schedule-traces.md)|Contém informações sobre como definir a hora de início e a hora de término de um rastreamento.|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)  
  
  
