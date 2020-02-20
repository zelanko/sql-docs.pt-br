---
title: Resultados da mensagem do SQL Server | Microsoft Docs
description: Resultados da mensagem do SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 05d731f418bad21f9e8ec32c620b352c5663994a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994913"
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
  
 Estas instruções retornam uma ou mais mensagens informativas ou fazem o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retornar mensagens informativas em vez de resultados de contagens ou conjuntos de linhas. Após a execução bem-sucedida, o Driver do OLE DB para SQL Server retorna S_OK e as mensagens estão disponíveis para o consumidor do Driver do OLE DB para SQL Server.  
  
 O Driver do OLE DB para SQL Server retorna S_OK e tem uma ou mais mensagens informativas disponíveis após a execução de várias instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou a execução do consumidor de uma função de membro do Driver do OLE DB para SQL Server.  
  
 O consumidor do OLE DB Driver for SQL Server que permite a especificação dinâmica do texto da consulta deve verificar as interfaces de erro após a execução de cada função de membro, independentemente do valor do código de retorno, da presença ou ausência de uma referência de interface **IRowset** ou **IMultipleResults** retornada ou de uma contagem de linhas afetadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](../../oledb/ole-db-errors/errors.md)  
  
  
