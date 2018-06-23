---
title: Função Level (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 3df298cda1e6439d9c539c125689a3687cdc97f8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120516"
---
# <a name="level-function-report-builder-and-ssrs"></a>Função Level (Construtor de Relatórios e SSRS)
  Retorna o nível atual de profundidade em uma hierarquia recursiva.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Level(scope)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *escopo*  
 (`String`) (Opcional). O nome de um conjunto de dados, um grupo ou uma região de dados que contém os itens de relatório aos quais a função de agregação deve ser aplicada. Se *scope* não estiver especificado, será usado o escopo atual.  
  
## <a name="return-type"></a>Tipo de retorno  
 Retorna um `Integer`. Se *escopo* Especifica um conjunto de dados ou região de dados, ou um agrupamento não recursivo (isto é, um agrupamento sem nenhum `Parent` elemento), `Level` retornará 0. Se o *scope* for omitido, ele retornará o nível do escopo atual.  
  
## <a name="remarks"></a>Remarks  
 O valor retornado pela função `Level` é baseado em zero; isto é, o primeiro nível em uma hierarquia é 0.  
  
 A função `Level` pode ser usada para fornecer recuo em uma hierarquia recursiva, como uma lista de funcionários.  
  
 Para obter mais informações sobre hierarquias recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir fornece o nível de linha no grupo de Funcionários:  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressão usa relatórios de &#40;SSRS e construtor de relatórios&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;SSRS e construtor de relatórios&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  