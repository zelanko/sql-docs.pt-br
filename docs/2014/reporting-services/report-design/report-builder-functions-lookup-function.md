---
title: Função Lookup (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e60e5bab-b286-4897-9685-9ff12703517d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93e53646314d211ced489d3538b40c77195f494b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105220"
---
# <a name="lookup-function-report-builder-and-ssrs"></a>Função Lookup (Construtor de Relatórios e SSRS)
  Retorna o primeiro valor correspondente para o nome especificado de um conjunto de dados que contém pares de nome/valor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Lookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *source_expression*  
 (`Variant`) Uma expressão que é avaliada no escopo atual e que especifica o nome ou chave para procurar. Por exemplo, `=Fields!ProdID.Value`.  
  
 *destination_expression*  
 (`Variant`) Uma expressão que é avaliada para cada linha em um conjunto de dados e que especifica o nome ou a chave para correspondência. Por exemplo, `=Fields!ProductID.Value`.  
  
 *result_expression*  
 (`Variant`) Uma expressão que é avaliada para a linha no conjunto de linhas em que *source_expression* = *destination_expression*e que especifica o valor a ser recuperado. Por exemplo, `=Fields!ProductName.Value`.  
  
 *conjunto de dados*  
 Uma constante que especifica o nome do conjunto de dados no relatório. Por exemplo, "Produtos".  
  
## <a name="return"></a>Retorno  
 Retorna `Variant` ou `Nothing` se não houver correspondência.  
  
## <a name="remarks"></a>Comentários  
 Use `Lookup` para recuperar o valor do conjunto de dados especificado para um par de nome/valor onde há uma relação de 1 para 1. Por exemplo, para um campo de ID em uma tabela, você pode usar `Lookup` para recuperar todos os números de telefone associados àquele cliente de um conjunto de dados que não esteja associado à região de dados.  
  
 `Lookup` faz o seguinte:  
  
-   Avalia a expressão de origem no escopo atual.  
  
-   Avalia a expressão de destino para cada linha do conjunto de dados especificado depois que foram aplicados filtros, com base na ordenação do conjunto de dados especificado.  
  
-   Na primeira correspondência da expressão de origem e destino, avalia a expressão resultante para aquela linha no conjunto de dados.  
  
-   Retorna o valor da expressão resultante.  
  
 Para recuperar diversos valores para um único nome ou campo de chave em que há uma relação um para muitos, use [Função LookupSet &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-lookupset-function.md). Para chamar `Lookup` um conjunto de valores, use a [função multilookup &#40;Construtor de relatórios e o SSRS&#41;](report-builder-functions-lookup-function.md).  
  
 As restrições a seguir se aplicam:  
  
-   `Lookup` é avaliado depois que todas as expressões de filtro são aplicadas.  
  
-   Só um nível de pesquisa tem suporte. Uma expressão de origem, destino ou resultado não pode incluir uma referência a uma função de pesquisa.  
  
-   Expressões de origem e destino devem ser avaliadas como o mesmo tipo de dados. O tipo de retorno é o mesmo que o tipo de dados da expressão resultante avaliada.  
  
-   Expressões de origem, destino e resultado não podem incluir referências a variáveis de relatório ou grupo.  
  
-   `Lookup` não pode ser usado como uma expressão para os seguintes itens de relatório:  
  
    -   Cadeias de conexão dinâmicas para uma fonte de dados.  
  
    -   Campos calculados em um conjunto de dados.  
  
    -   Parâmetros de consulta em um conjunto de dados.  
  
    -   Filtros em um conjunto de dados.  
  
    -   Parâmetros de relatório.  
  
    -   A propriedade Report.Language.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo seguinte, suponha que a tabela esteja associada a um conjunto de dados que inclui um campo para o identificador de produto ProductID. Um conjunto de dados separado chamado "Produto" contém a ID do identificador de produto correspondente e o nome de produto Nome.  
  
 Na expressão seguinte, `Lookup` compara o valor de ProductID com a ID em cada linha do conjunto de dados chamado "Produto" e, quando uma correspondência é localizada, retorna o valor do campo Nome para aquela linha.  
  
```  
=Lookup(Fields!ProductID.Value, Fields!ID.Value, Fields!Name.Value, "Product")  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
