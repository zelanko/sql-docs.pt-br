---
title: Criando grupos de hierarquias recursivas (Construtor de Relatórios e SSRS) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 14eb29f4e5390a92118ddb97bab908d8c6c1a1d2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169192"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>Criando grupos de hierarquias recursivas (Construtor de Relatórios e SSRS)
  Para exibir dados recursivos onde o relacionamento entre pai e filho é representado por campos no conjunto de dados, você pode definir a expressão de grupo da região de dados com base no campo filho e defina a propriedade Parent com base no campo pai.  
  
 Exibir dados hierárquicos é um uso comum dos grupos de hierarquias recursivas (por exemplo, funcionários em um organograma). O conjunto de dados inclui uma lista de funcionários e gerentes, em que os nomes de gerentes também aparecem na lista de funcionários.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>Criando hierarquias recursivas  
 Para criar uma hierarquia recursiva em uma região de dados tablix, você deve definir a expressão de grupo como o campo que especifica os dados filho e a propriedade Parent do grupo como o campo que especifica os dados pai. Por exemplo, no caso de um conjunto de dados que inclui campos ID de funcionário e ID de gerente em que os funcionários estão subordinados aos gerentes, defina a expressão de grupo como ID de funcionário e a propriedade Parent como ID de gerente.  
  
 Um grupo definido como hierarquia recursiva (isto é, um grupo que usa a propriedade Parent) só pode ter uma expressão de grupo. É possível usar a função `Level` no preenchimento da caixa de texto para recuar os nomes de funcionários conforme seu nível na hierarquia.  
  
 Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) e [Criar um grupo de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md).  
  
### <a name="aggregate-functions-that-support-recursion"></a>Funções de agregação compatíveis com recursão  
 Você pode usar as funções de agregação do Reporting Services que aceitam o parâmetro *Recursive* para calcular dados resumidos de uma hierarquia recursiva. As seguintes funções aceitam `Recursive` como um parâmetro: [soma](report-builder-functions-sum-function.md), [Avg](report-builder-functions-avg-function.md), [contagem](report-builder-functions-count-function.md), [CountDistinct](report-builder-functions-countdistinct-function.md), [ CountRows](report-builder-functions-countrows-function.md), [máx](report-builder-functions-max-function.md), [Min](report-builder-functions-min-function.md), [StDev](report-builder-functions-stdev-function.md), [StDevP](report-builder-functions-stdevp-function.md), [soma](report-builder-functions-sum-function.md), [Var](report-builder-functions-var-function.md), e [VarP](report-builder-functions-varp-function.md). Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Referência de funções de agregação &#40;relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
