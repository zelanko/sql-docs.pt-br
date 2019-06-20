---
title: Função Multilookup (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1fec079e-33b3-4e4d-92b3-6b4d06a49a77
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e6a60f1b47c7015fa0fca27cc7ce68bf4d04b15d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105207"
---
# <a name="multilookup-function-report-builder-and-ssrs"></a>Função Multilookup (Construtor de Relatórios e SSRS)
  Retorna o conjunto de primeiros valores correspondentes para o conjunto de nomes especificado de um conjunto de dados que contém pares de nome/valor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Multilookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *source_expression*  
 (`VariantArray`) Uma expressão que é avaliada no escopo atual e que especifica o conjunto de nomes ou chaves para procurar. Por exemplo, para um parâmetro de vários valores, `=Parameters!IDs.value`.  
  
 *destination_expression*  
 (`Variant`) Uma expressão que é avaliada para cada linha em um conjunto de dados e que especifica o nome ou a chave para correspondência. Por exemplo, `=Fields!ID.Value`.  
  
 *result_expression*  
 (`Variant`) Uma expressão avaliada para a linha do conjunto de dados em que *source_expression* = *destination_expression*e que especifica o valor a ser recuperado. Por exemplo, `=Fields!Name.Value`.  
  
 *conjunto de dados*  
 Uma constante que especifica o nome do conjunto de dados no relatório. Por exemplo, "Cores".  
  
## <a name="return"></a>Retorno  
 Retorna `VariantArray` ou `Nothing` se não houver correspondência.  
  
## <a name="remarks"></a>Comentários  
 Use `Multilookup` para recuperar um conjunto de valores de um conjunto de dados para os pares nome/valor em que cada par tem uma relação de 1 para 1. `MultiLookup` é o equivalente a chamar `Lookup` para um conjunto de nomes ou chaves. Por exemplo, para um parâmetro de vários valores que é baseado em identificadores de chave primária, você pode usar `Multilookup` em uma expressão em uma caixa de texto de uma tabela para recuperar valores associados de um conjunto de dados que não está associado ao parâmetro ou à tabela.  
  
 `Multilookup` faz o seguinte:  
  
-   Avalia a expressão de origem no escopo atual e gera uma matriz de objetos variantes.  
  
-   Para cada objeto na matriz, chama [Função Lookup &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-lookup-function.md) e adiciona o resultado à matriz de retorno.  
  
-   Retorna o conjunto de resultados.  
  
 Para recuperar um único valor de um conjunto de dados com pares nome-valor de um nome especificado em que existe uma relação um-para-um, use [Função Lookup &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-lookup-function.md). Para recuperar vários valores de um conjunto de dados com pares nome-valor de um nome em que existe uma relação um para muitos, use [Função LookupSet &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-lookupset-function.md).  
  
 As seguintes restrições são aplicadas:  
  
-   `Multilookup` é avaliado depois que todas as expressões de filtro são aplicadas  
  
-   Só há suporte para um nível de pesquisa. Uma expressão de origem, destino ou resultado não pode incluir uma referência a uma função de pesquisa.  
  
-   Expressões de origem e destino devem ser avaliadas como o mesmo tipo de dados.  
  
-   Expressões de origem, destino e resultado não podem incluir referências a variáveis de relatório ou grupo.  
  
-   `Multilookup` não pode ser usado como uma expressão para os seguintes itens de relatório:  
  
    -   Cadeias de conexão dinâmicas para uma fonte de dados.  
  
    -   Campos calculados em um conjunto de dados.  
  
    -   Parâmetros de consulta em um conjunto de dados.  
  
    -   Filtros em um conjunto de dados.  
  
    -   Parâmetros de relatório.  
  
    -   A propriedade Report.Language.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Exemplo  
 Suponha que um conjunto de dados denominado "Category" contenha o campo CategoryList, que é um campo que contém uma lista separada por vírgulas de identificadores de categoria, por exemplo, "2, 4, 2, 1".  
  
 O conjunto de dados CategoryNames contém o identificador de categoria e o nome da categoria, como mostra a tabela a seguir.  
  
|ID|Nome|  
|--------|----------|  
|1|Acessórios|  
|2|Bikes|  
|3|Clothing|  
|4|Componentes|  
  
 Para procurar os nomes que correspondem à lista de identificadores, use `Multilookup`. Você primeiro deve dividir a lista em uma matriz de cadeia de caracteres, chamar `Multilookup` para recuperar os nomes de categoria e concatenar os resultados em uma cadeia de caracteres.  
  
 A seguinte expressão, quando colocada em uma caixa de texto em uma região de dados associada ao conjunto de dados Category, exibe "Bikes, Components, Bikes, Accessories":  
  
```  
=Join(MultiLookup(Split(Fields!CategoryList.Value,","),  
   Fields!CategoryID.Value,Fields!CategoryName.Value,"Category")),  
   ", ")  
```  
  
## <a name="example"></a>Exemplo  
 Suponha que um conjunto de dados ProductColors contenha um campo identificador de cor ColorID e um campo de valor de cor Color, como mostra a tabela a seguir.  
  
|ColorID|Cor|  
|-------------|-----------|  
|1|Vermelho|  
|2|Azul|  
|3|Verde|  
  
 Suponha que o parâmetro de vários valores *MyColors* não esteja associado a um conjunto de dados para obter seus valores disponíveis. Os valores padrão para o parâmetro estão definidos como 2 e 3. A expressão a seguir, quando colocada em uma caixa de texto em uma tabela, concatena os vários valores selecionados para o parâmetro em uma lista separada por vírgulas e exibe "Blue, Green".  
  
```  
=Join(MultiLookup(Parameters!MyColors.Value,Fields!ColorID.Value,Fields!Color.Value,"ProductColors"),", ")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
