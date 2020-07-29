---
title: Suporte ao conjunto de linhas de esquema (OLE DB) | Microsoft Docs
description: Suporte ao conjunto de linhas de esquema (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- OLE DB Driver for SQL Server, schema rowsets
- rowsets [OLE DB], schema
author: pmasl
ms.author: pelopes
ms.openlocfilehash: fdd00a0c53e2570ec9688665ce5348401571531b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012819"
---
# <a name="schema-rowset-support-ole-db"></a>Suporte a conjunto de linhas de esquema (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O OLE DB Driver for SQL Server também dá suporte ao retorno de informações de esquema de um servidor vinculado ao processar consultas distribuídas do [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  Apesar de o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dar suporte a sinônimos, metadados para sinônimos não são retornados pelo Driver do OLE DB para SQL Server.  
  
 As tabelas a seguir listam conjuntos de linhas de esquema e as colunas de restrição compatíveis com o OLE DB Driver for SQL Server.  
  
|Conjunto de linhas de esquema|Colunas de restrição|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|Todas as restrições são suportadas.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|DBSCHEMA_COLUMNS|Todas as restrições são suportadas.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME<br /><br /> As colunas adicionais a seguir são específicas ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:<br /><br /> COLUMN_LCID, que é a ID de localidade da ordenação. COLUMN_LCID tem o mesmo valor de um LCID do Windows.<br /><br /> COLUMN_COMPFLAGS define quais comparações são suportadas para a ordenação. O formato de dados é o mesmo do DBPROB_FINDCOMPAREOPS.<br /><br /> COLUMN_SORTID, que é o estilo de classificação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para a ordenação.<br /><br /> COLUMN_TDSCOLLATION, que é a ordenação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para a coluna.<br /><br /> IS_COMPUTED, que é VARIANT_TRUE se a coluna for uma coluna computada e VARIANT_FALSE em caso contrário.|  
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
 [Suporte à consulta distribuída no conjunto de linhas do esquema](../../oledb/ole-db/schema-rowsets-distributed-query-support.md)  
  
 [Conjunto de linhas LINKEDSERVERS &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no OLE DB Driver for SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [Usando tipos definidos pelo usuário](../../oledb/features/using-user-defined-types.md)  
  
  
