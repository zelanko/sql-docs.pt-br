---
title: Criando grupos de hierarquias recursivas (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 92412bbde8a1032b34264ca254560f31704281e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63135581"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>Criando grupos de hierarquias recursivas (construtor de relatórios e SSRS)
  Para exibir dados recursivos onde o relacionamento entre pai e filho é representado por campos no conjunto de dados, você pode definir a expressão de grupo da região de dados com base no campo filho e defina a propriedade Parent com base no campo pai.  
  
 Exibir dados hierárquicos é um uso comum para grupos de hierarquia recursiva, por exemplo, os funcionários em um organograma. O conjunto de dados inclui uma lista de funcionários e gerentes, em que os nomes de gerentes também aparecem na lista de funcionários.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>Criando hierarquias recursivas  
 Para criar uma hierarquia recursiva em uma região de dados tablix, você deve definir a expressão de grupo para o campo que especifica os dados filho e a propriedade pai do grupo para o campo que especifica os dados pai. Por exemplo, um conjunto de dados que inclui campos ID de funcionário e ID de gerente em que os funcionários estão subordinados aos gerentes, defina a expressão de grupo para ID de funcionário e a propriedade pai para o Gerenciador de ID.  
  
 Um grupo que é definido como uma hierarquia recursiva (isto é, um grupo que usa a propriedade Parent) pode ter apenas uma expressão de grupo. Você pode usar o `Level` função no preenchimento da caixa de texto para recuar os nomes de funcionário com base em seu nível na hierarquia.  
  
 Para obter mais informações, consulte [adicionar ou excluir um grupo em uma região de dados &#40;construtor de relatórios e SSRS&#41; ](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) e [criar um grupo de hierarquia recursiva &#40;construtor de relatórios e SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md).  
  
### <a name="aggregate-functions-that-support-recursion"></a>Funções de agregação que oferece suporte à recursão  
 Você pode usar as funções de agregação do Reporting Services que aceitam o parâmetro *recursiva* para calcular dados resumidos de uma hierarquia recursiva. As seguintes funções aceitam `Recursive` como um parâmetro: [Soma](report-builder-functions-sum-function.md), [Avg](report-builder-functions-avg-function.md), [contagem](report-builder-functions-count-function.md), [CountDistinct](report-builder-functions-countdistinct-function.md), [CountRows](report-builder-functions-countrows-function.md), [Max](report-builder-functions-max-function.md), [Mín](report-builder-functions-min-function.md), [StDev](report-builder-functions-stdev-function.md), [StDevP](report-builder-functions-stdevp-function.md), [Sum](report-builder-functions-sum-function.md), [Var](report-builder-functions-var-function.md), e [VarP](report-builder-functions-varp-function.md) . Para obter mais informações, consulte [referência de funções de agregação &#40;construtor de relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas, matrizes e listas de &#40;relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Região de dados Tablix &#40;relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Referência de funções de agregação &#40;relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [Tabelas &#40;relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Lista &#40;relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas de &#40;relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
