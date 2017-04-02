---
title: "Fun&#231;&#227;o Multilookup (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1fec079e-33b3-4e4d-92b3-6b4d06a49a77
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Fun&#231;&#227;o Multilookup (Construtor de Relat&#243;rios e SSRS)
  Retorna o conjunto de primeiros valores correspondentes para o conjunto de nomes especificado de um conjunto de dados que contém pares de nome/valor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Sintaxe  
  
```  
  
Multilookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### Parâmetros  
 *source_expression*  
 (**VariantArray**) Uma expressão avaliada no escopo atual e que especifica o conjunto de nomes ou chaves a serem procurados. Por exemplo, para um parâmetro de vários valores, `=Parameters!IDs.value`.  
  
 *destination_expression*  
 (**Variant**) Uma expressão avaliada para cada linha em um conjunto de dados e que especifica o nome ou a chave para correspondência. Por exemplo, `=Fields!ID.Value`.  
  
 *result_expression*  
 (**Variant**) Uma expressão avaliada para a linha do conjunto de dados em que *source_expression* = *destination_expression* e que especifica o valor a ser recuperado. Por exemplo, `=Fields!Name.Value`.  
  
 *conjunto de dados*  
 Uma constante que especifica o nome do conjunto de dados no relatório. Por exemplo, "Cores".  
  
## Retorno  
 Retorna **VariantArray**ou **Nothing** se não houver correspondência.  
  
## Comentários  
 Use **Multilookup** para recuperar um conjunto de valores de um conjunto de dados para os pares nome/valor em que cada par tem uma relação de um para um. **MultiLookup** é o equivalente a chamar **Lookup** para um conjunto de nomes ou chaves. Por exemplo, para um parâmetro de vários valores que é baseado em identificadores de chave primária, você pode usar **Multilookup** em uma expressão em uma caixa de texto de uma tabela para recuperar valores associados de um conjunto de dados que não está associado ao parâmetro ou à tabela.  
  
 **Multilookup** faz o seguinte:  
  
-   Avalia a expressão de origem no escopo atual e gera uma matriz de objetos variantes.  
  
-   Para cada objeto na matriz, chama [Função Lookup &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/lookup-function-report-builder-and-ssrs.md) e adiciona o resultado à matriz de retorno.  
  
-   Retorna o conjunto de resultados.  
  
 Para recuperar um único valor de um conjunto de dados com pares de nome/valor para um nome especificado em que exista uma relação de um para um, use [Função Lookup &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/lookup-function-report-builder-and-ssrs.md). Para recuperar vários valores de um conjunto de dados com pares de nome/valor para um nome em que exista uma relação de um para muitos, use [Função LookupSet &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/lookupset-function-report-builder-and-ssrs.md).  
  
 As seguintes restrições são aplicadas:  
  
-   **Multilookup** é avaliado depois que todas as expressões de filtro são aplicadas  
  
-   Só há suporte para um nível de pesquisa. Uma expressão de origem, destino ou resultado não pode incluir uma referência a uma função de pesquisa.  
  
-   Expressões de origem e destino devem ser avaliadas como o mesmo tipo de dados.  
  
-   Expressões de origem, destino e resultado não podem incluir referências a variáveis de relatório ou grupo.  
  
-   **Multilookup** não pode ser usado como uma expressão para os seguintes itens de relatório:  
  
    -   Cadeias de conexão dinâmicas para uma fonte de dados.  
  
    -   Campos calculados em um conjunto de dados.  
  
    -   Parâmetros de consulta em um conjunto de dados.  
  
    -   Filtros em um conjunto de dados.  
  
    -   Parâmetros de relatório.  
  
    -   A propriedade Report.Language.  
  
 Para obter mais informações, consulte [Referência de funções agregadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
## Exemplo  
 Suponha que um conjunto de dados denominado "Category" contenha o campo CategoryList, que é um campo que contém uma lista separada por vírgulas de identificadores de categoria, por exemplo, "2, 4, 2, 1".  
  
 O conjunto de dados CategoryNames contém o identificador de categoria e o nome da categoria, como mostra a tabela a seguir.  
  
|ID|Nome|  
|--------|----------|  
|1|Acessórios|  
|2|Bikes|  
|3|Clothing|  
|4|Componentes|  
  
 Para procurar os nomes que correspondem à lista de identificadores, use **Multilookup**. Você primeiro deve dividir a lista em uma matriz de cadeia de caracteres, chamar **Multilookup** para recuperar os nomes de categoria e concatenar os resultados em uma cadeia de caracteres.  
  
 A seguinte expressão, quando colocada em uma caixa de texto em uma região de dados associada ao conjunto de dados Category, exibe "Bikes, Components, Bikes, Accessories":  
  
```  
=Join(MultiLookup(Split(Fields!CategoryList.Value,","),  
   Fields!CategoryID.Value,Fields!CategoryName.Value,"Category")),  
   ", ")  
```  
  
## Exemplo  
 Suponha que um conjunto de dados ProductColors contenha um campo identificador de cor ColorID e um campo de valor de cor Color, como mostra a tabela a seguir.  
  
|ColorID|Color|  
|-------------|-----------|  
|1|Vermelho|  
|2|Azul|  
|3|Verde|  
  
 Suponha que o parâmetro de vários valores *MyColors* não esteja associado a um conjunto de dados para obter seus valores disponíveis. Os valores padrão para o parâmetro estão definidos como 2 e 3. A expressão a seguir, quando colocada em uma caixa de texto em uma tabela, concatena os vários valores selecionados para o parâmetro em uma lista separada por vírgulas e exibe "Blue, Green".  
  
```  
=Join(MultiLookup(Parameters!MyColors.Value,Fields!ColorID.Value,Fields!Color.Value,"ProductColors"),", ")  
```  
  
## Consulte também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  