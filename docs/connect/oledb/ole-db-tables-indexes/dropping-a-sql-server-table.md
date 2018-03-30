---
title: Descartando uma tabela do SQL Server | Microsoft Docs
description: Descartando uma tabela do SQL Server usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- OLE DB Driver for SQL Server, tables
- removing tables
- dropping tables
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 62ff10b72d209dce89a4995542d40b4f3e262a34
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2018
---
# <a name="dropping-a-sql-server-table"></a>Descartando uma tabela do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server expõe o **itabledefinition:: Droptable** function para remover um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabela de banco de dados.  
  
 Especifique o nome da tabela como uma cadeia de caracteres Unicode no *pwszName* membro do *uName* união no *pTableID* parâmetro. O *eKind* membro *pTableID* deve ser DBKIND_NAME.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
