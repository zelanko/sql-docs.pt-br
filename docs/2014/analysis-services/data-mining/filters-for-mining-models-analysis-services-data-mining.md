---
title: Filtros para modelos de mineração (Analysis Services-Mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- filter syntax [data mining]
- models [Analysis Services], filtering
- filters [data mining]
- filtering data [Analysis Services]
ms.assetid: 0f29c19c-4be3-4bc7-ab60-f4130a10d59c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4a7695bef91ace5eb6ff8d642c51b379343fb0b1
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522343"
---
# <a name="filters-for-mining-models-analysis-services---data-mining"></a>Filtros para modelos de mineração (Analysis Services - Mineração de dados)
  A filtragem de modelos com base em dados ajuda na criação de modelos de mineração que usam subconjuntos de dados em uma estrutura de mineração. A filtragem proporciona flexibilidade quando você projeta suas estruturas de mineração e fontes de dados porque você pode criar uma única estrutura de mineração, com base em uma exibição da fonte de dados abrangente. Em seguida, é possível criar filtros que serão usados somente como parte dos dados para treinar e testar uma variedade de modelos, em vez de criar uma estrutura diferente e um modelo relacionado para cada subconjunto de dados.  
  
 Por exemplo, você define a exibição da fonte de dados na tabela Clientes e nas tabelas relacionadas. Em seguida, define uma única estrutura de mineração que inclui todos os campos necessários. Finalmente, você cria um modelo filtrado em um atributo de cliente particular, como Região. Você pode fazer facilmente uma cópia desse modelo e alterar apenas a condição de filtro para gerar um novo modelo com base em uma região diferente.  
  
 Algumas situações reais das quais você pode tirar proveito desse recurso incluem:  
  
-   Criar modelos separados para obter valores discretos como gênero, regiões e assim sucessivamente. Por exemplo, uma loja de roupas pode usar dados demográficos do cliente para criar modelos separados por sexo, mesmo que os dados de vendas sejam provenientes de uma única fonte de dados para todos os clientes.  
  
-   Experimentar modelos criando e testando vários agrupamentos dos mesmos dados, como idades de 20 a 30 comparadas com 20 a 40 e 20 a 25.  
  
-   Especificar filtros complexos em conteúdo de tabela aninhada, como exigir que um caso seja incluído no modelo somente se o cliente tiver comprado pelo menos dois de um determinado item.  
  
 Esta seção explica como criar, usar e administrar filtros em modelos de mineração.  
  
## <a name="creating-model-filters"></a>Criando filtros de modelos  
 Você pode criar e aplicar filtros das seguintes formas:  
  
-   Usando a guia **Modelos de Mineração** no Designer de Mineração de Dados para criar condições com a ajuda das caixas de diálogo do editor de filtros.  
  
-   Digitando uma expressão de filtro diretamente na `Filter` Propriedade do modelo de mineração.  
  
-   Definindo condições de filtro em um modelo de forma programática usando AMO.  
  
### <a name="creating-model-filters-using-data-mining-designer"></a>Criando filtros de modelo usando o Designer de Mineração de Dados  
 Você filtra um modelo no Designer de Mineração de Dados alterando a propriedade `Filter` do modelo de mineração. É possível digitar uma expressão de filtro diretamente no painel **Propriedades** ou abrir uma caixa de diálogo de filtros para criar condições.  
  
 Há duas caixas de diálogo de filtro. A primeira permite criar condições aplicadas à tabela de casos. Se a fonte de dados contiver várias tabelas, primeiro você escolherá uma tabela e, em seguida, selecionará uma coluna e especificará os operadores e as condições que se aplicam àquela coluna. Você pode vincular várias condições usando `AND` / `OR` operadores. Os operadores disponíveis para definir os valores dependem se a coluna contém valores discretos ou contínuos. Por exemplo, com valores contínuos, você pode usar os operadores `greater than` e `less than`. Porém, para valores discretos, você pode usar apenas os operadores `= (equal to)`, `!= (not equal to)`e `is null`.  
  
> [!NOTE]  
>  Não há suporte para a palavra-chave `LIKE`. Para incluir vários atributos discretos, é preciso criar várias condições separadas e vinculá-las usando o operador `OR`.  
  
 Se as condições forem complexas, você pode usar a segunda caixa de diálogo de filtros para trabalhar com uma tabela por vez. Quando você fechar a segunda caixa de diálogo do filtro, a expressão será avaliada e combinada com as condições de filtro definidas em outras colunas na tabela de casos.  
  
### <a name="creating-filters-on-nested-tables"></a>Criando filtros em tabelas aninhadas  
 Se a exibição da fonte de dados contiver tabelas aninhadas, você poderá usar a segunda caixa de diálogo de filtro para criar condições nas linhas das tabelas aninhadas.  
  
 Por exemplo, se a tabela de casos estiver relacionada a clientes e a tabela aninhada mostrar os produtos que um cliente comprou, você poderá criar um filtro para os clientes que compraram determinados itens usando a seguinte sintaxe no filtro de tabela aninhada: `[ProductName]='Water Bottle' OR ProductName='Water Bottle Cage'`.  
  
 Você também pode filtrar a existência de um determinado valor na tabela aninhada, usando as palavras-chave `EXISTS` ou `NOT EXISTS` e uma subconsulta. Isso permite que você crie condições como `EXISTS (SELECT * FROM Products WHERE ProductName='Water Bottle')`. `EXISTS SELECT(<subquery>)` retornará `true` se a tabela aninhada contiver pelo menos uma linha que inclua o valor `Water Bottle`.  
  
 Você pode combinar condições na tabela de casos com as condições da tabela aninhada. Por exemplo, a sintaxe a seguir inclui uma condição na tabela de casos (`Age > 30` ), uma subconsulta na tabela aninhada (`EXISTS (SELECT * FROM Products)`) e várias condições na tabela aninhada (`WHERE ProductName='Milk'  AND Quantity>2`) ).  
  
