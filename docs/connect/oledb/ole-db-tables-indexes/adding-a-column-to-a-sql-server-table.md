---
title: Adicionar uma coluna a uma tabela do SQL Server | Microsoft Docs
description: Adicionar uma coluna para uma tabela do SQL Server usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- OLE DB Driver for SQL Server, columns
- adding columns
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2c6cd539e499f80342a30371d047c9870c4fda08
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994096"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Adicionando uma coluna a uma tabela do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server expõe a função **ITableDefinition::AddColumn**. Isso permite que os consumidores adicionem uma coluna a uma tabela do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Quando você adiciona uma coluna a uma tabela do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o consumidor do Driver do OLE DB para SQL Server é restringido da seguinte forma:  
  
-   Caso DBPROP_COL_AUTOINCREMENT seja VARIANT_TRUE, DBPROP_COL_NULLABLE deve ser VARIANT_FALSE.  
  
-   Caso a coluna seja definida usando o tipo de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]timestamp**do**, DBPROP_COL_NULLABLE precisará ser VARIANT_FALSE.  
  
-   Para qualquer outra definição de coluna, DBPROP_COL_NULLABLE deve ser VARIANT_TRUE.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pTableID*. O membro *eKind* de *pTableID* precisa ser DBKIND_NAME.  
  
 O nome da nova coluna é especificado como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no membro *dbcid* do parâmetro *pColumnDesc* de DBCOLUMNDESC. O membro *eKind* precisa ser DBKIND_NAME.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
