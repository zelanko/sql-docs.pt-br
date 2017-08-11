---
title: "Nível de função (construtor de relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 171842909a300d0c98fca2a26bbf4567810e8e95
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---level-function"></a>Funções do construtor de relatórios - nível de função
  Retorna o nível atual de profundidade em uma hierarquia recursiva.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Level(scope)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *escopo*  
 (**String**) (Opcional). O nome de um conjunto de dados, um grupo ou uma região de dados que contém os itens de relatório aos quais a função de agregação deve ser aplicada. Se *scope* não estiver especificado, será usado o escopo atual.  
  
## <a name="return-type"></a>Tipo de retorno  
 Retorna um **Integer**. Se *scope* especificar um conjunto de dados ou uma região de dados ou especificar um agrupamento não recursivo (ou seja, um agrupamento sem nenhum elemento **Parent** ), **Level** retornará 0. Se o *scope* for omitido, ele retornará o nível do escopo atual.  
  
## <a name="remarks"></a>Comentários  
 O valor retornado pela função **Level** é baseado em zero; isto é, o primeiro nível em uma hierarquia é 0.  
  
 A função **Level** pode ser usada para fornecer recuo em uma hierarquia recursiva, como uma lista de funcionários.  
  
 Para obter mais informações sobre hierarquias recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir fornece o nível de linha no grupo de Funcionários:  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Uso de expressões em relatórios &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
