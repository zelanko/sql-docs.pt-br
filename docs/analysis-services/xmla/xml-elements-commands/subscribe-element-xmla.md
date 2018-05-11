---
title: Elemento Subscribe (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78fb69cc1a9843f4ebbc01711f3e5be5d0146ec6
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="subscribe-element-xmla"></a>Elemento Subscribe (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Assina um rastreamento e retorna um conjunto de linhas que contém os eventos de rastreamento de um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O **assinar** comando assina e devolve um conjunto de linhas de um rastreamento especificado em um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. Se um objeto que não seja um rastreamento for especificado no elemento **Object** , ocorrerá um erro.  
  
 Se o **objeto** elemento não for especificado, um rastreamento de sessão é definido e assinado na [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. O rastreamento de sessão retorna um conjunto fixo de eventos de rastreamento da sessão atual.  
  
 O fluxo do conjunto de linhas retornado por este comando será finalizado se o aplicativo cliente fecha a conexão para o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância, ou se a sessão na qual o **assinar** comando é executado é encerrada.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
