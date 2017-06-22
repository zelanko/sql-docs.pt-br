---
title: "Exemplos de expressões (construtor de relatórios e SSRS) de grupo | Microsoft Docs"
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
helpviewer_keywords:
- data [Reporting Services], grouping
- grouping data
- expressions [Reporting Services], adding
- groups [Reporting Services], expressions
ms.assetid: 34cd0249-fc74-4cf2-ba11-7b072992bfd2
caps.latest.revision: 24
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cbb4f5f3af2a8986fdc7384ad4da1740f2be6638
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="group-expression-examples-report-builder-and-ssrs"></a>Exemplos de expressões de grupo (Construtor de Relatórios e SSRS)
  Em uma região de dados, você pode agrupar dados por um único campo ou criar expressões mais complexas que identifiquem os dados nos quais deve ser feito o agrupamento. Expressões complexas incluem referências a vários campos ou parâmetros, instruções condicionais ou código personalizado. Quando você define um grupo para uma região de dados, você adiciona essas expressões às propriedades **Group** . Para obter mais informações, consulte [Adicionar ou excluir um grupo em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
 Para mesclar dois ou mais grupos baseados em expressões de campo simples, adicione cada campo à lista de expressões de grupo na definição do grupo.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="examples-of-group-expressions"></a>Exemplos de expressões de grupo  
 A tabela a seguir fornece exemplos de expressões de grupo que podem ser usadas para definir um grupo.  
  
|Description|Expressão|  
|-----------------|----------------|  
|Agrupar pelo campo `Region` .|`=Fields!Region.Value`|  
|Agrupar por sobrenome e nome.|`=Fields!LastName.Value`<br /><br /> `=Fields!FirstName.Value`|  
|Agrupar pela primeira letra do sobrenome.|`=Fields!LastName.Value.Substring(0,1)`|  
|Agrupar pelo parâmetro, baseado na seleção do usuário.<br /><br /> Neste exemplo, o parâmetro `GroupBy` deve ser baseado em uma lista de valores disponíveis que fornece uma opção válida na qual deve ser feito o agrupamento.|`=Fields(Parameters!GroupBy.Value).Value`|  
|Agrupar por três faixas etárias separadas:<br /><br /> "Menos de 21", "Entre 21 e 50" e "Mais de 50".|`=IIF(First(Fields!Age.Value)<21,"Under 21",(IIF(First(Fields!Age.Value)>=21 AND First(Fields!Age.Value)<=50,"Between 21 and 50","Over 50")))`|  
|Agrupar por muitas faixas etárias. Este exemplo mostra o código personalizado, escrito em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET, que retorna uma cadeia para as seguintes faixas:<br /><br /> 25 ou menos<br /><br /> 26 a 50<br /><br /> 51 a 75<br /><br /> Mais de 75|`=Code.GetRangeValueByAge(Fields!Age.Value)`<br /><br /> Código personalizado:<br /><br /> `Function GetRangeValueByAge(ByVal age As Integer) As String`<br /><br /> `Select Case age`<br /><br /> `Case 0 To 25`<br /><br /> `GetRangeValueByByAge = "25 or Under"`<br /><br /> `Case 26 To 50`<br /><br /> `GetRangeValueByByAge = "26 to 50"`<br /><br /> `Case 51 to 75`<br /><br /> `GetRangeValueByByAge = "51 to 75"`<br /><br /> `Case Else`<br /><br /> `GetRangeValueByByAge = "Over 75"`<br /><br /> `End Select`<br /><br /> `Return GetRangeValueByByAge`<br /><br /> `End Function`|  
  
## <a name="see-also"></a>Consulte também  
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)  
  
  
