---
title: Sinalizadores de modelagem (mineração de dados) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f644f882d1a252f678d868d3492b4aed4e11006f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509988"
---
# <a name="modeling-flags-data-mining"></a>Sinalizadores de modelagem (Mineração de Dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Use sinalizadores de modelagem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para fornecer informações adicionais para um algoritmo de mineração de dados sobre os dados definidos em uma tabela de casos. O algoritmo pode usar essas informações para criar um modelo de mineração de dados mais preciso.  
  
 Alguns sinalizadores de modelagem são definidos no nível da estrutura de mineração, enquanto outros são definidos no nível de coluna do modelo de mineração. Por exemplo, o sinalizador de modelagem **NOT NULL** é usado com colunas da estrutura de mineração. Você pode definir sinalizadores de modelagem adicionais nas colunas de modelo de mineração, dependendo do algoritmo usado para criar o modelo.  
  
> [!NOTE]  
>  Plug-ins de terceiros podem ter outros sinalizadores de modelagem, além daqueles predefinidos pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="list-of-modeling-flags"></a>Lista de sinalizadores de modelagem  
 A lista a seguir descreve os sinalizadores de modelagem suportados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter informações sobre como os sinalizadores de modelagem têm suporte de algoritmos específicos, consulte o tópico de referência técnica do algoritmo que foi usado para criar o modelo.  
  
 **NOT NULL**  
 Indica que os valores da coluna de atributo não devem jamais conter um valor nulo. Ocorrerá um erro se o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] encontrar um valor nulo nessa coluna de atributo durante o processo de treinamento do modelo.  
  
 **MODEL_EXISTENCE_ONLY**  
 Indica que a coluna será tratada como tendo dois estados: **Faltando** e **existentes**. Se o valor for **NULL**, será tratado como Missing. O sinalizador MODEL_EXISTENCE_ONLY é aplicado ao atributo previsível e tem suporte pela maioria dos algoritmos.  
  
 De fato, definir o sinalizador MODEL_EXISTENCE_ONLY para **verdadeira** alterar a representação dos valores de modo que haja somente dois estados: **Faltando** e **existentes**. Todos os estados não ausentes são combinados em um único valor **Existente** .  
  
 Um uso comum desse sinalizador de modelagem seria em atributos para os quais o estado **NULL** tem um significado implícito e o valor explícito do estado **NOT NULL** pode não ser tão importante quanto o fato de que a coluna possui algum valor. Por exemplo, uma coluna [DateContractSigned] pode ser **NULL** se nunca houve um contrato assinado e **NOT NULL** se o contrato foi assinado. Portanto, se o objetivo do modelo é prever se um contrato será assinado, você pode usar o sinalizador MODEL_EXISTENCE_ONLY para ignorar o valor da data exata dos casos **NOT NULL** e distinguir somente os casos em que um contrato seja **Ausente** ou **Existente**.  
  
