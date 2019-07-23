---
title: Iniciar um rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, stopping traces
- pausing traces
- Profiler [SQL Server Profiler], stopping traces
- Profiler [SQL Server Profiler], starting traces
- traces [SQL Server], starting
- SQL Server Profiler, pausing traces
- traces [SQL Server], stopping
- Profiler [SQL Server Profiler], pausing traces
- traces [SQL Server], pausing
- SQL Server Profiler, starting traces
- stopping traces
- starting traces
ms.assetid: aeeb38eb-229a-4c8b-ad66-57e9ce45fb6a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 40526c910ad10dd280f7eb304abe4db518f8c530
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059649"
---
# <a name="start-a-trace"></a>Iniciar um rastreamento
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Após definir um novo rastreamento ou criar um modelo usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você pode iniciar, pausar ou interromper a captura de dados usando a nova definição ou modelo de rastreamento.  
  
## <a name="starting-a-trace"></a>Iniciando um rastreamento  
 Quando se inicia um rastreamento e a origem definida é uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ou do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria uma fila que fornece um local de guarda temporária para os eventos de servidor capturados.  
  
 Quando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] é utilizado para acessar o Rastreamento do SQL, uma nova janela de rastreamento é aberta (se já não houver uma) quando o rastreamento é iniciado e os dados são capturados imediatamente.  
  
 Quando se usam procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] do sistema para acessar o Rastreamento do SQL, é necessário iniciar um rastreamento toda vez que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada para a captura de dados. Depois que um rastreamento é iniciado, só é possível modificar seu nome.  
  
> [!NOTE]  
>  Ao trabalhar com rastreamentos existentes, você pode exibir as propriedades, mas não pode modificá-las. Para modificar as propriedades, interrompa ou pause o rastreamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar um rastreamento automaticamente após a conexão com um servidor &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [Pausar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)   
 [Parar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)   
 [Limpar uma janela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)   
 [Executar um rastreamento que foi pausado ou interrompido &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
  
