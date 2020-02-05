---
title: MSSQLSERVER_10003 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10003 (Database Engine error)
ms.assetid: 9e2cb199-f077-4d88-8117-1b7550afc696
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9061845efbbbf3c20b4d079af2c2b00cfeef1dfd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68068320"
---
# <a name="mssqlserver_10003"></a>MSSQLSERVER_10003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
[Modelos e permissões do SQL Server Profiler](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
[SQL Server Native Client &#40;OLE DB&#41;](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
