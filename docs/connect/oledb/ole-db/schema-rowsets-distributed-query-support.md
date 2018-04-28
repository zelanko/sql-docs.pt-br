---
title: Suporte a consultas nos conjuntos de linhas de esquema distribuídas | Microsoft Docs
description: Suporte a consultas nos conjuntos de linhas de esquema distribuídas
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], OLE DB Driver for SQL Server
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa604a66d953a4e25c3df3f20fb32218e179451b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="schema-rowsets---distributed-query-support"></a>Conjuntos de linhas de esquema - suporte à consulta distribuída
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para dar suporte a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consultas, o Driver OLE DB para SQL Server distribuídas **IDBSchemaRowset** interface retorna metadados em servidores vinculados.  
  
 Caso a propriedade SSPROP_QUOTEDCATALOGNAMES de DBPROPSET_SQLSERVERSESSION seja VARIANT_TRUE, um identificador citado pode ser especificado para o nome do catálogo (por exemplo "my.catalog"). Quando a restrição de saída do conjunto de linhas de esquema por catálogo, o Driver OLE DB para SQL Server reconhece um nome de duas partes que contém o servidor vinculado e nome do catálogo. Para os conjuntos de linhas de esquema na tabela a seguir, especificando um nome de catálogo de duas partes como *linked_server ***.*** catálogo* restringe a saída para o catálogo aplicável do servidor vinculado nomeado.  
  
|Conjunto de linhas de esquema|Restrição de catálogo|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMNS|TABLE_CATALOG|  
|DBSCHEMA_PRIMARY_KEYS|TABLE_CATALOG|  
|DBSCHEMA_TABLES|TABLE_CATALOG|  
|DBSCHEMA_FOREIGN_KEYS|PK_TABLE_CATALOG FK_TABLE_CATALOG|  
|DBSCHEMA_INDEXES|TABLE_CATALOG|  
|DBSCHEMA_COLUMN_PRIVILEGES|TABLE_CATALOG|  
|DBSCHEMA_TABLE_PRIVILEGES|TABLE_CATALOG|  
  
> [!NOTE]  
>  Para restringir um conjunto de linhas de esquema em todos os catálogos de um servidor vinculado, use a sintaxe *linked_server* (onde o separador de ponto é parte da especificação do nome). Essa sintaxe é equivalente a especificar NULL para a restrição do nome do catálogo, além de ser usada quando o servidor vinculado indica uma fonte de dados que não oferece suporte a catálogos.  
  
 O Driver OLE DB para SQL Server define o conjunto de linhas do esquema LINKEDSERVERS, retornando uma lista de fontes de dados OLE DB registradas como servidores vinculados.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao conjunto de linhas de esquema &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [Conjunto de linhas LINKEDSERVERS &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
