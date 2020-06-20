---
title: MSSQLSERVER_10003 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10003 (Database Engine error)
ms.assetid: 9e2cb199-f077-4d88-8117-1b7550afc696
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2253fc0db73583d3e8f5e5fb97767557ec47d49e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969886"
---
# <a name="mssqlserver_10003"></a>MSSQLSERVER_10003
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10003|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HR_E_OUTOFMEMORY|  
|Texto da mensagem|O provedor ficou sem memória.|  
  
## <a name="explanation"></a>Explicação  
 A pouca memória do sistema fez com que o provedor do OLE DB ficasse sem memória.  
  
## <a name="user-action"></a>Ação do usuário  
 Reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se isso não ajudar, reinicie o computador. Se o problema persistir, colete eventos de rastreamento OLE DB usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e forneça esses dados ao suporte do produto do provedor OLE DB.  
  
## <a name="see-also"></a>Consulte Também  
 [Modelos e permissões do SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
