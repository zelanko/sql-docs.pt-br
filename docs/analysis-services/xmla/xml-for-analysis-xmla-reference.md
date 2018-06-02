---
title: XML for Analysis (XMLA) referência | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e8c3645175d8d1f3251fd621825f5a542669cbb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576758"
---
# <a name="xml-for-analysis--xmla-reference"></a>XML for Analysis (XMLA) referência
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]   

Azure Analysis Services e SQL Server Analysis Services usam XML para o protocolo de análise (XMLA) para comunicações entre aplicativos cliente e uma instância do Analysis Services. No seu nível mais básico, outras bibliotecas de cliente como o ADOMD.NET e AMO constroem solicitações e decodificam respostas no XMLA, servindo como um intermediário a uma instância do Analysis Services, que usa XMLA exclusivamente.  
  
 Para dar suporte à descoberta e manipulação de dados nos modos de tabela e multidimensionais, a especificação XMLA define dois métodos geralmente acessíveis, [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) e [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)e um coleção de tipos de dados e elementos XML. Uma vez que o XML permite uma arquitetura de cliente e servidor livremente acoplada, ambos os métodos controlam as informações de entrada e saída no formato XML. 

O Analysis Services é compatível com a especificação XMLA 1.1, especificação, mas também estende-o para incluir a capacidade de definição e manipulação de dados, implementada como anotações no **Discover** e **Execute** métodos. As sintaxes XML estendidas são a linguagem de script de modelo Tabular (TMSL) e o Analysis Services Scripting Language (ASSL). 

O TMSL é a sintaxe de definição de modelo de comando e o objeto para bancos de dados de modelo de tabela no nível de compatibilidade 1200 e superior. O TMSL se comunica com o Analysis Services por meio do protocolo XMLA, onde o `XMLA.Execute` método aceita os dois scripts de instrução com base em JSON em TMSL, bem como os scripts tradicionais baseado em XML no Analysis Services Scripting Language (ASSL para XMLA). Para obter mais informações, consulte [referência de linguagem de script de modelo Tabular (TMSL)](../tabular-model-scripting-language-tmsl-reference.md).

ASSL é a sintaxe de definição de modelo de comando e o objeto para bancos de dados de modelo multidimensional e modo de tabela no nível de compatibilidade 1103 ou inferior. Essa definição se baseia a especificação XMLA sem quebrá-la. A interoperabilidade baseada em XMLA é assegurada se você usar somente XMLA, ou XMLA e ASSL juntos. Para obter mais informações, consulte [Analysis Services Scripting Language (ASSL para XMLA)](../scripting/analysis-services-scripting-language-assl-for-xmla.md).
  
 Como desenvolvedor, você pode usar o XMLA como uma interface se os requisitos de solução especificarem protocolos padrão, como XML, SOAP e HTTP. Desenvolvedores e administradores também podem usar XMLA em uma base ad hoc para recuperar informações do servidor ou executar comandos. 
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Tipos de dados XML (XMLA)](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)|Descreve tipos de dados na especificação XMLA.|  
|[Elementos XML - comandos (XMLA)](../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)|Elementos que podem ser usados dentro do elemento de comando durante uma chamada de método de execução.|  
|[Elementos XML - comandos (XMLA)](../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)|Elementos que podem ser usados dentro do elemento de comando durante uma chamada de método de execução.|  
|[Elementos XML - cabeçalhos (XMLA)](../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)| Elementos de cabeçalho implementados pelo Microsoft Analysis Services.|  
|[Elementos XML - propriedades (XMLA)](../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)| Elementos para representar informações de propriedade e valores para XMLA cabeçalhos, métodos, objetos, comandos e tipos de dados.|  
|[Elementos XML - métodos - Discover (XMLA)](../../analysis-services/xmla/xml-elements-methods-discover.md)| Recupera informações, como a lista de bancos de dados disponíveis ou detalhes sobre um objeto específico, de uma instância do Analysis Services.|  
|[Elementos XML - métodos - Execute (XMLA)](../../analysis-services/xmla/xml-elements-methods-execute.md)| Envia o XML para comandos Analysis (XMLA) para uma instância do Analysis Services.|  
|[XML elementos - objetos - DiscoverResponse (XMLA)](../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)| Contém as informações retornadas por uma instância do Analysis Services em resposta a uma chamada de método de descoberta.|  
|[XML elementos - objetos - ExecuteResponse (XMLA)](../../analysis-services/xmla/xml-elements-objects-executeresponse.md)| Contém as informações retornadas por uma instância do Analysis Services em resposta a uma chamada de método de execução.|  
|[Elementos XML - objetos (XMLA)](../../analysis-services/xmla/xml-elements-objects.md)| Objetos implementados pelo Analysis Services.|  
|[Conformidade com XMLA (XML for Analysis)](../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)|Descreve o nível de conformidade com a especificação do XMLA 1.1.|  
  
## <a name="see-also"></a>Confira também
 [Conjunto de linhas de esquema do XML](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
 [Desenvolvendo com ADOMD.NET](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
 [Desenvolvendo com AMO &#40;Objetos de Gerenciamento de Análise&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
