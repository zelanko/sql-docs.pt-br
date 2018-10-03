---
title: Descartando um índice do SQL Server | Microsoft Docs
description: Descartando um índice do sql server usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 990318037a3f1b35e311a983859507a364c52127
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669164"
---
# <a name="dropping-a-sql-server-index"></a>Descartando um índice do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server expõe a **iindexdefinition:: Dropindex** função. Isso permite que os consumidores removam um índice de uma tabela do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 O Driver do OLE DB para SQL Server expõe algumas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] restrições PRIMARY KEY e UNIQUE como índices. O proprietário da tabela, o proprietário do banco de dados e alguns membros de função administrativa podem modificar uma tabela do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], removendo uma restrição. Por padrão, somente o proprietário da tabela pode descartar um índice existente. Portanto, o êxito ou a falha de **DropIndex** depende não só dos direitos de acesso do usuário do aplicativo, como também do tipo de índice indicado.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pTableID*. O membro *eKind* de *pTableID* precisa ser DBKIND_NAME.  
  
 Os consumidores especificam o nome do índice como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pIndexID*. O membro *eKind* de *pIndexID* precisa ser DBKIND_NAME. O OLE DB Driver for SQL Server não dá suporte ao recurso do OLE DB de remoção de todos os índices em uma tabela quando *pIndexID* é nulo. Se *pIndexID* for nulo, E_INVALIDARG será retornado.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
