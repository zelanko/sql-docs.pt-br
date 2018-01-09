---
title: Resultados de mensagem do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-errors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be4cde80aa97b0216c9879c892fc1bc4a54cfe1a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sql-server-message-results"></a>Resultados de mensagem do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções não geram [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor OLE DB Native Client ou uma contagem de linhas afetadas quando executadas:  
  
-   PRINT  
  
-   RAISERROR com uma severidade de 10 ou menor  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instruções retornam uma ou mais mensagens informativas ou fazem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornar mensagens informativas em vez de resultados de contagens ou conjuntos de linhas. Na execução bem sucedida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client Retorna S_OK e as mensagens estão disponíveis para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB Native Client.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client Retorna S_OK e tem uma ou mais mensagens informativas disponíveis após a execução de várias [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções ou a execução do consumidor de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro do provedor OLE DB Native Client.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB Native Client que permite a especificação dinâmica do texto da consulta deve verificar as interfaces de erro após cada execução de função de membro, independentemente do valor do código de retorno, a presença ou ausência de um retornados **IRowset** ou **IMultipleResults** referência de interface ou uma contagem de linhas afetadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
