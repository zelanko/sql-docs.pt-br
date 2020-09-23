---
title: Adicionar uma coluna a uma tabela do SQL Server (Driver do OLE DB) | Microsoft Docs
description: Saiba como o método ITableDefinition::AddColumn permite que os clientes adicionem uma coluna à tabela do SQL Server no Driver do OLE DB para SQL Server.
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4366011d2f417dc7c35383a4460bfe5871065940
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859803"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Adicionando uma coluna a uma tabela do SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

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
  
  
