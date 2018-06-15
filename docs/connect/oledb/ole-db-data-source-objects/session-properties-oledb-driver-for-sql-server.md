---
title: Propriedades da sessão - Driver do OLE DB para SQL Server | Microsoft Docs
description: Propriedades da sessão - OLE DB Driver para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- OLE DB Driver for SQL Server, sessions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: a0d7e97017a8d188eaf9fb9cc24b0b2fbc0e80b2
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2018
ms.locfileid: "35666426"
---
# <a name="session-properties---ole-db-driver-for-sql-server"></a>Propriedades da sessão - Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver OLE DB para SQL Server interpreta as propriedades de sessão do OLE DB da seguinte maneira.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|O Driver OLE DB para SQL Server dá suporte a todos os níveis de isolamento de transação de confirmação automática com a exceção de nível de caos DBPROPVAL_TI_CHAOS.|  
  
 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERSESSION, o Driver OLE DB para SQL Server define a propriedade de sessão adicional a seguir.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Tipo: VT_BOOL<br /><br /> Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Identificadores citados permitidos na restrição CATALOG.<br /><br /> VARIANT_TRUE: São reconhecidos identificadores citados para uma restrição de catálogo dos conjuntos de linhas de esquema que fornecem suporte à consulta distribuída.<br /><br /> VARIANT_FALSE: Não são reconhecidos identificadores citados para uma restrição de catálogo dos conjuntos de linhas de esquema que fornecem suporte à consulta distribuída.<br /><br /> Para obter mais informações sobre conjuntos de linhas de esquema que fornecem suporte à consulta distribuída, consulte [suporte à consulta distribuída em conjuntos de linhas de esquema](../../oledb/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Tipo: VT_BOOL<br /><br /> Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Determina se os dados buscados são como DBTYPE_VARIANT ou DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: o tipo de coluna é retornado como DBTYPE_SQLVARIANT e o buffer terá a estrutura SSVARIANT.<br /><br /> VARIANT_FALSE: o tipo de coluna é retornado como DBTYPE_VARIANT e o buffer terá a estrutura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Para usar o modo assíncrono, defina a propriedade de sessão SSPROP_ASYNCH_BULKCOPY específica do provedor como VARIANT_TRUE antes de chamar o método BCPExec. Essa propriedade está disponível no conjunto de propriedades DBPROPSET_SQLSERVERSESSION.|  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
