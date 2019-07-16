---
title: Iniciar um rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1c53c039d6194edbc37438ef30ac4fef0113ae87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211033"
---
# <a name="start-a-trace"></a>Iniciar um rastreamento
  Após definir um novo rastreamento ou criar um modelo usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você pode iniciar, pausar ou interromper a captura de dados usando a nova definição ou modelo de rastreamento.  
  
## <a name="starting-a-trace"></a>Iniciando um rastreamento  
 Quando se inicia um rastreamento e a origem definida é uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ou do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria uma fila que fornece um local de guarda temporária para os eventos de servidor capturados.  
  
 Quando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] é utilizado para acessar o Rastreamento do SQL, uma nova janela de rastreamento é aberta (se já não houver uma) quando o rastreamento é iniciado e os dados são capturados imediatamente.  
  
 Quando se usam procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] do sistema para acessar o Rastreamento do SQL, é necessário iniciar um rastreamento toda vez que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada para a captura de dados. Depois que um rastreamento é iniciado, só é possível modificar seu nome.  
  
> [!NOTE]  
>  Ao trabalhar com rastreamentos existentes, você pode exibir as propriedades, mas não pode modificá-las. Para modificar as propriedades, interrompa ou pause o rastreamento.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar um rastreamento automaticamente após a conexão com um servidor &#40;SQL Server Profiler&#41;](start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [Pausar um rastreamento &#40;SQL Server Profiler&#41;](pause-a-trace-sql-server-profiler.md)   
 [Parar um rastreamento &#40;SQL Server Profiler&#41;](stop-a-trace-sql-server-profiler.md)   
 [Limpar uma janela de rastreamento &#40;SQL Server Profiler&#41;](clear-a-trace-window-sql-server-profiler.md)   
 [Executar um rastreamento que foi pausado ou interrompido &#40;SQL Server Profiler&#41;](run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
  
