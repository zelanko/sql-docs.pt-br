---
title: Elemento Subscribe (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f784cbe3c33eb6b2587b7b535668e793fac3b138
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37973068"
---
# <a name="subscribe-element-xmla"></a>Elemento Subscribe (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Assina um rastreamento e retorna um conjunto de linhas que contém os eventos de rastreamento de uma instância do Analysis Services.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O **Subscribe** comando assina e devolve um conjunto de linhas de um rastreamento específico em um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. Se um objeto que não seja um rastreamento for especificado no elemento **Object** , ocorrerá um erro.  
  
 Se o **objeto** elemento não for especificado, um rastreamento de sessão é definido e assinado na [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. O rastreamento de sessão retorna um conjunto fixo de eventos de rastreamento da sessão atual.  
  
 O fluxo de conjunto de linhas retornado por este comando é encerrado se o aplicativo cliente fechar a conexão para o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância, ou se a sessão na qual o **Subscribe** comando é executado for encerrada.  
  
## <a name="see-also"></a>Confira também
 [Comandos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
