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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6defada32a68472e4578cff1622288c973399118
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707438"
---
# <a name="data-source-information-properties"></a>Propriedades de informações da fonte de dados
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
 [Objetos de fonte de dados &#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
