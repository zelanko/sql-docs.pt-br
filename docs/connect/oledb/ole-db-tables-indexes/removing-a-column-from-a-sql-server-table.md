---
title: Remover uma coluna de uma tabela do SQL Server | Microsoft Docs
description: Remover uma coluna de uma tabela do SQL Server usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- OLE DB Driver for SQL Server, columns
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 702f003afe0088daacd756af7abdf1935ed447ad
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="removing-a-column-from-a-sql-server-table"></a>Removendo uma coluna de uma tabela do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server expõe o **itabledefinition:: Dropcolumn** função. Isso permite que os consumidores removam uma coluna de uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabela.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no *pwszName*membro do *uName* união no *pTableID* parâmetro. O *eKind*membro *pTableID* deve ser DBKIND_NAME.  
  
 O consumidor indica um nome de coluna no *pwszName*membro do *uName* união no *pColumnID* parâmetro. O nome da coluna é uma cadeia de caracteres Unicode. O *eKind* membro *pColumnID* deve ser DBKIND_NAME.  
  
## <a name="example"></a>Exemplo  
  
### <a name="code"></a>Código  
  
```  
DBID TableID;  
DBID ColumnID;  
HRESULT hr;  
  
TableID.eKind = DBKIND_NAME;  
TableID.uName.pwszName = L"MyTableName";  
  
ColumnID.eKind = DBKIND_NAME;  
ColumnID.uName.pwszName = L"MyColumnName";  
  
hr = m_pITableDefinition->DropColumn(&TableID, &ColumnID);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
