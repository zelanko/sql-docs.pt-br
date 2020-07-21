---
title: MSSQLSERVER_10001 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10001 (Database Engine error)
ms.assetid: f8fd2d8d-a4af-4b6a-ba51-9123b7e4c9bf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9fe3b41642150d7fe6587e6747d2a2c72ab26700
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554201"
---
# <a name="mssqlserver_10001"></a>MSSQLSERVER_10001
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10001|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HR_E_UNEXPECTED|  
|Texto da mensagem|O provedor reportou uma falha catastrófica inesperada.|  
  
## <a name="explanation"></a>Explicação  
 O processamento de consulta distribuído encontrou um erro genérico ao chamar no provedor OLE DB.  
  
## <a name="user-action"></a>Ação do usuário  
 Colete eventos de rastreamento OLE DB usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e forneça esses dados ao suporte ao produto do provedor OLE DB.  
  
## <a name="see-also"></a>Consulte Também  
 [Modelos e permissões do SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
