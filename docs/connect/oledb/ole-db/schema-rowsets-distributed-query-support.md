---
title: Suporte a consultas em conjuntos de linhas de esquema distribuídas | Microsoft Docs
description: Suporte à consulta distribuída no conjunto de linhas do esquema
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 77960d1a5b38ef9ae66fe2705f38f10a739daa2a
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031725"
---
# <a name="schema-rowsets---distributed-query-support"></a>Conjuntos de linhas do esquema – suporte à consulta distribuída
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Para oferecer suporte a consultas distribuídas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a interface **IDBSchemaRowset** do OLE DB Driver for SQL Server retorna metadados em servidores vinculados.  
  
 Caso a propriedade SSPROP_QUOTEDCATALOGNAMES de DBPROPSET_SQLSERVERSESSION seja VARIANT_TRUE, um identificador citado pode ser especificado para o nome do catálogo (por exemplo "my.catalog"). Durante a restrição da saída do conjunto de linhas do esquema por catálogo, o OLE DB Driver for SQL Server reconhece um nome em duas partes que contém o servidor vinculado e o nome do catálogo. Para os conjuntos de linhas de esquema na tabela abaixo, especificar um nome de catálogo em duas partes como *linked_server ***.*** catalog* restringe a saída para o catálogo aplicável do servidor vinculado nomeado.  
  
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
>  Para restringir um conjunto de linhas do esquema a todos os catálogos de um servidor vinculado, use a sintaxe *linked_server* (em que o separador do período faz parte da especificação do nome). Essa sintaxe é equivalente a especificar NULL para a restrição do nome do catálogo, além de ser usada quando o servidor vinculado indica uma fonte de dados que não oferece suporte a catálogos.  
  
 O OLE DB Driver for SQL Server define o conjunto de linhas do esquema LINKEDSERVERS, retornando uma lista de fontes de dados OLE DB registradas como servidores vinculados.  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte ao conjunto de linhas de esquema &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [Conjunto de linhas LINKEDSERVERS &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
