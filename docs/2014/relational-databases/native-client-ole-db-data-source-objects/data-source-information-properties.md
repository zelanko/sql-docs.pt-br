---
title: Propriedades de informações da fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 946c6d39bd02bbccd898262da6642813fbb3c94f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679784"
---
# <a name="data-source-information-properties"></a>Propriedades de informações da fonte de dados
  No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERDATASOURCEINFO, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define as seguintes propriedades de informações da fonte de dados.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|Digite: VT_BOOL<br /><br /> R/W: leitura<br /><br /> Padrão: VARIANT_TRUE<br /><br /> Descrição: Usado para determinar se há suporte para o agrupamento de coluna.<br /><br /> VARIANT_TRUE: Há suporte para agrupamento em nível de coluna.<br /><br /> VARIANT_FALSE: Não há suporte para agrupamento em nível de coluna.|  
|SSPROP_UNICODELCID|Digite: VT_I4 R/W: leitura<br /><br /> Descrição: ID de localidade Unicode.<br /><br /> Esta é a localidade usada para classificação de dados Unicode.|  
|SSPROP_UNICODECOMPARISONSTYLE|Digite: VT_I4 R/W: leitura<br /><br /> Descrição: Estilo de comparação Unicode.<br /><br /> As opções de classificação usadas para a classificação de dados Unicode.|  
  
 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERSTREAM, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define a seguinte propriedade adicional.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|Digite: VT_BSTR R/W: Leitura/gravação<br /><br /> Descrição: O resultado de uma consulta FOR XML não pode ser um documento bem formado. Quando essa propriedade for especificada, o resultado de uma consulta 'select... for XML' é encapsulado na marca raiz fornecida por essa propriedade para retornar um documento XML bem formado. Se a consulta for executada no navegador, ela pode fazer o navegador exibir erros de analisador ao carregar o resultado. Para evitar o erro, o SQL ISAPI dá suporte à palavra-chave ROOT. Essa palavra-chave é mapeada para a propriedade SSPROP_STREAM_XMLROOT.|  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
