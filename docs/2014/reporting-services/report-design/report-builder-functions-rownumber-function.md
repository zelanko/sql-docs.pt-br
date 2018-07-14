---
title: Função RowNumber (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bb6025b8cf196d45fe0a6c9ac5cf0c19aa54013e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37276272"
---
# <a name="rownumber-function-report-builder-and-ssrs"></a>Função RowNumber (Construtor de Relatórios e SSRS)
  Retorna uma contagem contínua do número de linhas para o escopo especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *escopo*  
 (`String`) O nome de um conjunto de dados, região de dados ou grupo ou nulo (`Nothing` em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica o contexto no qual avaliar o número de linhas. `Nothing` Especifica o contexto mais externo, geralmente o conjunto de dados do relatório.  
  
## <a name="remarks"></a>Remarks  
 `RowNumber` Retorna um valor em uso da contagem de linhas dentro do escopo especificado, assim como [RunningValue](report-builder-functions-runningvalue-function.md) retorna o valor em execução de uma função de agregação. Ao especificar um escopo, você especifica quando redefinir a contagem de linhas como 1.  
  
 O*scope* não pode ser uma expressão. *scope* deve ser um escopo contentor. Escopos típicos, do confinamento mais externo ao mais interno, são conjuntos de dados de relatório, região de dados, grupos de linhas ou grupos de colunas.  
  
 Para incrementar valores entre colunas, especifique um escopo que seja o nome de um grupo de colunas. Para incrementar números em baixo das linhas, especifique um escopo que seja o nome de um grupo de linhas.  
  
> [!NOTE]  
>  Não há suporte para a inclusão de agregações que especificam um grupo de linhas e um grupo de colunas em uma única expressão.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="code-example"></a>Exemplo de código  
 A seguir é uma expressão que você pode usar para o `BackgroundColor` propriedade de uma linha de detalhe de região de dados Tablix para alternar a cor das linhas de detalhes para cada grupo, sempre começando com branco.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usos de expressões em relatórios &#40;relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
