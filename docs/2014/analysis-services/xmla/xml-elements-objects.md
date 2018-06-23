---
title: Objetos (XMLA) | Microsoft Docs
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
helpviewer_keywords:
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, objects
ms.assetid: 768188ef-85d4-432a-9390-be05c835137f
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 98ff50749cc45b5ffe4343acc19668f4dd0db126
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009417"
---
# <a name="objects-xmla"></a>Objetos (XMLA)
  O protocolo XML for Analysis (XMLA) usa dois métodos, `Discover` e `Execute`, para oferecer uma maneira padronizada de aplicativos para acessar informações em uma instância de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Uma vez que esses métodos são chamados usando o protocolo SOAP, eles aceitam a entrada e entregam a saída em XML.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos a seguir descrevem os objetos XMLA implementados por [!INCLUDE[ssAS](../../includes/ssas-md.md)].  
  
|Método|Description|  
|------------|-----------------|  
|[Elemento DiscoverResponse &#40;XMLA&#41;](xml-elements-objects-discoverresponse.md)|Contém as informações retornadas por uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em resposta a um [Discover](xml-elements-methods-discover.md) chamada de método.|  
|[Elemento ExecuteResponse &#40;XMLA&#41;](xml-elements-objects-executeresponse.md)|Contém as informações retornadas por uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em resposta a um [Execute](xml-elements-methods-execute.md) chamada de método.|  
  
## <a name="see-also"></a>Consulte também  
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Tipos de dados XML &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  