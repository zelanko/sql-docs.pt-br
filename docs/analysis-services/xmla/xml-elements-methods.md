---
title: "Métodos (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
f1_keywords: http://schemas.microsoft.com/analysisservices/2003/engine#
helpviewer_keywords:
- methods [XML for Analysis]
- XML for Analysis, methods
- XMLA, methods
ms.assetid: c6768dd4-ca06-4a85-93b7-5fd5700886ad
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7adec520de671a643eed87a5fcda9419b9f6bfa5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="xml-elements---methods"></a>Elementos XML - métodos
  O protocolo XML for Analysis (XMLA) usa dois métodos, **Discover** e **Execute**, para oferecer uma maneira padronizada de aplicativos para acessar informações em uma instância de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Uma vez que esses métodos são chamados usando o protocolo SOAP, eles aceitam a entrega e entregam a saída em XML. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa ambos os métodos, em conformidade com a especificação XML for Analysis 1.1.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir descrevem os métodos XMLA implementados por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Método|Description|  
|------------|-----------------|  
|[Descobrir o método &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|Recupera informações, como a lista de banco de dados disponíveis ou detalhes de um objeto específico, de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os dados recuperados com o método **Discover** dependem dos valores dos parâmetros configurados.|  
|[Executar método &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|Envia comandos XMLA para uma instância de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Isso inclui solicitações que envolvem transferência de dados, como a recuperação ou a atualização dos dados no servidor.|  
  
## <a name="see-also"></a>Consulte também  
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Tipos de dados XML &#40; XMLA &#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
