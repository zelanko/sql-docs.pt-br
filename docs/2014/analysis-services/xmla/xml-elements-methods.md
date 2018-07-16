---
title: Métodos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#
helpviewer_keywords:
- methods [XML for Analysis]
- XML for Analysis, methods
- XMLA, methods
ms.assetid: c6768dd4-ca06-4a85-93b7-5fd5700886ad
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1baf254e9965153394a3a7b1367ced21c009a7f4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171417"
---
# <a name="methods-xmla"></a>Métodos (XMLA)
  O protocolo XML for Analysis (XMLA) usa dois métodos, `Discover` e `Execute`, para oferecer uma maneira padronizada de aplicativos para acessar informações em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Uma vez que esses métodos são chamados usando o protocolo SOAP, eles aceitam a entrega e entregam a saída em XML. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa ambos os métodos, em conformidade com a especificação XML for Analysis 1.1.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir descrevem os métodos XMLA implementados por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Método|Description|  
|------------|-----------------|  
|[Descobrir o método &#40;XMLA&#41;](xml-elements-methods-discover.md)|Recupera informações, como a lista de banco de dados disponíveis ou detalhes de um objeto específico, de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os dados recuperados com o método `Discover` dependem dos valores dos parâmetros configurados.|  
|[Executar o método &#40;XMLA&#41;](xml-elements-methods-execute.md)|Envia comandos XMLA para uma instância de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Isso inclui solicitações que envolvem transferência de dados, como a recuperação ou a atualização dos dados no servidor.|  
  
## <a name="see-also"></a>Consulte também  
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Tipos de dados XML &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  
