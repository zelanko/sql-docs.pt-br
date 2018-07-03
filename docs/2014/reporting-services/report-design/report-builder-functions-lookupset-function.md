---
title: Função LookupSet (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7685acfd-1c8d-420c-993c-903236fbe1ff
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: c7721c5cc57392f1e9968b4b59cb01ba07916f00
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117606"
---
# <a name="lookupset-function-report-builder-and-ssrs"></a>Função LookupSet (Construtor de Relatórios e SSRS)
  Retorna o conjunto de valores correspondentes para o nome especificado de um conjunto de dados que contém pares de nome/valor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
LookupSet(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *source_expression*  
 (`Variant`) Uma expressão que é avaliada no escopo atual e que especifica o nome ou chave para procurar. Por exemplo, `=Fields!ID.Value`.  
  
 *destination_expression*  
 (`Variant`) Uma expressão que é avaliada para cada linha em um conjunto de dados e que especifica o nome ou a chave para correspondência. Por exemplo, `=Fields!CustomerID.Value`.  
  
 *result_expression*  
 (`Variant`) Uma expressão avaliada para a linha do conjunto de dados em que *source_expression* = *destination_expression*e que especifica o valor a ser recuperado. Por exemplo, `=Fields!PhoneNumber.Value`.  
  
 *conjunto de dados*  
 Uma constante que especifica o nome do conjunto de dados no relatório. Por exemplo, "ContactInformation".  
  
## <a name="return"></a>Retorno  
 Retorna um `VariantArray`, ou `Nothing` se não houver nenhuma correspondência.  
  
## <a name="remarks"></a>Remarks  
 Use `LookupSet` para recuperar um conjunto de valores do conjunto de dados especificado para um par nome/valor onde há uma relação de 1-para-muitos. Por exemplo, para um identificador de cliente em uma tabela, você pode usar `LookupSet` para recuperar todos os números de telefone associados do cliente de um conjunto de dados que não esteja associado à região de dados.  
  
 `LookupSet` faz o seguinte:  
  
-   Avalia a expressão de origem no escopo atual.  
  
-   Avalia a expressão de destino para cada linha do conjunto de dados especificado depois que foram aplicados filtros, com base no agrupamento do conjunto de dados especificado.  
  
-   Para cada correspondência da expressão de origem e destino, avalia a expressão resultante para aquela linha no conjunto de dados.  
  
-   Retorna o conjunto de valores de expressão resultante.  
  
 Para recuperar um único valor de um conjunto de dados com pares nome/valor de um nome especificado em que existe uma relação um-para-um, use [Função Lookup &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-lookup-function.md). Para chamar `Lookup` para um conjunto de valores, use [Multilookup função &#40;construtor de relatórios e SSRS&#41;](report-builder-functions-multilookup-function.md).  
  
 As seguintes restrições são aplicadas:  
  
-   `LookupSet` é avaliado depois que todas as expressões de filtro são aplicadas.  
  
-   Só um nível de pesquisa tem suporte. Uma expressão de origem, destino ou resultado não pode incluir uma referência a uma função de pesquisa.  
  
-   Expressões de origem e destino devem ser avaliadas como o mesmo tipo de dados.  
  
-   Expressões de origem, destino e resultado não podem incluir referências a variáveis de relatório ou grupo.  
  
-   `LookupSet` não pode ser usado como uma expressão para os seguintes itens de relatório:  
  
    -   Cadeias de conexão dinâmicas para uma fonte de dados.  
  
    -   Campos calculados em um conjunto de dados.  
  
    -   Parâmetros de consulta em um conjunto de dados.  
  
    -   Filtros em um conjunto de dados.  
  
    -   Parâmetros de relatório.  
  
    -   A propriedade Report.Language.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo seguinte, suponha que a tabela esteja associada a um conjunto de dados que inclui um identificador de território de vendas TerritoryGroupID. Um conjunto de dados separado chamado "Repositórios" contém a lista de todos os repositórios em um território e inclui o identificador ID de território e o nome do repositório StoreName.  
  
 A expressão `LookupSet` compara o valor TerritoryGroupID à ID de cada linha no conjunto de dados chamado "Repositórios". Para cada correspondência, o valor do campo StoreName para aquela linha é acrescentado ao conjunto de resultados.  
  
```  
=LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores")  
```  
  
## <a name="example"></a>Exemplo  
 Porque `LookupSet` retorna uma coleção de objetos, você não pode exibir a expressão de resultado diretamente em uma caixa de texto. Você pode concatenar o valor de cada objeto na coleção como uma cadeia de caracteres.  
  
 Use o [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] função `Join` criar uma cadeia de caracteres delimitada de um conjunto de objetos. Use vírgula como separador combinar os objetos em uma única linha. Em alguns renderizadores, você pode usar uma alimentação de linha ( [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ) do`vbCrLF`como um separador para listar cada valor em uma nova linha.  
  
 A expressão a seguir, quando ele é usado como a propriedade de valor para uma caixa de texto usa `Join` para criar uma lista.  
  
```  
=Join(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"),",")  
```  
  
## <a name="example"></a>Exemplo  
 Para caixas de texto que só renderizam algumas vezes, você pode escolher adicionar código personalizado para gerar HTML para exibir valores em uma caixa de texto. O HTML em uma caixa de texto requer processamento extra; portanto, não é uma boa escolha para uma caixa de texto que é renderizada milhares de vezes.  
  
 Copiar as seguintes funções do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para um bloco Code em uma definição de relatório. **MakeList** considera a matriz de objetos que é retornada em *result_expression* e compila uma lista não ordenada usando marcas HTML. **Length** retorna o número de itens em uma matriz de objetos.  
  
```  
Function MakeList(ByVal items As Object()) As String  
   If items Is Nothing Then  
      Return Nothing  
   End If  
  
   Dim builder As System.Text.StringBuilder =   
      New System.Text.StringBuilder()  
   builder.Append("<ul>")  
  
   For Each item As Object In items  
      builder.Append("<li>")  
      builder.Append(item)  
   Next  
   builder.Append("</ul>")  
  
   Return builder.ToString()  
End Function  
  
Function Length(ByVal items as Object()) as Integer  
   If items is Nothing Then  
      Return 0  
   End If  
   Return items.Length  
End Function  
```  
  
## <a name="example"></a>Exemplo  
 Para gerar o HTML, você deve chamar a função. Cole a expressão seguinte na propriedade Value para a caixa de texto e defina o tipo de marcação para texto como HTML. Para obter mais informações, consulte [Adicionar HTML a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-html-into-a-report-report-builder-and-ssrs.md).  
  
```  
=Code.MakeList(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"))  
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressão usa relatórios de &#40;SSRS e construtor de relatórios&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;SSRS e construtor de relatórios&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  