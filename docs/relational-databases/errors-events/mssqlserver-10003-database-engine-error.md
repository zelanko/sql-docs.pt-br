---
title: MSSQLSERVER_10003 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10003 (Database Engine error)
ms.assetid: 9e2cb199-f077-4d88-8117-1b7550afc696
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 071285c2f6ea5edfc757448cbcc6ef639ef3428b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10003"></a>MSSQLSERVER_10003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10003|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HR_E_OUTOFMEMORY|  
|Texto da mensagem|O provedor ficou sem memória.|  
  
## <a name="explanation"></a>Explicação  
A pouca memória do sistema fez com que o provedor do OLE DB ficasse sem memória.  
  
## <a name="user-action"></a>Ação do usuário  
Reinicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se isso não ajudar, reinicie o computador. Se o problema persistir, colete eventos de rastreamento OLE DB usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e forneça esses dados ao suporte do produto do provedor OLE DB.  
  
## <a name="see-also"></a>Consulte também  
[Modelos e permissões do SQL Server Profiler](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
[SQL Server Native Client &#40;OLE DB&#41;](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
