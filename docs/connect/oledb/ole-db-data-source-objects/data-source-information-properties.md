---
title: Propriedades de informações da fonte de dados | Microsoft Docs
description: Propriedades de informações da fonte de dados
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ba9fa21f0c22c342922946a43124216a25ba09ef
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68016027"
---
# <a name="data-source-information-properties"></a>Propriedades de informações da fonte de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERDATASOURCEINFO, o OLE DB Driver for SQL Server define as propriedades de informações da fonte de dados a seguir.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|Tipo: VT_BOOL<br /><br /> L/G: Ler<br /><br /> Padrão: VARIANT_TRUE<br /><br /> Descrição: usado para determinar se a ordenação de colunas é compatível.<br /><br /> VARIANT_TRUE: a ordenação em nível de coluna é compatível.<br /><br /> VARIANT_FALSE: a ordenação em nível de coluna não é compatível.|  
|SSPROP_UNICODELCID|Tipo: VT_I4 R/W: Ler<br /><br /> Descrição: Identificação de localidade Unicode.<br /><br /> Esta é a localidade usada para classificação de dados Unicode.|  
|SSPROP_UNICODECOMPARISONSTYLE|Tipo: VT_I4 R/W: Ler<br /><br /> Descrição: estilo de comparação Unicode.<br /><br /> As opções de classificação usadas para a classificação de dados Unicode.|  
  
 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERSTREAM, o OLE DB Driver for SQL Server define a propriedade adicional a seguir.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|Tipo: VT_BSTR R/W: Leitura/Gravação<br /><br /> Descrição: o resultado de uma Consulta XML FOR pode não ser um documento bem formado. Quando esta propriedade é especificada, o resultado de uma consulta ‘select ... for XML' é quebrado na marca raiz fornecida por essa propriedade para retornar um documento XML bem formado. Se a consulta for executada no navegador, ela pode fazer o navegador exibir erros de analisador ao carregar o resultado. Para evitar o erro, o SQL ISAPI dá suporte à palavra-chave ROOT. Essa palavra-chave é mapeada para a propriedade SSPROP_STREAM_XMLROOT.|  
  
## <a name="see-also"></a>Consulte Também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
