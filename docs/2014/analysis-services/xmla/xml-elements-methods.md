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
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: fe42e2330e3e108ad1ee0e09d1e1e1007eda9102
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130828"
---
# <a name="methods-xmla"></a>Métodos (XMLA)
  O protocolo XML for Analysis (XMLA) usa dois métodos, `Discover` e `Execute`, para oferecer uma maneira padronizada de aplicativos para acessar informações em uma instância de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Uma vez que esses métodos são chamados usando o protocolo SOAP, eles aceitam a entrega e entregam a saída em XML. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa ambos os métodos, em conformidade com a especificação XML for Analysis 1.1.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir descrevem os métodos XMLA implementados por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Método|Description|  
|------------|-----------------|  
|[Método Discover &#40;XMLA&#41;](xml-elements-methods-discover.md)|Recupera informações, como a lista de banco de dados disponíveis ou detalhes de um objeto específico, de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os dados recuperados com o método `Discover` dependem dos valores dos parâmetros configurados.|  
|[Método Execute &#40;XMLA&#41;](xml-elements-methods-execute.md)|Envia comandos XMLA para uma instância de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Isso inclui solicitações que envolvem transferência de dados, como a recuperação ou a atualização dos dados no servidor.|  
  
## <a name="see-also"></a>Consulte também  
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Tipos de dados XML &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  