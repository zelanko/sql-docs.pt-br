---
title: "Extensões específicas do SQL Server no processo para o ADO.NET | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- data access [CLR integration]
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], in-process extensions
- in-process data access providers [CLR integration]
- extensions [CLR integration]
ms.assetid: 781b812e-eb14-472a-85fa-aa4cdb929bee
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 778957280803b758bbf31775d71a7aca141d8494
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="sql-server-in-process-specific-extensions-to-adonet"></a>Extensões específicas em processo do SQL Server para o ADO.NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Há quatro extensões funcionais principais para o ADO.NET que se destinam especificamente ao uso em processo. Os tópicos a seguir abrangem essas extensões detalhadamente.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Objeto SqlContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
 Esta classe fornece acesso às outras extensões abstraindo o contexto de um chamador de uma rotina do SQL Server que executa código gerenciado em processo.  
  
 [Objeto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)  
 Esta classe contém rotinas para enviar mensagens e resultados tabulares ao cliente.  
  
 [Objeto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)  
 Esta classe fornece informações sobre o contexto no qual um gatilho é executado.  
  
 [Objeto SqlDataRecord](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)  
 A classe SqlDataRecord representa uma única linha de dados, juntamente com seus metadados relacionados, e permite que procedimentos armazenados retornem conjuntos de resultados personalizados ao cliente.  
  
  
