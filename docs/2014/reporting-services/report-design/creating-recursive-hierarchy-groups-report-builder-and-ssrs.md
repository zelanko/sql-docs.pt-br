---
title: Criando grupos de hierarquias recursivas (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea704f5ec6ab26db37bb56b86a42605ab50dd48b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106114"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>Criando grupos de hierarquias recursivas (Construtor de Relatórios e SSRS)
  Para exibir dados recursivos em que a relação entre pai e filho é representada por campos no conjunto de dados, você pode definir a expressão do grupo de região de dado com base no campo filho e definir a propriedade Parent com base no campo pai.  
  
 Exibir dados hierárquicos é um uso comum dos grupos de hierarquias recursivas (por exemplo, funcionários em um organograma). O conjunto de dados inclui uma lista de funcionários e gerentes, em que os nomes de gerentes também aparecem na lista de funcionários.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>Criando hierarquias recursivas  
 Para criar uma hierarquia recursiva em uma região de dados tablix, você deve definir a expressão de grupo como o campo que especifica os dados filho e a propriedade Parent do grupo como o campo que especifica os dados pai. Por exemplo, no caso de um conjunto de dados que inclui campos ID de funcionário e ID de gerente em que os funcionários estão subordinados aos gerentes, defina a expressão de grupo como ID de funcionário e a propriedade Parent como ID de gerente.  
  
 Um grupo definido como hierarquia recursiva (isto é, um grupo que usa a propriedade Parent) só pode ter uma expressão de grupo. É possível usar a função `Level` no preenchimento da caixa de texto para recuar os nomes de funcionários conforme seu nível na hierarquia.  
  
 Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) e [Criar um grupo de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md).  
  
### <a name="aggregate-functions-that-support-recursion"></a>Funções de agregação compatíveis com recursão  
 Você pode usar as funções de agregação do Reporting Services que aceitam o parâmetro *Recursive* para calcular dados resumidos de uma hierarquia recursiva. As funções a seguir `Recursive` aceitam como um parâmetro: [sum](report-builder-functions-sum-function.md), [AVG](report-builder-functions-avg-function.md), [Count](report-builder-functions-count-function.md), [CountDistinct](report-builder-functions-countdistinct-function.md), [COUNTROWS](report-builder-functions-countrows-function.md), [Max](report-builder-functions-max-function.md), [min](report-builder-functions-min-function.md), [Desv](report-builder-functions-stdev-function.md), [DESVPADP](report-builder-functions-stdevp-function.md), [sum](report-builder-functions-sum-function.md), [var](report-builder-functions-var-function.md)e [VARP](report-builder-functions-varp-function.md). Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
