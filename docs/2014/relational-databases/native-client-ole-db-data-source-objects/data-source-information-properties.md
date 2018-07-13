---
title: Propriedades de informações da fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 7fd80e47-5bd9-41e2-a3d3-091a7c8c5f2b
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ac3906946e7f732d9f7ddb92989ceaf79c5225c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410017"
---
# <a name="data-source-information-properties"></a>Propriedades de informações da fonte de dados
  No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERDATASOURCEINFO, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define as seguintes propriedades de informações da fonte de dados.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|Tipo: VT_BOOL<br /><br /> Leitura/gravação: leitura<br /><br /> Padrão: VARIANT_TRUE<br /><br /> Descrição: usado para determinar se há suporte para o agrupamento de coluna.<br /><br /> VARIANT_TRUE: há suporte ao agrupamento em nível de coluna.<br /><br /> VARIANT_FALSE: não há suporte para o agrupamento em nível de coluna.|  
|SSPROP_UNICODELCID|Tipo: VT_I4 Leitura/gravação: leitura<br /><br /> Descrição: ID da localidade Unicode.<br /><br /> Esta é a localidade usada para classificação de dados Unicode.|  
|SSPROP_UNICODECOMPARISONSTYLE|Tipo: VT_I4 Leitura/gravação: leitura<br /><br /> Descrição: estilo de comparação Unicode.<br /><br /> As opções de classificação usadas para a classificação de dados Unicode.|  
  
 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERSTREAM, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define a seguinte propriedade adicional.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|Tipo: VT_BSTR Leitura/gravação: leitura/gravação<br /><br /> Descrição: o resultado de uma consulta XML FOR pode não ser um documento bem formado. Quando essa propriedade for especificada, o resultado de um ' Selecionar... para XML' consulta é encapsulada na marca raiz fornecida por essa propriedade para retornar um documento XML bem formado. Se a consulta for executada no navegador, ela pode fazer o navegador exibir erros de analisador ao carregar o resultado. Para evitar o erro, o SQL ISAPI dá suporte à palavra-chave ROOT. Essa palavra-chave é mapeada para a propriedade SSPROP_STREAM_XMLROOT.|  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
