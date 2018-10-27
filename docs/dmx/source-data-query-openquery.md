---
title: OPENQUERY (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 895c28f0989debb899c1e01c80a18483d3cda5a1
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147811"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;consulta de fonte de dados&gt; -OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Substitui uma consulta de dados de origem por uma consulta em uma fonte de dados existente. As instruções INSERT, SELECT FROM PREDICTION JOIN e SELECT FROM NATURAL PREDICTION JOIN oferecem suporte a **OPENQUERY**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *fonte de dados nomeado*  
 Uma fonte de dados que existe na [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados.  
  
 *sintaxe de consulta*  
 Sintaxe de consulta que retorna um conjunto de linhas.  
  
## <a name="remarks"></a>Comentários  
 **OPENQUERY** fornece uma maneira mais segura para acessar dados externos, oferecendo suporte a permissões de fonte de dados. Como a cadeia de conexão é armazenada na fonte de dados, os administradores podem usar as propriedades da fonte de dados para gerenciar o acesso aos dados. Para obter mais informações sobre fontes de dados, consulte [fontes de dados com suporte &#40;SSAS - Multidimensional&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
 Você pode obter uma lista das fontes de dados que estão disponíveis em um servidor consultando as **MDSCHEMA_INPUT_DATASOURCES** linhas de esquema. Para obter mais informações sobre como usar **MDSCHEMA_INPUT_DATASOURCES**, consulte [de linhas MDSCHEMA_INPUT_DATASOURCES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset).  
  
 Também é possível retornar uma lista das fontes de dados no banco de dados atual do Analysis Services usando a seguinte consulta DMX:  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a fonte de dados MyDS já definida a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados para criar uma conexão para o [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] banco de dados e consulta o **vTargetMail** exibição.  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>Consulte também  
 [&#60;consulta de fonte de dados&#62;](../dmx/source-data-query.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
