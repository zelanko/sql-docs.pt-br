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
ms.openlocfilehash: 15f930695e13d824e70da748dad20cf574e9bc38
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579138"
---
# <a name="xml-elements---methods"></a>Elementos XML - métodos
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  O protocolo XML for Analysis (XMLA) usa dois métodos, **Discover** e **Execute**, para oferecer uma maneira padronizada de aplicativos para acessar informações em uma instância do Analysis Services. Uma vez que esses métodos são chamados usando o protocolo SOAP, eles aceitam a entrega e entregam a saída em XML. Analysis Services implementa ambos os métodos, em conformidade com a especificação XML for Analysis 1.1.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir descrevem os métodos XMLA implementados pelo Analysis Services.  
  
|Método|Description|  
|------------|-----------------|  
|[Método Discover &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|Recupera informações, como a lista de bancos de dados disponíveis ou detalhes sobre um objeto específico, de uma instância do Analysis Services. Os dados recuperados com o método **Discover** dependem dos valores dos parâmetros configurados.|  
|[Método Execute &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|Envia comandos XMLA para uma instância do Analysis Services. Isso inclui solicitações que envolvem transferência de dados, como a recuperação ou a atualização dos dados no servidor.|  
  
## <a name="see-also"></a>Confira também
 [Elementos XML &#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Tipos de dados XML &#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
