---
title: Rastreando e reproduzindo eventos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d478fa9203988d043212e4187792d816a69c0402
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62724785"
---
# <a name="tracing-and-replaying-events"></a>Rastreando e reproduzindo eventos
  No SMO, os objetos `Trace` e `Replay` no namespace <xref:Microsoft.SqlServer.Management.Trace> fornecem acesso de programação à funcionalidade [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)], usada para monitorar uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Você pode capturar e salvar dados sobre cada evento em um arquivo ou tabela para análise posterior. Por exemplo, é possível monitorar um ambiente de produção para observar quais procedimentos estão impedindo o desempenho devido à lentidão na execução.  
  
 Os objetos `Trace` e `Replay` fornecem um conjunto de objetos que podem ser usados para criar rastreamentos em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esses objetos podem ser usados de dentro dos seus aplicativos para criar rastreamentos manualmente para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Além disso, os objetos `Trace` de SMO podem ser usados para ler arquivos e tabelas de Rastreamento do SQL que foram criadas monitorando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou o log de DTS.  
  
 Os objetos `Trace` de SMO permitem que você execute estas funções:  
  
-   Criar um rastreamento.  
  
-   Definir os filtros no rastreamento.  
  
-   Definir os eventos que estão sendo localizados.  
  
-   Interromper ou iniciar um rastreamento.  
  
-   Ler arquivos e tabelas de rastreamento.  
  
-   Obter informações sobre eventos em um rastreamento.  
  
-   Obter informações sobre filtros em um rastreamento.  
  
-   Manipular dados de rastreamento programaticamente.  
  
-   Escrever tabelas e arquivos de rastreamento.  
  
-   Reproduzir arquivos ou tabelas de rastreamento.  
  
 Os dados de rastreamento a partir de `Trace` e `Replay` objetos podem ser usados pelo aplicativo de SMO ou podem ser examinado manualmente usando [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md). Os dados de rastreamento também são compatíveis com os procedimentos armazenados [SQL Trace](../../sql-trace/sql-trace.md) que também fornecem capacidades de rastreamento.  
  
 Os objetos de rastreamento SMO residem no namespace <xref:Microsoft.SqlServer.Management.Trace>, que requer uma referência ao arquivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
 Os objetos `Trace` e `Replay` exigem um objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection><xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> para estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> reside no namespace <xref:Microsoft.SqlServer.Management.Common>, que requer uma referência ao arquivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
> [!NOTE]  
>  Os objetos `Trace` e `Replay` não têm suporte em uma plataforma de 64 bits.  
  
  
