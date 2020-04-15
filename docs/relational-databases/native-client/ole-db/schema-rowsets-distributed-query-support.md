---
title: Suporte à consulta distribuída no conjunto de linhas do esquema | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: daf4f4c0c7c6c1d53c2ab899dd150756399d53a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296948"
---
# <a name="schema-rowsets---distributed-query-support"></a>Conjuntos de linhas do esquema – suporte à consulta distribuída
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suportar consultas distribuídas, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de IDB Dole **DB,** nativo, retorna metadados em servidores vinculados.  
  
 Caso a propriedade SSPROP_QUOTEDCATALOGNAMES de DBPROPSET_SQLSERVERSESSION seja VARIANT_TRUE, um identificador citado pode ser especificado para o nome do catálogo (por exemplo "my.catalog"). Ao restringir a saída de esquema de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] linha definida por catálogo, o provedor Native Client OLE DB reconhece um nome de duas partes contendo o servidor vinculado e o nome do catálogo. Para os conjuntos de linhas de esquema na tabela abaixo, especificando um nome de catálogo de duas partes como _linked_server_**.** _catálogo_ restringe a saída ao catálogo aplicável do servidor vinculado nomeado.  
  
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
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor Native Client OLE DB define o esquema de conjunto de linhas LINKEDSERVERS, retornando uma lista de fontes de dados OLE DB registradas como servidores vinculados.  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte ao conjunto de linhas de esquema &#40;&#41;OLE DB](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [Conjunto de linhas LINKEDSERVERS &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
