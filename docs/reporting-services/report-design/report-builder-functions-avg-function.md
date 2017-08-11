---
title: "Função AVG (construtor de relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: f1276c4c-bb44-44c0-a1bf-386a0c340003
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 53e1a61cc39b3aa0b3ef2f6222106ee162529417
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---avg-function"></a>Relatório de funções de construtor - função Avg
Nos relatórios paginados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , ele retorna a média de todos os valores numéricos não nulos especificados pela expressão, avaliados no escopo fornecido.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Avg(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *expressão*  
 (**Float**) A expressão na qual executar a agregação.  
  
 *escopo*  
 (**String**) Opcional. O nome de um conjunto de dados, um grupo ou uma região de dados que contém os itens de relatório aos quais a função de agregação deve ser aplicada. Se *scope* não estiver especificado, será usado o escopo atual.  
  
 *recursivos*  
 (**Enumerated Type**) Opcional. **Simple** (padrão) ou **RdlRecursive**. Especifica se a agregação deve ser executada recursivamente.  
  
## <a name="return-type"></a>Tipo de retorno  
 Retorna um **Decimal** para expressões decimais e um **Double** para todas as outras expressões.  
  
## <a name="remarks"></a>Comentários  
 O conjunto de dados especificado na expressão deve ter o mesmo tipo de dados. Para converter dados que têm vários tipos de dados numéricos no mesmo tipo de dados, use funções de conversão, como **CInt**, **CDbl** ou **CDec**. Para obter mais informações, consulte [Funções de conversão de tipo](http://go.microsoft.com/fwlink/?LinkId=96142).  
  
 O valor de *scope* deve ser uma constante de cadeia de caracteres e não pode ser uma expressão. Para agregações externas ou que não especificam outras agregações, *scope* deve se referir ao escopo atual ou a um escopo contentor. Para agregações de agregações, as agregações aninhadas podem especificar um escopo filho.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   *Scope* para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   *Scope* para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   *Expression* não deve conter a função **First**, **Last**, **Previous**ou **RunningValue** .  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para obter mais informações, consulte [Referência de funções agregadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Exemplo  
 Os dois exemplos de código a seguir fornecem uma média de todos os valores do campo `Cost` contidos em um conjunto de dados denominado `Inventory`.  
  
```  
=Avg(Fields!Cost.Value, "Inventory")   
  OR    
=Avg (CDbl(Fields!Cost.Value), "Inventory")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Uso de expressões em relatórios &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
