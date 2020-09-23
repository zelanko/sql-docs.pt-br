---
title: Resultados da mensagem de SQL Server (Driver do OLE DB)
description: Saiba mais sobre instruções do Transact-SQL que não geram conjuntos de linhas ou uma contagem do Driver do OLE DB para SQL Server e seus valores retornados esperados.
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc3701313f920eead650435ca40538ad8a4b6ef0
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862502"
---
# <a name="sql-server-message-results"></a>Resultados da mensagem do SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

As seguintes instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] não geram conjuntos de linhas do Driver do OLE DB para SQL Server nem uma contagem de linhas afetadas quando executadas:  
  
-   PRINT  
  
-   RAISERROR com uma severidade de 10 ou menor  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instruções retornam uma ou mais mensagens informativas ou fazem o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retornar mensagens informativas em vez de resultados de contagens ou conjuntos de linhas. Após a execução bem-sucedida, o Driver do OLE DB para SQL Server retorna S_OK e as mensagens estão disponíveis para o consumidor do Driver do OLE DB para SQL Server.  
  
 O Driver do OLE DB para SQL Server retorna S_OK e tem uma ou mais mensagens informativas disponíveis após a execução de várias instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou a execução do consumidor de uma função de membro do Driver do OLE DB para SQL Server.  
  
O consumidor do Driver do OLE DB para SQL Server tem permissão para especificação dinâmica do texto da consulta. O consumidor deve verificar as interfaces de erro depois de _cada_ execução de função membro. Ele sempre deve executar essas verificações, independentemente do valor do código de retorno, da contagem de linhas afetadas e de se uma referência de interface a um `IRowset` ou `IMultipleResults` é retornada ou não.
  
## <a name="see-also"></a>Consulte Também  
 [Erros](../../oledb/ole-db-errors/errors.md)  
  
  
