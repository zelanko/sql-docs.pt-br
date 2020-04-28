---
title: Conjuntos de linhas de esquema, OLE DB parâmetros com valor de tabela
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
ms.assetid: 581e3ead-53db-44da-8718-f3fc4b5108f1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b79f2b2b87e4a51c71a3c2c89378875810f92fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283051"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>Conjuntos de linhas de esquema alterados para parâmetros com valor de tabela de OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A seguir, são mostrados os conjuntos de linhas de esquema que foram alterados ou adicionados para dar suporte a parâmetros com valor de tabela.  
  
|Conjunto de linhas de esquema|Descrição|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Foram adicionadas duas novas colunas ao final do conjunto de linhas denominado SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMANAME. Essas colunas poderiam ser reutilizadas para tipos futuros. As colunas TYPE_NAME e LOCAL_TYPE_NAME conterão o nome do tipo TABLE do parâmetro com valor de tabela. A coluna DATA_TYPE terá o valor de DBTYPE_TABLE = 143 para parâmetros com valor de tabela.|  
|DBSCHEMA_TABLE_TYPES|Este conjunto de linhas foi adicionado para dar suporte a parâmetros com valor de tabela. Ele é idêntico ao DBSCHEMA_TABLES, a não ser pelo fato de retornar metadados apenas para tipos de tabela, em vez de tabelas, exibições ou sinônimos. A coluna TABLE_TYPE terá o valor 'TABLE TYPE'.|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|Este conjunto de linhas foi adicionado para dar suporte a parâmetros com valor de tabela. Ele é idêntico ao DBSCHEMA_PRIMARY_KEYS, a não ser pelo fato de retornar metadados de chaves primárias apenas para tipos de tabela, em vez de tabelas.|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|Este conjunto de linhas foi adicionado para dar suporte a parâmetros com valor de tabela. Ele é idêntico ao DBSCHEMA_COLUMNS, a não ser pelo fato de retornar metadados de coluna apenas para tipos de tabela, em vez de tabelas, exibições ou sinônimos.|  
|||

## <a name="see-also"></a>Consulte Também  
 [Os parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
