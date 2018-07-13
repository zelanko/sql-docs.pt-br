---
title: Suporte a consultas em conjuntos de linhas de esquema distribuídas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b640761d4c88f5a6a93772e12a2249f9f88f28f5
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419755"
---
# <a name="distributed-query-support-in-schema-rowsets"></a>Suporte à consulta distribuída no conjunto de linhas do esquema
  Para dar suporte à [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consultas distribuídas, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB provider **IDBSchemaRowset** interface retorna metadados em servidores vinculados.  
  
 Caso a propriedade SSPROP_QUOTEDCATALOGNAMES de DBPROPSET_SQLSERVERSESSION seja VARIANT_TRUE, um identificador citado pode ser especificado para o nome do catálogo (por exemplo "my.catalog"). Quando a restrição da saída do conjunto de linhas de esquema por catálogo, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client reconhece um nome de duas partes que contém o nome de catálogo e de servidor vinculado. Para os conjuntos de linhas de esquema na tabela a seguir, especificando um nome de catálogo de duas partes como *linked_server ***.*** catálogo* restringe a saída para o catálogo aplicável do servidor vinculado nomeado.  
  
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
>  Para restringir um conjunto de linhas de esquema a todos os catálogos de um servidor vinculado, use a sintaxe *linked_server* (onde o separador de ponto é parte da especificação do nome). Essa sintaxe é equivalente a especificar NULL para a restrição do nome do catálogo, além de ser usada quando o servidor vinculado indica uma fonte de dados que não oferece suporte a catálogos.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client define o conjunto de linhas do esquema LINKEDSERVERS, retornando uma lista de fontes de dados OLE DB registradas como servidores vinculados.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao conjunto de linhas de esquema &#40;OLE DB&#41;](schema-rowset-support-ole-db.md)   
 [Conjunto de linhas LINKEDSERVERS &#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
  
