---
title: Propriedades de sessão – OLE DB Driver for SQL Server | Microsoft Docs
description: Propriedades de sessão – OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- OLE DB Driver for SQL Server, sessions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7bc2ae9c6908bfcd0bf28b4f05be757d22c55f75
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015912"
---
# <a name="session-properties---ole-db-driver-for-sql-server"></a>Propriedades de sessão – OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server interpreta as propriedades de sessão do OLE DB como a seguir.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|O OLE DB Driver for SQL Server dá suporte a todos os níveis de isolamento da transação de confirmação automática, com a exceção do nível de caos DBPROPVAL_TI_CHAOS.|  
  
 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERSESSION, o OLE DB Driver for SQL Server define a propriedade de sessão adicional a seguir.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Tipo: VT_BOOL<br /><br /> L/G: Leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Identificadores citados permitidos na restrição de CATÁLOGO.<br /><br /> VARIANT_TRUE: identificadores citados são reconhecidos para uma restrição de catálogo dos conjuntos de linhas de esquema que fornecem suporte à consulta distribuída.<br /><br /> VARIANT_FALSE: identificadores citados não são reconhecidos para uma restrição de catálogo dos conjuntos de linhas de esquema que fornecem suporte à consulta distribuída.<br /><br /> Para obter mais informações sobre conjuntos de linhas de esquema que fornecem suporte à consulta distribuída, confira [Suporte à consulta distribuída em conjuntos de linhas de esquema](../../oledb/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Tipo: VT_BOOL<br /><br /> L/G: Leitura/Gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: determina se os dados buscados são como DBTYPE_VARIANT ou DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: o tipo de coluna é retornado como DBTYPE_SQLVARIANT e, nesse caso, o buffer terá a estrutura SSVARIANT.<br /><br /> VARIANT_FALSE: o tipo de coluna é retornado como DBTYPE_VARIANT e o buffer terá a estrutura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Para usar o modo assíncrono, defina a propriedade de sessão SSPROP_ASYNCH_BULKCOPY específica do provedor como VARIANT_TRUE antes de chamar o método BCPExec. Essa propriedade está disponível no conjunto de propriedades DBPROPSET_SQLSERVERSESSION.|  
  
## <a name="see-also"></a>Consulte Também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
