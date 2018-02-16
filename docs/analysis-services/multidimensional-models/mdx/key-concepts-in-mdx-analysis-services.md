---
title: Principais conceitos em MDX (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], about MDX
- dimensional modeling [MDX]
- MDX [Analysis Services], about MDX
- Multidimensional Expressions [Analysis Services], dimensional modeling
- MDX [Analysis Services], dimensional modeling
ms.assetid: 4797ddc8-6423-497a-9a43-81a1af7eb36c
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 23aca9e6a5595c8597d13e2e832390988c50be3c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="key-concepts-in-mdx-analysis-services"></a>Principais conceitos em MDX (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Antes de usar MDX (Multidimensional Expressions) para consultar dados multidimensionais ou criar expressões MDX em um cubo, é importante entender os conceitos e a terminologia multidimensional.  
  
 O melhor é começar com um exemplo de resumo de dados já conhecido para ver como o MDX se relaciona com ele. Este é um PivotTable criado no Excel, populado com os dados de um cubo de exemplo do Analysis Services.  
  
 ![Tabela dinâmica com medidas e dimensões destacadas](../../../analysis-services/multidimensional-models/media/ssas-keyconcepts-pivot1-measures-dimensions.png "tabela dinâmica com medidas e dimensões destacadas")  
  
## <a name="measures-and-dimensions"></a>Medidas e dimensões  
 Um cubo do Analysis Services é composto por medida, dimensões e atributos de dimensão, todos demonstrados no exemplo do PivotTable.  
  
 **Medidas** são valores numéricos encontrados nas células, agregados como soma, contagem, percentual, mínimo, máximo ou média. Os valores de medida são dinâmicos, calculados em tempo real, em resposta à navegação do usuário e interação com o PivotTable. Neste exemplo, as células mostram os Valores de Venda do Revendedor que aumentam ou diminuem se você expandir ou ocultar os eixos. É possível obter o Valor de Vendas do Revendedor para qualquer contexto e combinação de Data (ano, trimestre, mês ou data) e Território de Vendas (Grupo de países, País, Região). Outros termos sinônimos de medidas são os fatos (nas data warehouses) e campos calculados (em modelos de dados tabulares ou do Excel).  
  
 **Dimensões** encontram-se nos eixos de coluna e linha do PivotTable, fornecendo o significado por trás da medida. Dimensões são análogas a Tabelas em um modelo de dados relacional. Exemplos comuns de dimensões incluem Hora, Geografia, Produtos, Clientes, Funcionários e assim por diante. Este exemplo possui duas dimensões, o Território de Vendas nas linhas e a Data no topo, porém você pode facilmente arrastar e soltar outras dimensões associadas às Vendas do Revendedor, como Promoções ou Produtos, para ver o desempenho de vendas de acordo com essas dimensões. Sua capacidade de explorar os dados de maneiras interessantes depende das dimensões criadas e se elas possuem relação com as tabelas de fatos na fonte de dados.  
  
 **Atributos de Dimensão** são os itens nomeados em uma dimensão, similar às colunas de uma tabela. Neste exemplo, os atributos da dimensão Território de Vendas consistem em Grupo de Países (Europa, América do Norte, Pacífico), País (Canadá, Estados Unidos) e Região (Central, Nordeste, Noroeste, Sudeste, Sudoeste).  
  
 Cada categoria tem um conjunto de valores de dados, ou membros, associado a ela. No nosso exemplo, os membros do atributo Grupo de Países são Europa, América do Norte e Pacífico. **Membros** refere-se aos valores de dados reais pertencentes a um atributo.  
  
> [!NOTE]  
>  Um aspecto da modelagem de dados é formalizar os padrões e relacionamentos já existentes nos próprios dados. Ao trabalhar com dados que se enquadram em uma hierarquia natural, como no caso de países-regiões-cidades, você pode formalizar essa relação criando uma **relação de atributo**. Uma relação de atributo é uma relação entre atributos de um para muitos, por exemplo, uma relação entre um atributo de dimensão de um estado e uma cidade, onde um estado possui muitas cidades, mas uma cidade pertence a apenas um estado. Criar relações de atributo no modelo acelera o desempenho das consultas, por isso é uma prática recomendada criá-las se os dados suportarem. Você pode criar uma relação de atributo no Designer de Dimensão no SQL Server Data Tools. Consulte [Define Attribute Relationships](../../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
 No Excel, os metadados do modelo são mostrados na lista de campos do PivotTable.  Compare o PivotTable acima com a lista de campos abaixo. Observe que a lista de campos contém Território de Vendas, Grupo e País (metadados), enquanto o PivotTable contém somente os membros (valores dos dados). Conhecer o visual dos ícones pode ajudar você a relacionar mais facilmente as partes de um modelo multidimensional de PivotTable no Excel.  
  
 ![Lista de campos da tabela dinâmica](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-ptfieldlist.png "lista de campos da tabela dinâmica")  
  
## <a name="attribute-hierarchies"></a>Hierarquias de atributo  
 Quase sem pensar nisso, você sabe que os valores de um PivotTable sobem ou descem ao expandir ou recolher os níveis em cada eixo, mas por que isso ocorre? A resposta está nas hierarquias de atributo.  
  
 Recolha todos os níveis e observe os totais de cada Grupo de País e Ano Civil. Este valor é derivado de algo chamado de **Membro (Todos)** em uma hierarquia. O Membro (All) é o valor calculado de todos os membros em uma hierarquia de atributos.  
  
-   O Membro (All) de todos os Grupos de Países e Datas combinado é US$80.450.596,98  
  
-   O Membro (All) do AC2008 is US$16.038.062,60  
  
-   O Membro (All) do Pacífico é US$1.594.335,38  
  
 Agregações como esta são pré-computadas e armazenadas com antecedência, como parte do segredo para um desempenho de consulta rápida do Analysis Services.  
  
 ![Tabela dinâmica com todos os membros destacados](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot2-allmember.png "tabela dinâmica com todos os membros destacados")  
  
 Expanda a hierarquia e eventualmente você chegará ao nível mais baixo. Ele é chamado de **membro folha**. Um membro folha é um membro de uma hierarquia que não tem filho. Neste exemplo, a Austrália é o membro folha.  
  
 ![Tabela dinâmica com membro folha destacado](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot3-leafparent.PNG "tabela dinâmica com membro folha destacado")  
  
 Tudo acima é chamado de **membro pai**. Pacífico é o pai da Austrália.  
  
 **Componentes de uma hierarquia de atributos.**  
  
 Em conjunto, todos esses conceitos levam ao conceito de uma **hierarquia de atributo**. Uma hierarquia de atributo é uma árvore de membros de atributo que contém os seguintes níveis:  
  
-   Um nível folha que contém cada membro distinto de atributo, com cada membro do nível folha também conhecido como um **membro folha**.  
  
-   Níveis intermediários se a hierarquia de atributo for uma hierarquia pai-filho (veremos mais sobre este caso posteriormente).  
  
-   Um Membro (All) que contém o valor agregado de todos os atributos filhos. Opcionalmente, você pode ocultar ou desativar o nível (All) quando ele não se aplicar aos dados. Por exemplo, embora Código de Produto seja numérico, não faz sentido contabilizar sua soma ou média, ou ainda agregar todos os Códigos de Produto.  
  
> [!NOTE]  
>  Os desenvolvedores de BI geralmente definem as propriedades de uma hierarquia de atributo para alcançar certos comportamentos em aplicativos cliente ou obter certos benefícios no desempenho. Por exemplo, você poderia definir AttributeHierarchyEnabled=False nos atributos aos quais o Membro (All) não se aplica. Como alternativa, talvez você possa simplesmente ocultar o Membro (All), definindo nesse caso AttributeHierarchyVisible=False. Veja [Dimension Attribute Properties Reference](../../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md) para obter mais detalhes sobre propriedades.  
  
## <a name="navigation-hierarchies"></a>Hierarquias de navegação  
 No PivotTable (pelo menos nesse exemplo), os eixos de linha e coluna são expandidos para mostrar níveis inferiores dos atributos. Uma árvore expansível é obtida por meio das hierarquias de navegação criadas em um modelo.  No modelo de exemplo do AdventureWorks, a dimensão Território de Vendas possui muitas hierarquias em múltiplos níveis, começando com Grupo de Países, seguido por País e por fim Região.  
  
 Vemos aqui como as hierarquias são usadas para fornecer um caminho de navegação em um PivotTable ou outros objetos de resumo de dados. Há dois tipos básicos: equilibrada e desbalanceada.  
  
 **Hierarquias equilibradas**  
  
|||  
|-|-|  
|![Tabela dinâmica com hierarquia balanceada destacada](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot4-balancedhierarchy.PNG "tabela dinâmica com hierarquia balanceada destacada")|Uma **hierarquia equilibrada** é uma hierarquia em que o mesmo número de níveis existe entre o nível superior e qualquer membro folha.<br /><br /> Uma **hierarquia natural** é aquela que surge naturalmente dos dados subjacentes. Exemplos comuns são País-Região-Estado, Ano-Mês-Dia ou Categoria-Subcategoria-Modelo, onde cada nível subordinado flui previsivelmente do pai.<br /><br /> Em um modelo multidimensional, a maioria das hierarquias são equilibradas e muitas também são naturais.<br /><br /> Outro termo de modelagem relacionado é uma **hierarquia definida pelo usuário**, geralmente usado em contraste com hierarquias de atributo. Isso significa apenas uma hierarquia criada pelo desenvolvedor de BI, em contraposição a hierarquias de atributo geradas automaticamente pelo Analysis Services ao definir um atributo.|  
  
 **Hierarquias desbalanceadas**  
  
|||  
|-|-|  
|![Tabela dinâmica com Hierarquia desbalanceada destacada](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot15-raggedhierarchy.PNG "tabela dinâmica com Hierarquia desbalanceada destacada")|Uma **hierarquia imperfeita** ou **hierarquia desbalanceada** é uma hierarquia em que existem diferentes números de níveis entre o nível superior e os membros folha. Novamente, esta é uma hierarquia criada pelo desenvolvedor de BI, mas neste caso existem lacunas nos dados.<br /><br /> No modelo de exemplo do AdventureWorks, o Território de Vendas demonstra uma hierarquia irregular, pois os Estados Unidos possuem um nível adicional (Regiões) que não existe para os demais países deste exemplo.<br /><br /> Hierarquias irregulares são um desafio para os desenvolvedores de BI se o aplicativo cliente não puder lidar com elas de maneira elegante. No modelo do Analysis Services, você pode criar uma **hierarquia pai-filho** que define explicitamente uma relação entre dados de vários níveis, eliminando qualquer ambiguidade quanto a como um nível se relaciona com o próximo. Consulte [Dimensões pai-filho](../../../analysis-services/multidimensional-models/parent-child-dimension.md) para obter detalhes.|  
  
## <a name="key-attributes"></a>Atributos de chave  
 Os modelos são uma colação de objetos relacionados que contam com chaves e índices para fazer associações. O mesmo vale para os modelos do Analysis Services. Para cada dimensão (lembre-se que é equivalente a uma tabela em um modelo relacional) há um atributo de chave. O **atributo de chave** é usado em relações de chave estrangeira com a tabela de fatos (grupo de medidas). Todos os atributos que não são de chave na dimensão são vinculados (direta ou indiretamente) ao atributo de chave.  
  
 Em geral, mas não sempre, o atributo de chave também é o **Atributo de Granularidade**. A granularidade refere-se ao nível de detalhes ou precisão dos dados. Novamente, um exemplo comum é o jeito mais rápido de entender. Considere os valores de data: Para vendas diárias, você precisa dos valores de data específicos do dia em questão; para cotas, pode ser suficiente especificar o trimestre, mas se seus dados analíticos são os resultados de corridas de um evento esportivo, a granulação poderá ser milissegundos. O nível de precisão dos valores dos dados é a granulação.  
  
 A moeda é outro exemplo: um aplicativo financeiro pode acompanhar valores monetários até vários decimais, enquanto que o angariador de fundos da escola local pode precisar apenas de valores arredondados para a unidade. É importante entender a granulação para evitar armazenar dados desnecessários. Retirar os milissegundos da marcação de hora ou centavos do valor de vendas pode economizar espaço de armazenamento e tempo de processamento quando este nível de detalhe não for relevante para sua análise.  
  
 Para definir o atributo de granularidade, use a guia Uso da Dimensão no Designer de Cubo no SQL Server Data Tools. No modelo de exemplo do AdventureWorks, o atributo de chave da dimensão Data é a chave Data. Para Pedidos de Compra, o atributo de granularidade é equivalente ao atributo de chave. Para Metas de Venda, o nível de granularidade é trimestral, por isso o atributo de granularidade está definido para o Trimestre Civil.  
  
 ![Modelo que exibe o atributo de granularidade](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-granularityattrib.png "mostrando o atributo de granularidade de modelo")  
  
> [!NOTE]  
>  Se o atributo de granularidade e o atributo de chave forem diferentes, todos os atributos não chave deverão ser vinculados, direta ou indiretamente, ao atributo de granularidade. Dentro de um cubo, o atributo de granularidade define a granularidade de uma dimensão.  
  
## <a name="query-scope-cube-space"></a>Escopo da consulta (Espaço de cubo)  
 O escopo de uma consulta refere-se aos limites dentro dos quais os dados são selecionados. Ele pode variar de um cubo inteiro (um cubo é o maior objeto de consulta) até uma célula.  
  
 **Espaço de cubo** é o produto dos membros das hierarquias de atributo de um cubo com as medidas do cubo.  
  
 **Subcubo** é um subconjunto de um cubo que representa uma exibição filtrada do cubo. Subcubos podem ser definidos com uma instrução Scope no script de cálculo MDX ou em cláusula de subseleção em uma consulta MDX ou como um cubo de sessão.  
  
 **Célula** refere-se ao espaço na interseção de um membro do membro de dimensão de medidas e um membro de cada hierarquia de atributo em um cubo.  
  
## <a name="other-modeling-terms"></a>Outros termos de modelagem  
 Esta seção é uma coleção de conceitos e termos que não pertencem a outras seções, mas que você ainda deve conhecer.  
  
 **Membro calculado** é um membro de dimensão definido e calculado na hora da consulta. Um membro calculado pode ser definido como uma consulta de usuário ou como script de cálculo MDX e armazenado no servidor. Um membro calculado corresponde a filas na tabela de dimensão da dimensão onde ele é definido.  
  
 **Contagem Distinta** é um tipo especial de medida usado para itens de dados que somente devem ser contados uma vez. O modelo de exemplo do AdventureWorks inclui diferentes medidas de contagem para Pedidos da Internet, Pedidos do Revendedor e Pedidos de Venda.  
  
 **Grupos de medidas** são uma coleção de uma ou mais medidas. A maioria deles são definidos pelo usuário, e você pode usá-los para reunir medidas relacionadas. A exceção são as medidas de contagens distintas. Elas sempre são colocadas em um grupo de medidas dedicado que contém somente a medida diferente. A ilustração de exemplo do PivotTable não mostra o grupo de medidas, mas este aparece na lista de campos do PivotTable como uma coleção de medidas com nome.  
  
 **Dimensão de medidas** é a dimensão que contém todas as medidas em um cubo. Ela não fica exposta em um modelo multidimensional criado no SQL Server Data Tools, mas existe mesmo assim. Como ela contém medidas, todos os membros de uma dimensão de medidas são tipicamente agregados (geralmente por soma ou contagem).  
  
 **Dimensões de Banco de Dados e de Cubo**. Em um modelo, você pode definir dimensões independentes que serão incluídas nos cubos do mesmo modelo. Quando você adiciona uma dimensão a um cubo, esta é chamada de dimensão de cubo. Quando está sozinha em um projeto, como item independente do Pesquisador de Objetos, ela é chamada de dimensão de banco de dados. Por que esta diferença? Porque você pode definir suas propriedades independentemente. Você verá ambos os termos usados na documentação do produto, por isso é útil entender o que significam.  
  
## <a name="next-steps"></a>Próximas etapas  
 Agora que você tem uma melhor compreensão de conceitos e terminologia importantes, prossiga para esses tópicos adicionais que explicam com mais detalhes os conceitos fundamentais no Analysis Services:  
  
-   [A consulta MDX básica &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)  
  
-   [O Script básico de MDX &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)  
  
-   [Modelagem multidimensional &#40; Tutorial do Adventure Works &#41;](../../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Espaço de cubo](../../../analysis-services/multidimensional-models/mdx/cube-space.md)   
 [Tuplas](../../../analysis-services/multidimensional-models/mdx/tuples.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Trabalhando com membros, tuplas e conjuntos de &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Totais visuais e totais não visuais](../../../analysis-services/multidimensional-models/mdx/visual-totals-and-non-visual-totals.md)   
 [Conceitos básicos de consulta MDX &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Conceitos básicos de script MDX &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [Referência de linguagem MDX &#40; MDX &#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [Expressões multidimensionais &#40; MDX &#41; Referência](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
