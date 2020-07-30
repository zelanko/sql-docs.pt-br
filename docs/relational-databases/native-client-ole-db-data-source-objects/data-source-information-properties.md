---
title: Propriedades de informações da fonte de dados (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 7fd80e47-5bd9-41e2-a3d3-091a7c8c5f2b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6bd0f6a5cd28d4b8ec2f7ba8063de551c45d6b94
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247022"
---
#  <a name="sql-server-native-client-data-source-information-properties"></a>Propriedades de informações da fonte de dados do SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERDATASOURCEINFO, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define as seguintes propriedades de informações da fonte de dados.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|Tipo: VT_BOOL<br /><br /> Leitura/gravação: leitura<br /><br /> Padrão: VARIANT_TRUE<br /><br /> Descrição: usado para determinar se há suporte para a ordenação de coluna.<br /><br /> VARIANT_TRUE: há suporte à ordenação em nível de coluna.<br /><br /> VARIANT_FALSE: não há suporte para a ordenação em nível de coluna.|  
|SSPROP_UNICODELCID|Tipo: VT_I4 Leitura/gravação: leitura<br /><br /> Descrição: ID da localidade Unicode.<br /><br /> Esta é a localidade usada para classificação de dados Unicode.|  
|SSPROP_UNICODECOMPARISONSTYLE|Tipo: VT_I4 Leitura/gravação: leitura<br /><br /> Descrição: estilo de comparação Unicode.<br /><br /> As opções de classificação usadas para a classificação de dados Unicode.|  
  
 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERSTREAM, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define a seguinte propriedade adicional.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|Tipo: VT_BSTR Leitura/gravação: leitura/gravação<br /><br /> Descrição: o resultado de uma consulta XML FOR pode não ser um documento bem formado. Quando esta propriedade é especificada, o resultado de uma consulta ‘select ... for XML' é quebrado na marca raiz fornecida por essa propriedade para retornar um documento XML bem formado. Se a consulta for executada no navegador, ela pode fazer o navegador exibir erros de analisador ao carregar o resultado. Para evitar o erro, o SQL ISAPI dá suporte à palavra-chave ROOT. Essa palavra-chave é mapeada para a propriedade SSPROP_STREAM_XMLROOT.|  
  
## <a name="see-also"></a>Consulte Também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
