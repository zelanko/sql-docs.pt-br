---
title: Descartando um índice do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4178e4b44bc226e31b6f6287b366d154cc306a9c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069554"
---
# <a name="dropping-a-sql-server-index"></a>Descartando um índice do SQL Server
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client expõe a **iindexdefinition:: Dropindex** função. Isso permite que os consumidores removam um índice de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client expõe algumas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restrições PRIMARY KEY e UNIQUE como índices. O proprietário da tabela, o proprietário do banco de dados e alguns membros de função administrativa podem modificar uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], removendo uma restrição. Por padrão, somente o proprietário da tabela pode descartar um índice existente. Portanto, o êxito ou a falha de **DropIndex** depende não só dos direitos de acesso do usuário do aplicativo, como também do tipo de índice indicado.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pTableID*. O membro *eKind* de *pTableID* precisa ser DBKIND_NAME.  
  
 Os consumidores especificam o nome do índice como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pIndexID*. O membro *eKind* de *pIndexID* precisa ser DBKIND_NAME. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client não oferece suporte ao recurso de OLE DB de descartar todos os índices em uma tabela quando *pIndexID* é nulo. Se *pIndexID* for nulo, E_INVALIDARG será retornado.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
