---
title: Suporte de conjunto de linhas de esquema (OLE DB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- SQL Server Native Client OLE DB provider, schema rowsets
- rowsets [OLE DB], schema
ms.assetid: a75b4b69-b095-4690-9b31-a2b32a67489e
caps.latest.revision: "42"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5421f7ad80bdd973005dd94d7e9708bb1e694a7e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="schema-rowset-support-ole-db"></a>Suporte a conjunto de linhas de esquema (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client também suporta retornando informações de esquema de um servidor vinculado ao processar [!INCLUDE[tsql](../../../includes/tsql-md.md)] consultas distribuídas.  
  
> [!NOTE]  
>  Apesar de o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suportar sinônimos, metadados para sinônimos não são retornados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
 As tabelas a seguir lista conjuntos de linhas de esquema e as colunas de restrição com suporte a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client.  
  
|Conjunto de linhas de esquema|Colunas de restrição|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|Todas as restrições são suportadas.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|DBSCHEMA_COLUMNS|Todas as restrições são suportadas.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME<br /><br /> As colunas adicionais a seguir são específicas ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:<br /><br /> COLUMN_LCID, que é a ID de localidade do agrupamento. COLUMN_LCID tem o mesmo valor de um LCID do Windows.<br /><br /> COLUMN_COMPFLAGS define quais comparações são suportadas para o agrupamento. O formato de dados é o mesmo do DBPROB_FINDCOMPAREOPS.<br /><br /> COLUMN_SORTID, que é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estilo para o agrupamento de classificação.<br /><br /> COLUMN_TDSCOLLATION, que é o agrupamento do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para a coluna.<br /><br /> IS_COMPUTED, que é VARIANT_TRUE se a coluna for uma coluna computada e VARIANT_FALSE em caso contrário.|  
|DBSCHEMA_FOREIGN_KEYS|Há suporte para todas as restrições.<br /><br /> PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|DBSCHEMA_INDEXES|As restrições 1, 2, 3 e 5 são suportadas.<br /><br /> TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TABLE_NAME|  
|DBSCHEMA_PRIMARY_KEYS|Há suporte para todas as restrições.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Há suporte para todas as restrições.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|DBSCHEMA_PROCEDURES|As restrições 1, 2 e 3 são suportadas.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME<br /><br /> DBSCHEMA_PROCEDURES só retorna procedimentos que podem ser executados pelo usuário atual, ou para os quais o usuário atual obteve permissão de VIEW DEFINITION.|  
|DBSCHEMA_PROVIDER_TYPES|Há suporte para todas as restrições.<br /><br /> DATA_TYPE BEST_MATCH|  
|DBSCHEMA_SCHEMATA|Há suporte para todas as restrições.<br /><br /> CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|DBSCHEMA_STATISTICS|Há suporte para todas as restrições.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_TABLE_CONSTRAINTS|Há suporte para todas as restrições.<br /><br /> CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|DBSCHEMA_TABLE_PRIVILEGES|Há suporte para todas as restrições.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|DBSCHEMA_TABLES|Há suporte para todas as restrições.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|DBSCHEMA_TABLES_INFO|Há suporte para todas as restrições.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
  
## <a name="in-this-section"></a>Nesta seção  
 [Suporte a consultas nos conjuntos de linhas de esquema distribuídas](../../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md)  
  
 [Conjunto de linhas LINKEDSERVERS &#40; OLE DB &#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Cliente nativo do SQL Server &#40; OLE DB &#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usando tipos definidos pelo usuário](../../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
