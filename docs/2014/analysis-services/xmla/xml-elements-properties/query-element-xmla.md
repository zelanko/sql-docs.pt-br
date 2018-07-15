---
title: Consultar o elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Query Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Query
- microsoft.xml.analysis.query
- http://schemas.microsoft.com/analysisservices/2003/engine#Query
helpviewer_keywords:
- Query element
ms.assetid: 5a4544e4-012f-4a47-942c-23596400ea16
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 02feb5cb14e6b6acdc6100070495d0c84b89e483
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293228"
---
# <a name="query-element-xmla"></a>Elemento Query (XMLA)
  Contém uma consulta dentro de [consultas](queries-element-xmla.md) coleção usada pela [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md) comando durante a otimização baseada em uso.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Queries>  
   ...  
   <Query>...</Query>  
   ...  
</Queries>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Consultas](queries-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O comando `DesignAggregations` oferece suporte para a otimização baseada em uso incluindo um ou mais elementos `Query` na coleção `Queries` do comando. Cada `Query` elemento representa uma meta de consulta que usa o processo de design para definir agregações que se destinam às consultas usadas com mais frequência. Você pode especificar suas próprias consultas de meta ou você pode usar as informações armazenadas por uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no log de consultas para recuperar informações sobre com mais frequência as consultas usadas.  
  
 Se você estiver criando agregações iterativamente, você só precisa transmitir as metas de consulta no primeiro `DesignAggregations` o comando porque o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância armazena essas metas e utiliza essas consultas durante subsequentes `DesignAggregations` comandos. Após transmitir as metas de consulta no primeiro comando `DesignAggregations` de um processo iterativo, qualquer comando `DesignAggregations` subsequente que contém metas de consulta na propriedade `Queries` gerará um erro.  
  
 O elemento `Query` contém um valor delimitado por vírgula com os seguintes argumentos:  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *Frequência*  
 Um fator de ponderação que corresponde ao número de vezes que a consulta foi executada previamente. Se o `Query` elemento representa uma nova consulta, o *frequência* valor representa o fator de ponderação usado pelo processo de design para avaliar a consulta. À medida que o valor de frequência fica maior, o peso colocado na consulta durante processo de design aumenta.  
  
 *Conjunto de dados*  
 Uma sequência numérica que especifica quais atributos de uma dimensão devem ser incluídos na consulta. Essa sequência deve ter o mesmo número de caracteres do número de atributos na dimensão. Zero (0) indica que o atributo na posição ordinal especificada não está incluído na consulta para a dimensão especificada e um (1) indica que o atributo na posição ordinal especificada está incluído na consulta para a dimensão especificada.  
  
 Por exemplo, a sequência “011” faz referência a uma consulta que envolve uma dimensão com três atributos, dos quais o segundo e o terceiro estão incluídos na consulta.  
  
> [!NOTE]  
>  Alguns atributos não são considerados no conjunto de dados. Para obter mais informações sobre os atributos excluídos, consulte [Properties (XMLA)](query-element-xmla.md).  
  
 Cada dimensão no grupo de medidas que contém o design de agregação é representado por um *conjunto de dados* o valor de `Query` elemento. A ordem de valores *Dataset* deve coincidir com a ordem de dimensões incluída no grupo de medidas.  
  
## <a name="see-also"></a>Consulte também  
 [Projetando agregações &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
