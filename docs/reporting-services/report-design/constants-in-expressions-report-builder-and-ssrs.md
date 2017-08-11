---
title: "Constantes em expressões (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b8ae650b-0f46-4848-b62b-15f8a40751b8
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fbfeefbf5cf8bc3db1f467353de3c5bf3c8b0178
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="constants-in-expressions-report-builder-and-ssrs"></a>Constantes em expressões (Construtor de Relatórios e SSRS)
  Uma constante consiste em texto literal ou texto predefinido. O processador de relatório tem acesso às constantes predefinidas; portanto, quando elas são incluídas em uma expressão, os valores que elas representam são substituídos na expressão antes de ela ser avaliada.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="literal-text"></a>Texto literal  
 Em uma expressão, texto literal é o texto que está entre aspas duplas. Você também poderá digitar o texto diretamente em uma caixa de texto sem aspas duplas, se ele não fizer parte de uma expressão. Se o valor da caixa de texto não começar com um sinal de igual (=), o texto será tratado como texto literal. A tabela a seguir mostra vários exemplos de texto literal em uma expressão.  
  
|Constante|Texto de exibição|Texto de expressão|  
|--------------|------------------|---------------------|  
|Execução do relatório em:|<\<Expr >>|`="Report run at: " & Globals!ExecutionTime`|  
|Ciclos da Adventure Works|Ciclos da Adventure Works|Ciclos da Adventure Works|  
|[Texto de exibição entre colchetes]|\\[Texto de exibição entre colchetes\\]|[Texto de exibição entre colchetes]|  
  
## <a name="rdl-constants"></a>Constantes RDL  
 É possível usar constantes definidas em linguagem RDL (Report Definition Language) em uma expressão. Na caixa de diálogo **Expressão** , as constantes são exibidas quando você cria uma expressão para uma propriedade de relatório que aceita apenas determinados valores válidos, também conhecidos como tipos enumerados. A tabela a seguir mostra dois exemplos.  
  
|Propriedade|Description|Valores|  
|--------------|-----------------|------------|  
|TextAlign|Valores válidos para alinhamento de texto em uma caixa de texto.|Geral, À Esquerda, Centralizado, À Direita|  
|BorderStyle|Valores válidos para uma linha adicionada a um relatório.|Padrão, Nenhum, Pontilhado, Tracejado, Sólido, Duplo, TraçoPonto, TraçoPontoPonto|  
  
## <a name="visual-basic-constants"></a>Constantes do Visual Basic  
 É possível usar constantes definidas na biblioteca de tempo de execução [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] em uma expressão. Por exemplo, você pode usar a constante **DateInterval.Day**. A seguinte expressão para a data de 10 de janeiro de 2008 retorna o número 10:  
  
 `=DatePart("d",Globals!ExecutionTime)`  
  
## <a name="clr-constants"></a>Constantes CLR  
 É possível usar constantes definidas nas classes CLR (Common Language Runtime) [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] em uma expressão. A tabela a seguir mostra um exemplo de uma cor definida pelo sistema.  
  
|Constante|Description|  
|--------------|-----------------|  
|MistyRose|Ao criar uma expressão para uma propriedade do relatório baseada na cor do plano de fundo, é possível especificar uma cor pelo nome. Os nomes válidos são listados na caixa de diálogo **Expressão** .|  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo expressão](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [Expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Caixa de diálogo expressão &#40; Construtor de relatórios &#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
