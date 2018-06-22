---
title: Conjuntos de linhas de esquema alterados para parâmetros com valor de tabela do OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
ms.assetid: 581e3ead-53db-44da-8718-f3fc4b5108f1
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5a22515a53fe03e4076dc9cf0202516c61d5d683
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35699167"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>Conjuntos de linhas de esquema alterados para parâmetros com valor de tabela de OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  A seguir, são mostrados os conjuntos de linhas de esquema que foram alterados ou adicionados para dar suporte a parâmetros com valor de tabela.  
  
|Conjunto de linhas de esquema|Description|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Foram adicionadas duas novas colunas ao final do conjunto de linhas denominado SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMANAME. Essas colunas poderiam ser reutilizadas para tipos futuros. As colunas TYPE_NAME e LOCAL_TYPE_NAME conterão o nome do tipo TABLE do parâmetro com valor de tabela. A coluna DATA_TYPE terá o valor de DBTYPE_TABLE = 143 para parâmetros com valor de tabela.|  
|DBSCHEMA_TABLE_TYPES|Este conjunto de linhas foi adicionado para dar suporte a parâmetros com valor de tabela. Ele é idêntico ao DBSCHEMA_TABLES, a não ser pelo fato de retornar metadados apenas para tipos de tabela, em vez de tabelas, exibições ou sinônimos. A coluna TABLE_TYPE terá o valor 'TABLE TYPE'.|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|Este conjunto de linhas foi adicionado para dar suporte a parâmetros com valor de tabela. Ele é idêntico ao DBSCHEMA_PRIMARY_KEYS, a não ser pelo fato de retornar metadados de chaves primárias apenas para tipos de tabela, em vez de tabelas.|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|Este conjunto de linhas foi adicionado para dar suporte a parâmetros com valor de tabela. Ele é idêntico ao DBSCHEMA_COLUMNS, a não ser pelo fato de retornar metadados de coluna apenas para tipos de tabela, em vez de tabelas, exibições ou sinônimos.|  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
