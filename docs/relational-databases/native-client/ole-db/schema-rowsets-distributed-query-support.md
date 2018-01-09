---
title: "Suporte a consultas nos conjuntos de linhas de esquema distribuídas | Microsoft Docs"
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
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a297b79cea0cbde41e06e10ce494702553b835de
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="schema-rowsets---distributed-query-support"></a>Conjuntos de linhas de esquema - suporte à consulta distribuída
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Para dar suporte a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] distribuídas consultas, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client **IDBSchemaRowset** interface retorna metadados em servidores vinculados.  
  
 Caso a propriedade SSPROP_QUOTEDCATALOGNAMES de DBPROPSET_SQLSERVERSESSION seja VARIANT_TRUE, um identificador citado pode ser especificado para o nome do catálogo (por exemplo "my.catalog"). Quando a restrição de saída do conjunto de linhas de esquema por catálogo, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client reconhece um nome de duas partes que contém o nome de catálogo e de servidor vinculado. Para os conjuntos de linhas de esquema na tabela a seguir, especificando um nome de catálogo de duas partes como *linked_server***.** *catálogo* restringe a saída para o catálogo aplicável do servidor vinculado nomeado.  
  
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
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client define o conjunto de linhas do esquema LINKEDSERVERS, retornando uma lista de fontes de dados OLE DB registradas como servidores vinculados.  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte ao conjunto de linhas de esquema &#40; OLE DB &#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [Conjunto de linhas LINKEDSERVERS &#40; OLE DB &#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
