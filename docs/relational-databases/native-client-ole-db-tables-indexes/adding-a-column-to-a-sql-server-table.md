---
title: Adicionar coluna à tabela de SQL Server (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- SQL Server Native Client OLE DB provider, columns
- adding columns
ms.assetid: 22bae18a-bc9d-4617-8660-ed8b17a468d4
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c9042b2fb6c7495974cc64b16186834ebb30ed08
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942218"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>Adicionando uma coluna a uma tabela do SQL Server
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo expõe a função **ITableDefinition:: AddColumn** . Isso permite que os consumidores adicionem uma coluna a uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando você adiciona uma coluna a uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor de OLE DB de cliente nativo é restrito da seguinte maneira:  
  
-   Caso DBPROP_COL_AUTOINCREMENT seja VARIANT_TRUE, DBPROP_COL_NULLABLE deve ser VARIANT_FALSE.  
  
-   Caso a coluna seja definida usando o tipo de dados  **timestamp** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], DBPROP_COL_NULLABLE precisará ser VARIANT_FALSE.  
  
-   Para qualquer outra definição de coluna, DBPROP_COL_NULLABLE deve ser VARIANT_TRUE.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pTableID*. O membro *eKind* de *pTableID* precisa ser DBKIND_NAME.  
  
 O nome da nova coluna é especificado como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no membro *dbcid* do parâmetro *pColumnDesc* de DBCOLUMNDESC. O membro *eKind* precisa ser DBKIND_NAME.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
