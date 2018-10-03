---
title: Bloquear elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Lock Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Lock
- microsoft.xml.analysis.lock
- http://schemas.microsoft.com/analysisservices/2003/engine#Lock
helpviewer_keywords:
- Lock command
ms.assetid: a819e805-4793-43bb-8af3-16a19f8bdab3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aee5d603c2708cb42b666d3cc0c9acc5ea208f0b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079516"
---
# <a name="lock-element-xmla"></a>Elemento Lock (XMLA)
  Bloqueia um objeto especificado em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Lock>  
      <ID>...</ID>  
      <Object>...</Object>  
      <Mode>...</Mode>  
   </Lock>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[ID](../xml-elements-properties/id-element-xmla.md), [modo](../xml-elements-properties/mode-element-xmla.md), [objeto](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O comando `Lock` bloqueia um objeto, para uso compartilhado ou exclusivo, no contexto da transação ativa no momento. Apenas administradores de banco de dados ou de servidor podem emitir um comando `Lock` explicitamente. Um bloqueio em um objeto impede a confirmação de transações até que o bloqueio seja removido. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oferece suporte a dois tipos de bloqueios, bloqueios compartilhados e bloqueios exclusivos. Para obter mais informações sobre os tipos de bloqueio com suporte [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [elemento Mode &#40;XMLA&#41;](../xml-elements-properties/mode-element-xmla.md).  
  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] permite apenas o bloqueio de bancos de dados. O elemento `Object` deve conter uma referência de objeto a um banco de dados [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Se o `Object` não for especificado ou se o `Object` elemento se refere a um objeto diferente de um banco de dados, ocorrerá um erro.  
  
 Outros comandos emitem um comando `Lock` implicitamente em um banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Qualquer operação que leia dados ou metadados em um banco de dados, por exemplo, qualquer método `Discover` ou um método `Execute` que esteja executando um comando `Statement`, emite implicitamente um bloqueio compartilhado no banco de dados. Qualquer transação que confirme alterações em dados ou metadados em um objeto de um banco de dados [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], por exemplo, um método `Execute` que esteja executando um comando `Alter`, emite implicitamente um bloqueio exclusivo no banco de dados.  
  
 Todos os bloqueios são mantidos no contexto da transação atual. Quando a transação atual é confirmada ou revertida, todos os bloqueios definidos dentro da transação são liberados automaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Desbloquear elemento &#40;XMLA&#41;](lock-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