```  
(Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk'  AND Quantity>2) )  
```  
  
 Quando você terminar de criar o filtro, o texto do filtro será avaliado pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], convertido para uma expressão DMX e, em seguida, salvo com o modelo.  
  
 Para obter instruções sobre como usar as caixas de diálogo de filtro no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], consulte [Aplicar um filtro a um modelo de mineração](apply-a-filter-to-a-mining-model.md).  
  
## <a name="managing-mining-model-filters"></a>Gerenciando os filtros do modelo de mineração  
 A filtragem do modelo com base em dados simplifica a tarefa de gerenciar estruturas de mineração e modelos de mineração porque você pode criar facilmente vários modelos com base na mesma estrutura. Você também pode fazer cópias de modelos de mineração existentes rapidamente e, em seguida, alterar apenas a condição do filtro. Entretanto, os filtros podem gerar uma certa confusão.  
  
 Estas são algumas perguntas frequentes sobre como gerenciar e interpretar filtros em modelos de mineração:  
  
### <a name="how-can-i-tell-whether-a-filter-is-being-used"></a>Como posso saber se um filtro está sendo usado?  
 Existem várias maneiras de determinar se um filtro é aplicado a um modelo:  
  
-   No designer, clique na guia **modelos de mineração** , abra **Propriedades**e exiba a `Filter` Propriedade do modelo de mineração.  
  
-   O DMV, DMSCHEMA_MINING_MODELS, gera uma coluna que contém o texto do filtro. Você pode usar a seguinte consulta em um DMV para retornar os nomes de modelos e seus filtros:  
  
    ```  
    SELECT MODEL_NAME, [FILTER]   
    FROM $SYSTEM.DMSCHEMA_MINING_MODELS  
  
    ```  
  
-   É possível obter o valor da propriedade Filter do objeto MiningModel em AMO, ou inspecionar o elemento Filter em XMLA.  
  
 Você também pode estabelecer uma convenção de nomenclatura para modelos para refletir o conteúdo do filtro. Isso pode tomar mais fácil diferenciar os modelos relacionados.  
  
### <a name="how-can-i-save-a-filter"></a>Como posso salvar um filtro?  
 A expressão de filtro é salva como um script armazenado com o modelo de mineração associado ou tabela aninhada. Se você excluir o texto de filtro, ele só poderá ser restaurado manualmente, recriando a expressão de filtro. Portanto, se você criar expressões de filtro complexas, deve criar uma cópia de backup do texto de filtro.  
  
### <a name="why-cant-i-see-any-effects-from-the-filter"></a>Por que não consigo ver nenhum efeito do filtro?  
 Sempre que você alterar ou adicionar uma expressão de filtro, deverá reprocessar a estrutura e o modelo antes de poder criar os efeitos do filtro.  
  
### <a name="why-do-i-see-filtered-attributes-in-prediction-query-results"></a>Por que vejo atributos filtrados em resultados de consulta de previsão?  
 Quando você aplica um filtro a um modelo, ele afeta somente a seleção de casos usados para treinar o modelo. O filtro não afeta os atributos conhecidos pelo modelo, nem altera ou suprime dados presentes na fonte de dados. Como resultado, as consultas no modelo podem retornar previsões para outros tipos de casos, e listas suspensas de valores usados pelo modelo podem mostrar valores de atributos excluídos pelo filtro.  
  
 Por exemplo, digamos que você treine o modelo [Bike Buyer] usando apenas casos que envolvem mulheres na faixa etária 20-30. Você ainda pode executar uma consulta de previsão que prevê a probabilidade de um homem comprar uma bicicleta, ou prever o resultado para uma mulher na faixa etária 30-40. Isso ocorre porque os atributos e valores presentes na fonte de dados definem o que é teoricamente possível, enquanto os casos definem as ocorrências usadas para treinamento. Entretanto, essas consultas retornariam probabilidades bem pequenas, pois os dados de treinamento não contêm casos com os valores de destino.  
  
 Se você precisar ocultar totalmente ou tornar anônimos valores de atributo no modelo, há diversas opções:  
  
-   Filtrar os dados de entrada como parte da definição da exibição da fonte de dados, ou na fonte de dados relacional.  
  
-   Mascarar ou codificar o valor do atributo.  
  
-   Recolher valores excluídos em uma categoria como parte da definição da estrutura de mineração.  
  
## <a name="related-resources"></a>Recursos relacionados  
 Para obter mais informações sobre a sintaxe de filtro, bem como exemplos de expressões de filtro, consulte [Sintaxe de filtro de modelo e exemplos &#40;Analysis Services – Mineração de dados&#41;](model-filter-syntax-and-examples-analysis-services-data-mining.md).  
  
 Para obter informações sobre como usar filtros de modelo quando você estiver testando um modelo de mineração, consulte [Escolher um tipo de gráfico de precisão e definir opções de gráfico](choose-an-accuracy-chart-type-and-set-chart-options.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Sintaxe de filtro de modelo e exemplos &#40;mineração de dados Analysis Services&#41;](model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [Teste e validação &#40;Mineração de dados&#41;](testing-and-validation-data-mining.md)  
  
  
