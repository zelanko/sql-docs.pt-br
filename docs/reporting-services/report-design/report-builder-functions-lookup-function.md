---
title: Função Lookup (Construtor de Relatórios) | Microsoft Docs
description: Use a função Lookup para retornar o primeiro valor correspondente para o nome especificado de um conjunto de dados que contém pares de nome ou valor.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: e60e5bab-b286-4897-9685-9ff12703517d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f2a3016bc45537aed393124b6d20f8d4a1656759
ms.sourcegitcommit: 93e4fd75e8fe0cc85e7949c9adf23b0e1c275465
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2020
ms.locfileid: "84255719"
---
# <a name="report-builder-functions---lookup-function"></a>Funções do Construtor de Relatórios – Função Lookup
  Retorna o primeiro valor correspondente para o nome especificado de um conjunto de dados que contém pares de nome/valor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Lookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *source_expression*  
 (**Variante**) Uma expressão que é avaliada no escopo atual e que especifica o nome ou chave para procurar. Por exemplo, `=Fields!ProdID.Value`.  
  
 *destination_expression*  
 (**Variant**) Uma expressão avaliada para cada linha em um conjunto de dados e que especifica o nome ou a chave para correspondência. Por exemplo, `=Fields!ProductID.Value`.  
  
 *result_expression*  
 (**Variant**) Uma expressão avaliada para a linha do conjunto de dados em que *source_expression* = *destination_expression*e que especifica o valor a ser recuperado. Por exemplo, `=Fields!ProductName.Value`.  
  
 *conjunto de dados*  
 Uma constante que especifica o nome do conjunto de dados no relatório. Por exemplo, "Produtos".  
  
## <a name="return"></a>Retorno  
 Retorna **Variant**ou **Nothing** se não houver correspondência.  
  
## <a name="remarks"></a>Comentários  
 Use **Lookup** para recuperar o valor do conjunto de dados especificado para um par de nome/valor no qual há uma relação de um para um. Por exemplo, para um campo de ID em uma tabela, você pode usar **Lookup** para recuperar todos os números de telefone associados àquele cliente de um conjunto de dados que não esteja associado à região de dados.  
  
 **Lookup** faz o seguinte:  
  
-   Avalia a expressão de origem no escopo atual.  
  
-   Avalia a expressão de destino para cada linha do conjunto de dados especificado depois que foram aplicados filtros, com base na ordenação do conjunto de dados especificado.  
  
-   Na primeira correspondência da expressão de origem e destino, avalia a expressão resultante para aquela linha no conjunto de dados.  
  
-   Retorna o valor da expressão resultante.  
  
 Para recuperar diversos valores para um único nome ou campo de chave em que há uma relação um para muitos, use [Função LookupSet &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookupset-function.md). Para chamar **Lookup** para um conjunto de valores, use [Função Multilookup &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-multilookup-function.md).  
  
 As restrições a seguir se aplicam:  
  
-   **Lookup** é avaliado depois que todas as expressões de filtro são aplicadas.  
  
-   Só um nível de pesquisa tem suporte. Uma expressão de origem, destino ou resultado não pode incluir uma referência a uma função de pesquisa.  
  
-   Expressões de origem e destino devem ser avaliadas como o mesmo tipo de dados. O tipo de retorno é o mesmo que o tipo de dados da expressão resultante avaliada.  
  
-   Expressões de origem, destino e resultado não podem incluir referências a variáveis de relatório ou grupo.  
  
-   **Lookup** não pode ser usado como uma expressão para os seguintes itens de relatório:  
  
    -   Cadeias de conexão dinâmicas para uma fonte de dados.  
  
    -   Campos calculados em um conjunto de dados.  
  
    -   Parâmetros de consulta em um conjunto de dados.  
  
    -   Filtros em um conjunto de dados.  
  
    -   Parâmetros de relatório.  
  
    -   A propriedade Report.Language.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo seguinte, suponha que a tabela esteja associada a um conjunto de dados que inclui um campo para o identificador de produto ProductID. Um conjunto de dados separado chamado "Produto" contém a ID do identificador de produto correspondente e o nome de produto Nome.  
  
 Na expressão seguinte, **Lookup** compara o valor de ProductID com a ID em cada linha do conjunto de dados chamado "Produto" e, quando uma correspondência é localizada, retorna o valor do campo Nome para aquela linha.  
  
```  
=Lookup(Fields!ProductID.Value, Fields!ID.Value, Fields!Name.Value, "Product")  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
