---
title: Descartando um índice do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: efb206bda68421a8de81e0f1b03b541d839ef3cc
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429505"
---
# <a name="dropping-a-sql-server-index"></a>Descartando um índice do SQL Server
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client expõe a **iindexdefinition:: Dropindex** função. Isso permite que os consumidores removam um índice a partir de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client expõe algumas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restrições PRIMARY KEY e UNIQUE como índices. O proprietário da tabela, o proprietário do banco de dados e alguns membros de função administrativa podem modificar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela, descartando uma restrição. Por padrão, somente o proprietário da tabela pode descartar um índice existente. Portanto, **DropIndex** êxito ou falha depende não só os direitos de acesso do usuário do aplicativo, mas também no tipo de índice indicado.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode na *pwszName* membro do *uName* união no *pTableID* parâmetro. O *eKind* membro *pTableID* deve ser DBKIND_NAME.  
  
 Os consumidores especificam o nome do índice como uma cadeia de caracteres Unicode na *pwszName* membro do *uName* união no *pIndexID* parâmetro. O *eKind* membro *pIndexID* deve ser DBKIND_NAME. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client não oferece suporte ao recurso de OLE DB de descartar todos os índices em uma tabela quando *pIndexID* é nulo. Se *pIndexID* é nulo, E_INVALIDARG será retornado.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
