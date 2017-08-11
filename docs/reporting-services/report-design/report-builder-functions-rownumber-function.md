---
title: "Função RowNumber (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 25084e7140855c6535ef6432afdc09bee02a23e6
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---rownumber-function"></a>Relatório de funções de construtor - função RowNumber
  Retorna uma contagem contínua do número de linhas para o escopo especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *escopo*  
 (**String**) O nome de um conjunto de dados, região de dados ou grupo ou nulo (**Nothing** no [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica o contexto no qual avaliar o número de linhas. **Nothing** especifica o contexto mais externo, geralmente o conjunto de dados do relatório.  
  
## <a name="remarks"></a>Comentários  
 O**RowNumber** retorna um valor em uso da contagem de linhas dentro do escopo especificado, assim como [RunningValue](../../reporting-services/report-design/report-builder-functions-runningvalue-function.md) retorna o valor em uso de uma função de agregação. Ao especificar um escopo, você especifica quando redefinir a contagem de linhas como 1.  
  
 O*scope* não pode ser uma expressão. *scope* deve ser um escopo contentor. Escopos típicos, do confinamento mais externo ao mais interno, são conjuntos de dados de relatório, região de dados, grupos de linhas ou grupos de colunas.  
  
 Para incrementar valores entre colunas, especifique um escopo que seja o nome de um grupo de colunas. Para incrementar números em baixo das linhas, especifique um escopo que seja o nome de um grupo de linhas.  
  
> [!NOTE]  
>  Não há suporte para a inclusão de agregações que especificam um grupo de linhas e um grupo de colunas em uma única expressão.  
  
 Para obter mais informações, consulte [Referência de funções agregadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="code-example"></a>Exemplo de código  
 A expressão a seguir pode ser usada para a propriedade **BackgroundColor** de uma linha de detalhes da região de dados Tablix para alternar a cor das linhas de detalhes de cada grupo, sempre começando com Branco.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Uso de expressões em relatórios &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
