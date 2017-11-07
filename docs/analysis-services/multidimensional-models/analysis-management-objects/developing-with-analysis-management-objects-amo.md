---
title: "Desenvolvendo com objetos de gerenciamento de análise (AMO) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, programming
- AMO, programming
ms.assetid: 91354fc9-22da-4724-b97f-3b1e7b0e69d3
caps.latest.revision: 47
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f746ed6c0ad7dc9c0702282f7a508d44cca7f8be
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="developing-with-analysis-management-objects-amo"></a>Desenvolvendo com Objetos de Gerenciamento de Análise (AMO)
Analysis Management Objects (AMO) é a biblioteca completa de objetos programaticamente acessados que permite que um aplicativo gerenciar uma instância em execução de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].

Esta seção explica conceitos de AMO, concentrando-se nos objetos principais, como e quando usá-los, e a forma como eles se inter-relacionam. Para obter mais informações sobre objetos ou classes específicos, consulte:

- [Namespace Microsoft. AnalysisServices](http://msdn.microsoft.com/library/microsoft.analysisservices.aspx), para obter a documentação de referência
- [Analysis Services Management Objects (AMO)](http://www.bing.com/search?q=Analysis+Services+Management+Objects+%28AMO%29), como uma pesquisa geral Bing.com.


 **Novo no SQL Server 2016**

No SQL Server 2016, o AMO é refatorado em vários assemblies. Classes genéricas, como servidor, banco de dados e funções estão no **AnalysisServices** Namespace. APIs específicas multidimensional permanecem no [Namespace Microsoft. AnalysisServices](https://msdn.microsoft.com/library/ms146720.aspx).

Scripts personalizados e aplicativos desenvolvidos em versões anteriores do AMO continuarão a funcionar sem modificação. No entanto, se você tiver scripts ou aplicativos de destino do SQL Server 2016 especificamente, ou se você precisar recriar uma solução personalizada, certifique-se de adicionar o novo assembly e o namespace ao seu projeto.

## <a name="see-also"></a>Consulte também
[Desenvolvendo com o Analysis Services Scripting Language &#40; ASSL &#41; ](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md) 
 [Desenvolvendo com XMLA no Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)

