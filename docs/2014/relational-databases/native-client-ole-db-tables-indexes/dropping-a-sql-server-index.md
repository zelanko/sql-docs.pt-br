---
title: Descartar um índice do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9be4e3607097c476f083c32eed9f13fecc0d3842
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704519"
---
# <a name="dropping-a-sql-server-index"></a>Descartando um índice do SQL Server
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo expõe a função **IIndexDefinition::D ropindex** . Isso permite que os consumidores removam um índice de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo expõe algumas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restrições PRIMARY KEY e Unique como índices. O proprietário da tabela, o proprietário do banco de dados e alguns membros de função administrativa podem modificar uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], removendo uma restrição. Por padrão, somente o proprietário da tabela pode descartar um índice existente. Portanto, o êxito ou a falha de **DropIndex** depende não só dos direitos de acesso do usuário do aplicativo, como também do tipo de índice indicado.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pTableID*. O membro *eKind* de *pTableID* precisa ser DBKIND_NAME.  
  
 Os consumidores especificam o nome do índice como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pIndexID*. O membro *eKind* de *pIndexID* precisa ser DBKIND_NAME. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo não dá suporte ao recurso de OLE DB de remover todos os índices em uma tabela quando *pIndexID* é nulo. Se *pIndexID* for nulo, E_INVALIDARG será retornado.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e índices](tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
