---
title: Métodos (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f42c986f8ebb3be2126335663a0716049e908ab0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="xml-elements---methods"></a>Elementos XML - métodos
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  O protocolo XML for Analysis (XMLA) usa dois métodos, **Discover** e **Execute**, para oferecer uma maneira padronizada de aplicativos para acessar informações em uma instância de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Uma vez que esses métodos são chamados usando o protocolo SOAP, eles aceitam a entrega e entregam a saída em XML. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa ambos os métodos, em conformidade com a especificação XML for Analysis 1.1.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir descrevem os métodos XMLA implementados por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Método|Description|  
|------------|-----------------|  
|[Método Discover &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|Recupera informações, como a lista de banco de dados disponíveis ou detalhes de um objeto específico, de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os dados recuperados com o método **Discover** dependem dos valores dos parâmetros configurados.|  
|[Método Execute &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|Envia comandos XMLA para uma instância de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Isso inclui solicitações que envolvem transferência de dados, como a recuperação ou a atualização dos dados no servidor.|  
  
## <a name="see-also"></a>Consulte também  
 [Elementos XML & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Tipos de dados XML & #40; XMLA & #41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
