---
title: OLE DB de propriedades de sessão
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2044bed875e8671696ea5bc262eff1bf1dfd59e1
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998257"
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>Propriedades da sessão – Provedor OLE DB do SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo interpreta OLE DB Propriedades de sessão da seguinte maneira.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte a todos os níveis de isolamento da transação de confirmação automática, com exceção do nível de caos DBPROPVAL_TI_CHAOS.|  
|||

 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERSESSION, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo define a seguinte propriedade de sessão adicional.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Tipo: VT_BOOL<br /><br /> L/G: Leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Identificadores citados permitidos na restrição CATALOG.<br /><br /> VARIANT_TRUE: São reconhecidos identificadores citados para uma restrição de catálogo dos conjuntos de linhas de esquema que fornecem suporte à consulta distribuída.<br /><br /> VARIANT_FALSE: Não são reconhecidos identificadores citados para uma restrição de catálogo dos conjuntos de linhas de esquema que fornecem suporte à consulta distribuída.<br /><br /> Para obter mais informações sobre conjuntos de linhas de esquema que fornecem suporte à consulta distribuída, confira [Suporte à consulta distribuída em conjuntos de linhas de esquema](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Tipo: VT_BOOL<br /><br /> Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: Determina se os dados buscados são como DBTYPE_VARIANT ou DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: o tipo de coluna é retornado como DBTYPE_SQLVARIANT e o buffer terá a estrutura SSVARIANT.<br /><br /> VARIANT_FALSE: o tipo de coluna é retornado como DBTYPE_VARIANT e o buffer terá a estrutura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Para usar o modo assíncrono, defina a propriedade de sessão SSPROP_ASYNCH_BULKCOPY específica do provedor como VARIANT_TRUE antes de chamar o método BCPExec. Essa propriedade está disponível no conjunto de propriedades DBPROPSET_SQLSERVERSESSION.|  
|||

## <a name="see-also"></a>Consulte Também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