> [!NOTE]  
>  Missing é um estado especial usado pelo algoritmo e difere do valor de texto "Missing" em uma coluna. Para obter mais informações, consulte [Valores ausentes &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
 **REGRESSOR**  
 Indica que a coluna é uma candidata a ser usada como um regressor durante o processamento. Este sinalizador é definido em uma coluna de modelo de mineração e só pode ser aplicado a colunas com um tipo de dados numérico contínuo. Para obter mais informações sobre o uso desse sinalizador, consulte a seção neste tópico [Usos do sinalizador de modelagem REGRESSOR](#bkmk_UseRegressors).  
  
## <a name="viewing-and-changing-modeling-flags"></a>Exibindo e alterando sinalizadores de modelagem  
 É possível exibir os sinalizadores de modelagem associados a uma coluna de estrutura de mineração ou uma coluna de modelo no Designer de Mineração de Dados ao exibir as propriedades da estrutura ou do modelo.  
  
 Para determinar quais sinalizadores de modelagem foram aplicados à estrutura de mineração atual, você pode criar uma consulta no conjunto de linhas de esquema de mineração de dados que retorna os sinalizadores de modelagem somente para as colunas de estrutura, usando uma consulta como a seguinte:  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_STRUCTURE_COLUMNS  
WHERE STRUCTURE_NAME = '<structure name>'  
```  
  
 Você pode adicionar ou alterar os sinalizadores de modelagem usado em um modelo usando o Designer de Mineração de Dados e editando as propriedades das colunas associadas. Essas alterações exigem que a estrutura ou modelo sejam reprocessados.  
  
 Você pode especificar os sinalizadores de modelagem em uma nova estrutura de mineração ou modelo de mineração usando DMX, ou usando AMO ou scripts XMLA. No entanto, não é possível alterar os sinalizadores de modelagem usados em um modelo e em uma estrutura de mineração existentes com o uso de DMX. Você deve criar um novo modelo de mineração usando a sintaxe `ALTER MINING STRUCTURE....ADD MINING MODEL`.  
  
##  <a name="bkmk_UseRegressors"></a> Usos do sinalizador de modelagem REGRESSOR  
 Ao definir o sinalizador de modelagem REGRESSOR em uma coluna, você está indicando ao algoritmo que essa coluna contém possíveis regressores. Os regressores reais usados no modelo são determinados pelo algoritmo. Um regressor potencial poderá ser descartado se não modelar o atributo previsível.  
  
 Quando você construir um modelo usando o Assistente de Mineração de Dados, todas as colunas de entrada contínuas serão sinalizadas como possíveis regressores. Portanto, mesmo que você não defina explicitamente um sinalizador REGRESSOR em uma coluna, ela poderá ser usada como um regressor no modelo.  
  
 Para determinar os regressores que foram realmente usados no modelo processado, realize uma consulta em um conjunto de linhas do esquema do modelo de mineração, conforme mostrado neste exemplo:  
  
```  
SELECT COLUMN_NAME, MODELING_FLAG  
FROM $system.DMSCHEMA_MINING_COLUMNS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 **Observação** Se você modificar um modelo de mineração e alterar o tipo de conteúdo de uma coluna de contínuo para discreto, terá que alterar manualmente o sinalizador da coluna de mineração e, em seguida, processar novamente o modelo.  
  
### <a name="regressors-in-linear-regression-models"></a>Regressor em modelos de regressão lineares  
 Os modelos de regressão lineares baseiam-se no algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Mesmo que você não use o algoritmo Regressão Linear da [!INCLUDE[msCoName](../../includes/msconame-md.md)] , todo modelo de árvore de decisão poderá conter uma árvore ou nós que representam uma regressão em um atributo contínuo.  
  
 Portanto, nesses modelos, não é necessário especificar que uma coluna contínua representa um regressor. O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] particionará o conjunto de dados em regiões com padrões significativos mesmo que você não defina o sinalizador REGRESSOR na coluna. A diferença é que, quando você define o sinalizador de modelagem, o algoritmo tenta encontrar equações de regressão no seguinte formato de acordo com os padrões dos nós da árvore.  
  
 a\*C1 + b\*C2 + ...  
  
 Em seguida, a soma dos restos é calculada e, se o desvio for muito grande, será forçada uma divisão da árvore.  
  
 Por exemplo, se você estiver prevendo o comportamento de compra dos clientes usando **Renda** como um atributo e definir o sinalizador de modelagem REGRESSOR na coluna, o algoritmo primeiro tentará adequar-se aos valores de **Renda** usando uma fórmula de regressão padrão. Se o desvio for muito grande, a fórmula de regressão será abandonada e a árvore será dividida em algum outro atributo. O algoritmo árvore de decisão tentará então ajustar um regressor para income em cada uma das ramificações após a divisão.  
  
 Você pode usar o parâmetro FORCE_REGRESSOR para garantir que o algoritmo usará determinado regressor. Esse parâmetro pode ser usado com o algoritmo Árvores de Decisão e com o algoritmo Regressão Linear.  
  
## <a name="related-tasks"></a>Related Tasks  
 Use os links a seguir para saber mais sobre como usar sinalizadores de modelagem.  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Editar sinalizadores de modelagem usando o Designer de Mineração de Dados|[Exibir ou alterar sinalizadores de modelagem &#40;Mineração de dados&#41;](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)|  
|Especifique uma dica para o algoritmo recomendar regressores prováveis|[Especificar uma coluna para usar como regressor em um modelo](../../analysis-services/data-mining/specify-a-column-to-use-as-regressor-in-a-model.md)|  
|Veja os sinalizadores de modelagem que têm suporte por algoritmos específicos (na seção Sinalizadores de Modelagem para cada tópico de referência de algoritmo).|[Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)|  
|Saiba mais sobre as colunas da estrutura de mineração e as propriedades que você pode definir nelas|[Colunas da estrutura de mineração](../../analysis-services/data-mining/mining-structure-columns.md)|  
|Saiba sobre as colunas do modelo de mineração e sinalizadores de modelagem que podem ser aplicados no nível do modelo|[Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md)|  
|Consulte a sintaxe para trabalhar com sinalizadores de modelagem em instruções DMX|[Sinalizadores de modelagem &#40;DMX&#41;](../../dmx/modeling-flags-dmx.md)|  
|Entender valores ausentes e como trabalhar com eles|[Valores ausentes &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)|  
|Saiba sobre como gerenciar modelos e estruturas e definir propriedades de uso|[Movendo objetos de mineração de dados](../../analysis-services/data-mining/moving-data-mining-objects.md)|  
  
  
