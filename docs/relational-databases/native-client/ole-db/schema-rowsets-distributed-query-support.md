---
title: Suporte de consulta distribuída em conjuntos de linhas de esquema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3c162bbcbf9f9212d6adc3838a06b5eaaac8b13
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73759707"
---
# <a name="schema-rowsets---distributed-query-support"></a>Conjuntos de linhas do esquema – suporte à consulta distribuída
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para dar suporte a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consultas distribuídas, a interface **IDBSchemaRowset** do provedor de OLE DB do cliente nativo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] retorna metadados em servidores vinculados.  
  
 Caso a propriedade SSPROP_QUOTEDCATALOGNAMES de DBPROPSET_SQLSERVERSESSION seja VARIANT_TRUE, um identificador citado pode ser especificado para o nome do catálogo (por exemplo "my.catalog"). Ao restringir a saída do conjunto de linhas de esquema por catálogo, o provedor de OLE DB [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client reconhece um nome de duas partes que contém o servidor vinculado e o nome do catálogo. Para os conjuntos de linhas de esquema na tabela a seguir, especificando um nome de catálogo de duas partes como _linked_server_ **.** o _Catálogo_ restringe a saída para o catálogo aplicável do servidor vinculado nomeado.  
  
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
  
 O provedor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB define o conjunto de linhas de esquema LINKEDSERVERS, retornando uma lista de OLE DB fontes de dados registradas como servidores vinculados.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao conjunto de linhas de esquema &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [Conjunto de &#40;linhas LINKEDSERVERS OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
