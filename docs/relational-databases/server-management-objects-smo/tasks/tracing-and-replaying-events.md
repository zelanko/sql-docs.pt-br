---
title: Rastreando e reproduzindo eventos | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
caps.latest.revision: "21"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a5501861717bf21e6004730b38f93b309c40e0e
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2018
---
# <a name="tracing-and-replaying-events"></a>Rastreando e reproduzindo eventos
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  No SMO, o **rastreamento** e **Replay** objetos no <xref:Microsoft.SqlServer.Management.Trace> namespace fornece acesso programático para o [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] funcionalidade, que é usada para monitorar uma instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ou [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Você pode capturar e salvar dados sobre cada evento em um arquivo ou tabela para análise posterior. Por exemplo, é possível monitorar um ambiente de produção para observar quais procedimentos estão impedindo o desempenho devido à lentidão na execução.  
  
 O **rastreamento** e **Replay** objetos fornecem um conjunto de objetos que podem ser usados para criar rastreamentos em uma instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esses objetos podem ser usados de dentro dos seus aplicativos para criar rastreamentos manualmente para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Além disso, o SMO **rastreamento** objetos podem ser usados para ler arquivos de rastreamento do SQL e tabelas que foram criadas monitorando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], ou o log de DTS.  
  
 Os objetos **Trace** de SMO permitem que você execute estas funções:  
  
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
  
 Os dados de rastreamento do **rastreamento** e **Replay** objetos podem ser usados pelo aplicativo de SMO ou podem ser examinado manualmente usando [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md). Os dados de rastreamento também são compatíveis com o [SQL Trace](../../../relational-databases/sql-trace/sql-trace.md) procedimentos armazenados que também fornecem capacidades de rastreamento.  
  
 Os objetos de rastreamento SMO residem no namespace <xref:Microsoft.SqlServer.Management.Trace>, que requer uma referência ao arquivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
 O **rastreamento** e **Replay** objetos requerem um [ServerConnection](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> objeto para estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O [ServerConnection](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common.serverconnection.aspx) objeto reside no [Microsoft.SqlServer.Management.Common](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common) namespace, o que requer uma referência ao arquivo Microsoft.SQLServer.ConnectionInfo.dll.  
  
> [!NOTE]  
>  Os objetos **Trace** e **Replay** não têm suporte em uma plataforma de 64 bits.  
  
  
