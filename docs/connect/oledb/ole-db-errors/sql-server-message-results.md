---
title: Resultados de mensagem do SQL Server | Microsoft Docs
description: Resultados da mensagem do SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: e13ec74572e04e210b312e19d1e04aa1423d26db
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028833"
---
# <a name="sql-server-message-results"></a>Resultados da mensagem do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  As seguintes instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] não geram conjuntos de linhas do OLE DB Driver for SQL Server nem uma contagem de linhas afetadas quando executadas:  
  
-   PRINT  
  
-   RAISERROR com uma severidade de 10 ou menor  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instruções retornam uma ou mais mensagens informativas ou fazem o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retornar mensagens informativas em vez de resultados de contagens ou conjuntos de linhas. Na execução bem-sucedida, o Driver do OLE DB para SQL Server Retorna S_OK e as mensagens estão disponíveis para o Driver OLE DB para o consumidor do SQL Server.  
  
 O Driver do OLE DB para SQL Server Retorna S_OK e tem um ou mais mensagens informativas disponíveis após a execução de várias [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções ou a execução do consumidor de um Driver OLE DB para a função de membro do SQL Server.  
  
 O consumidor do OLE DB Driver for SQL Server que permite a especificação dinâmica do texto da consulta deve verificar as interfaces de erro após a execução de cada função de membro, independentemente do valor do código de retorno, da presença ou ausência de uma referência de interface **IRowset** ou **IMultipleResults** retornada ou de uma contagem de linhas afetadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](../../oledb/ole-db-errors/errors.md)  
  
  
