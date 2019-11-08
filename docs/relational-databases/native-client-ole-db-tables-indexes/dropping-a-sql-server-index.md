---
title: Descartando um índice de SQL Server | Microsoft Docs
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
ms.openlocfilehash: c2481c516714acd58ba243c614534b1079be6b0f
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761581"
---
# <a name="dropping-a-sql-server-index"></a>Descartando um índice do SQL Server

  O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client expõe a função **IIndexDefinition::D ropindex** . Isso permite que os consumidores removam um índice de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo do cliente expõe algumas restrições de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chave primária e exclusiva como índices. O proprietário da tabela, o proprietário do banco de dados e alguns membros de função administrativa podem modificar uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], removendo uma restrição. Por padrão, somente o proprietário da tabela pode descartar um índice existente. Portanto, o êxito ou a falha de **DropIndex** depende não só dos direitos de acesso do usuário do aplicativo, como também do tipo de índice indicado.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pTableID*. O membro *eKind* de *pTableID* precisa ser DBKIND_NAME.  
  
 Os consumidores especificam o nome do índice como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pIndexID*. O membro *eKind* de *pIndexID* precisa ser DBKIND_NAME. O provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte ao recurso OLE DB de remover todos os índices em uma tabela quando *pIndexID* é nulo. Se *pIndexID* for nulo, E_INVALIDARG será retornado.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
