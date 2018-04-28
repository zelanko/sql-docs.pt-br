---
title: Resultados de mensagem do SQL Server | Microsoft Docs
description: Resultados da mensagem do SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 586926250d1234c15cc77511800105b2c58f1e60
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-message-results"></a>Resultados de mensagem do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O seguinte [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções não geram Driver OLE DB para SQL Server de conjuntos de linhas ou uma contagem de linhas afetadas quando executadas:  
  
-   PRINT  
  
-   RAISERROR com uma severidade de 10 ou menor  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instruções retornam uma ou mais mensagens informativas ou fazem o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retornar mensagens informativas em vez de resultados de contagens ou conjuntos de linhas. Na execução bem sucedida, o Driver OLE DB para SQL Server Retorna S_OK e as mensagens estão disponíveis para o Driver OLE DB para o consumidor do SQL Server.  
  
 O Driver OLE DB para SQL Server Retorna S_OK e tem uma ou mais mensagens informativas disponíveis após a execução de várias [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções ou a execução do consumidor de um Driver OLE DB para a função de membro do SQL Server.  
  
 O Driver OLE DB para o consumidor do SQL Server que permite a especificação dinâmica do texto da consulta deve verificar as interfaces de erro após cada execução de função de membro, independentemente do valor do código de retorno, a presença ou ausência de um retornados **IRowset** ou **IMultipleResults** referência de interface ou uma contagem de linhas afetadas.  
  
## <a name="see-also"></a>Consulte também  
 [Erros](../../oledb/ole-db-errors/errors.md)  
  
  
