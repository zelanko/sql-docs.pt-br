---
title: "Tipos de conte&#250;do (minera&#231;&#227;o de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "colunas [mineração de dados], tipos de conteúdo"
  - "Coluna KEY SEQUENCE"
  - "tipos de conteúdo (mineração de dados)"
  - "atributos [mineração de dados]"
  - "Coluna DISCRETIZED"
  - "Colunas CONTINUOUS"
  - "Coluna CYCLICAL"
  - "Coluna ORDERED"
  - "colunas diferenciadas [mineração de dados]"
  - "colunas discretas [Analysis Services]"
  - "Coluna DISCRETE"
  - "Coluna KEY"
  - "Coluna KEY TIME"
  - "colunas contínuas"
  - "codificação [mineração de dados]"
ms.assetid: 2dacd968-70e8-4993-88b6-a6d36024a4e4
caps.latest.revision: 42
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 42
---
# Tipos de conte&#250;do (minera&#231;&#227;o de dados)
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode definir o tipo de dados físico para uma coluna em uma estrutura de mineração e um tipo de conteúdo lógico para a coluna quando usada em um modelo.  
  
 O *tipo de dados* determina como os algoritmos processarão os dados nessas colunas quando você criar modelos de mineração. A definição do tipo de dados de uma coluna dá ao algoritmo informações sobre o tipo de dados nas colunas e como processar os dados. Cada tipo de dados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte a um ou mais tipos de conteúdo de mineração de dados.  
  
 O *tipo de conteúdo* descreve o comportamento do conteúdo existente na coluna. Por exemplo, se o conteúdo em uma coluna for repetido em um intervalo específico, como dias da semana, você poderá especificar o tipo de conteúdo dessa coluna como cíclico.  
  
 Alguns algoritmos exigem tipos de dados e de conteúdo específicos para que funcionem corretamente. Por exemplo, o algoritmo Microsoft Naive Bayes não pode usar colunas contínuas como entrada, nem prever valores contínuos. Alguns tipos de conteúdo, como Key Sequence, só são usados por um algoritmo específico. Para obter uma lista dos algoritmos e dos tipos de conteúdo que cada um dá suporte, consulte [Algoritmos de mineração de dados &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 A lista a seguir descreve os tipos de conteúdo usados na mineração de dados e identifica os tipos de dados que oferecem suporte para cada tipo.  
  
## Discreto  
 *Discreto* significa que a coluna contém um número finito de valores sem continuidade entre eles. Por exemplo, uma coluna de gênero é uma coluna típica do atributo discreto, pois os dados representam um número específico de categorias.  
  
 Os valores em uma coluna de atributo discreto não podem envolver ordenação, mesmo que os valores sejam numéricos. Além disso, mesmo que os valores usados na coluna discreta sejam numéricos, não será possível calcular valores fracionários. Os códigos de área de telefone são um bom exemplo de dados numéricos discretos.  
  
 O tipo de conteúdo **Discrete** é suportado por todos os tipos de dados de mineração de dados.  
  
## Contínuo  
 *Contínuo* significa que a coluna contém valores que representam dados numéricos em uma escala que permite valores provisórios. Diferente da coluna discreta, que representa dados contáveis finitos, uma coluna contínua representa medições escaláveis e é possível que os dados contenham um número infinito de valores fracionários. Uma coluna de temperaturas é um exemplo de uma coluna do atributo contínuo.  
  
 Quando uma coluna contém dados numéricos contínuos, e você sabe como os dados devem ser distribuídos, é possível melhorar a precisão da análise especificando a distribuição esperada de valores. Especifique a distribuição de coluna no nível da estrutura de mineração. Assim, a configuração se aplica a todos os modelos que se baseiam na estrutura. Para obter mais informações, consulte [Distribuições de coluna &#40;Mineração de dados&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md).  
  
 O tipo de conteúdo **Continuous** é suportado pelos seguintes tipos de dados: **Date**, **Double**e **Long**.  
  
## Discretizado  
 *Discretização* é o processo que coloca valores de um conjunto contínuo de dados em buckets de modo a ter um número limitado de valores possíveis. É possível discretizar apenas dados numéricos.  
  
 Assim, o tipo de conteúdo *discretized* indica que a coluna contém valores que representam grupos ou recipientes de valores que são derivados de uma coluna contínua. Os blocos são tratados como valores ordenados e discretos.  
  
 Você pode discretizar os dados manualmente para garantir que terá os recipientes desejados ou pode usar os métodos de discretização fornecidos pelo SQL Server Analysis Services. Alguns algoritmos executam a discretização automaticamente. Para obter mais informações, consulte [Alterar a discretização de uma coluna em um modelo de mineração](../../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md).  
  
 O tipo de conteúdo **Discretized** é suportado pelos seguintes tipos de dados: **Date**, **Double**, **Long**e **Text**.  
  
## Chave  
 O tipo de conteúdo *key* significa que a coluna identifica uma linha exclusivamente. Normalmente, em uma tabela de casos, a coluna de chave é um identificador numérico ou de texto. Defina o tipo de conteúdo como **key** para indicar que a coluna não deve ser usada para análise, somente para registros de monitoramento.  
  
 Tabelas aninhadas também têm chaves, mas o uso da chave de tabela aninhada é um pouco diferente. Defina o tipo de conteúdo como **key** na tabela aninha se a coluna for o atributo que você deseja analisar. Os valores da chave da tabela aninhada devem ser exclusivos para cada caso, mas podem ser duplicados em todo um conjunto de casos.  
  
 Por exemplo, se você estiver analisando os produtos que os clientes compraram, poderia definir o tipo de conteúdo como chave na coluna **CustomerID** da tabela de casos e o tipo de conteúdo novamente como chave na coluna **PurchasedProducts** da tabela aninhada.  
  
> [!NOTE]  
>  Tabelas aninhadas estarão disponíveis somente se você usar dados de uma fonte de dados externa que foi definida como uma exibição da fonte de dados do Analysis Services.  
  
 Esse tipo de conteúdo tem suporte dos seguintes tipos de dados: **Date**, **Double**, **Long**e **Text**.  
  
## Key Sequence  
 O tipo de conteúdo *key sequence* somente pode ser usado em modelos de clustering de sequência. Quando você define o tipo de conteúdo como **key sequence**, ele indica que a coluna contém valores que representam uma sequência de eventos. Os valores são ordenados, mas a distância entre eles não precisa ser igual.  
  
 Esse tipo de conteúdo tem suporte dos seguintes tipos de dados: **Double**, **Long**, **Text**e **Date**.  
  
## Key Time  
 O tipo de conteúdo *key time* somente pode ser usado em modelos de série temporal. Quando você define o tipo de conteúdo como **key time**, isso indica que os valores são ordenados e representam uma escala de tempo.  
  
 Esse tipo de conteúdo é suportado pelos seguintes tipos de dados: **Double**, **Long**e **Date**.  
  
## Table  
 O tipo de conteúdo *table* indica que a coluna contém outra tabela de dados, com uma ou mais colunas e uma ou mais linhas. Para uma linha específica da tabela de casos, essa coluna pode conter diversos valores, todos relacionados ao registro de casos pai. Por exemplo, se a tabela de casos principal contiver uma lista de clientes, você poderá ter várias colunas contendo tabelas aninhadas, como uma coluna **ProductsPurchased** , onde a tabela aninhada lista os produtos comprados por esse cliente no passado, e a coluna **Hobbies** que lista os interesses do cliente.  
  
 O tipo de dados dessa coluna é sempre **Table**.  
  
## Cyclical  
 O tipo de conteúdo *cyclical* significa que a coluna contém valores que representam um conjunto ordenado cíclico. Por exemplo, os dias numerados da semana são um conjunto cíclico ordenado, pois o dia de número um segue o dia de número sete.  
  
 As colunas cíclicas são consideradas tanto ordenadas como discretas em termos de tipo de conteúdo.  
  
 Esse tipo de conteúdo é suportado por todos os tipos mineração de dados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. No entanto, a maioria dos algoritmos trata valores cíclicos como valores discretos e não executa processamento especial.  
  
## Ordered  
 O tipo de conteúdo *Ordered* também indica que a coluna contém valores que definem uma sequência ou ordem. No entanto, nesse tipo de conteúdo, os valores usados na ordenação não implicam nenhuma relação de distância ou magnitude entre os valores do conjunto. Por exemplo, se a coluna de atributo ordenada contiver informações sobre os níveis de habilidades em ordem de classificação de um a cinco, não há informações insinuadas na distância entre os níveis de habilidades, um nível de habilidades de cinco não é necessariamente cinco vezes melhor que um nível de habilidades de nível um.  
  
 As colunas de atributo ordenada são consideradas discretas em termos de tipo de conteúdo.  
  
 Esse tipo de conteúdo é suportado por todos os tipos mineração de dados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. No entanto, a maioria dos algoritmos trata valores ordenados como valores discretos e não executa processamento especial.  
  
## Classificados  
 Além dos tipos de conteúdo anteriores, usados normalmente com todos os modelos, você pode usar colunas classificadas para definir os tipos de conteúdo para alguns tipos de dados. Para obter mais informações sobre as colunas classificadas, consulte [Colunas classificadas &#40;Mineração de dados&#41;](../../analysis-services/data-mining/classified-columns-data-mining.md).  
  
## Consulte também  
 [Tipos de conteúdo &#40;DMX&#41;](../../dmx/content-types-dmx.md)   
 [Tipos de dados &#40;Mineração de dados&#41;](../../analysis-services/data-mining/data-types-data-mining.md)   
 [Tipos de dados &#40;DMX&#41;](../../dmx/data-types-dmx.md)   
 [Alterar as propriedades de uma estrutura de mineração](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)   
 [Colunas da estrutura de mineração](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  