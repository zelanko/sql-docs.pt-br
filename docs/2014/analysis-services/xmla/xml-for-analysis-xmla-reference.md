---
title: Referência XML for Analysis (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, reference
- XMLA, reference
ms.assetid: 88045e05-ce47-4e28-999b-7f9c74af9faf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fde04360c7b6af1c9bf6aa906328e5031eb76c32
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164436"
---
# <a name="xml-for-analysis--xmla-reference"></a>Referência XML for Analysis (XMLA)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa o protocolo XML for Analysis (XMLA) para lidar com toda a comunicação entre aplicativos cliente e uma instância do Analysis Services. No seu nível mais básico, outras bibliotecas de cliente como o ADOMD.NET e AMO constroem solicitações e decodificam respostas no XMLA, servindo como um intermediário a uma instância do Analysis Services, que usa XMLA exclusivamente.  
  
 Para dar suporte à descoberta e manipulação de dados nos formatos multidimensionais e tabulares, a especificação XMLA define dois métodos geralmente acessíveis, [Discover](xml-elements-methods-discover.md) e [Execute](xml-elements-methods-execute.md)e um coleção de tipos de dados e elementos XML. Uma vez que o XML permite uma arquitetura de cliente e servidor livremente acoplada, ambos os métodos controlam as informações de entrada e saída no formato XML. O Analysis Services é compatível com a especificação XMLA 1.1, mas também estende-o para incluir a definição de dados e o recurso de manipulação, implementado como anotações nos métodos `Discover` e `Execute`. A sintaxe de XML estendida é chamada de ASSL (Analysis Services Scripting Language). O ASSL baseia-se na especificação de XMLA sem quebrá-la. A interoperabilidade baseada em XMLA é assegurada se você usar somente XMLA, ou XMLA e ASSL juntos.  
  
 Como programador, você poderá usar o XMLA como uma interface de programação se os requisitos de solução especificarem protocolos padrão, como XML, SOAP e HTTP. Os programadores e administradores também podem usar XMLA de maneira ad hoc para recuperar informações dos comandos de servidor ou execução.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)|Descreve elementos na especificação XMLA.|  
|[Tipos de dados XML &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)|Descreve tipos de dados na especificação XMLA.|  
|[Conformidade XML for Analysis &#40;XMLA&#41;](xml-for-analysis-compliance-xmla.md)|Descreve o nível de conformidade com a especificação do XMLA 1.1.|  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Desenvolvimento com o Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
  
 [Conjunto de linhas de esquema do XML](../schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 [Desenvolvendo com ADOMD.NET](../multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
 [Desenvolvendo com objetos de gerenciamento de análise &#40;AMO&#41;](../multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre a arquitetura do Microsoft OLAP](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
