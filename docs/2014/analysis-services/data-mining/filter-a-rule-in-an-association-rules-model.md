---
title: Filtrar uma regra em um modelo de regras de associação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- filtering rules [Analysis Services]
- Mining Model Viewer [Analysis Services], rules
- Rules Viewer
ms.assetid: 26cdba5b-5bf1-439e-80a3-8759774e918b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b63a6d6da0cb1d489ecac418e2682590ea2164e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084407"
---
# <a name="filter-a-rule-in-an-association-rules-model"></a>Filtrar uma regra em um modelo de regras de associação
  Você pode usar a filtragem com modelos de associação para restringir os resultados a apenas as associações do seu interesse. Por exemplo, você pode filtrar as regras para mostrar apenas aquelas que incluem um produto específico.  
  
 No Designer de Mineração de Dados, você pode usar os controles na guia **Regras** do Visualizador de Regras de Associação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para filtrar as regras que são exibidas.  Você também pode criar uma consulta no modelo para ver apenas o conjunto de itens que contém um valor específico.  
  
> [!NOTE]  
>  Esta opção só está disponível para modelos de mineração que foram criados com o Algoritmo de Associação da Microsoft.  
  
### <a name="filter-a-rule-in-an-association-model"></a>Filtrar uma regra em um modelo de associação  
  
1.  Abra o modelo de mineração usando o **Visualizador de Regras de Associação**. Para fazer isso no SQL Server Management Studio, clique com o botão direito do mouse no nome do modelo e selecione **Procurar**. Para fazer isso no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique duas vezes na estrutura de mineração que contém o modelo e clique na guia **Visualizador do Modelo de Mineração** do **Designer de Mineração de Dados**.  
  
2.  Clique na guia **Regras** do **Visualizador de Regras de Associação**.  
  
3.  Digite em uma condição de regra na caixa **Filtrar Regra** . Por exemplo, uma condição de regra poderia ser "Posto de Bicicleta" que também retorna "Postos de Bicicleta."  
  
     A caixa de texto **Regra do Filtro** dá suporte a expressões regulares conforme a definição da linguagem .NET. Por isso, é possível usar expressões como as seguintes: `((.Helmets.*Fenders.*)|(.*Fenders.*Helmets.*))`. Essa expressão retornaria qualquer conjuntos de itens que incluísse atributos com as palavras Helmets e Fenders, em qualquer ordem.  
  
4.  Para **Probabilidade mínima**, aumente o valor da probabilidade para exibir menos regras ou diminua o valor para exibir mais regras.  
  
5.  Para **Importância mínima**, aumente o valor da importância para exibir menos regras ou diminua o valor para exibir mais regras.  
  
6.  Para **Mostrar**, selecione um das seguintes opções: **Mostrar nome e valor do atributo**, **Mostrar apenas o nome de atributo**ou **Mostrar apenas o valor de atributo**.  
  
7.  Para **Máximo de linhas**, aumente o valor para aumentar o número total de regras que atendem às condições especificadas ou diminua o valor para limitar o número de regras retornadas. As regras são ordenadas por probabilidade, assim você poderia eliminar regras adicionais que atendem às condições especificadas de probabilidade ou importância.  
  
8.  Marque ou desmarque a caixa de seleção **Mostrar nome longo** para alternar o modo como os nomes de regras são exibidos.  
  
     As regras agora são filtradas para exibir apenas as regras de exibição que contenham o item indicado. A condição de filtro se aplica a valores de atributo antes ou depois do delimitador de regra, "->".  
  
    > [!NOTE]  
    >  O visualizador armazena em cache a lista inicial de regras, baseado em uma consulta para o modelo de mineração, e não atualiza a lista de regras a menos que você altere as condições da consulta definindo o máximo de linhas, a probabilidade, importância ou a exibição de nomes longos. Por isso, se digitar uma condição e a exibição não for atualizada imediatamente, você poderá forçar o visualizador a atualizar os dados, marcando e desmarcando a caixa de seleção **Mostrar nomes longos** .  
  
### <a name="create-a-query-on-the-itemsets-in-an-association-model"></a>Criar uma consulta nos conjuntos de itens em um modelo de associação  
  
-   [Exemplos de consulta de um modelo de associação](association-model-query-examples.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções do Visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Procurar um modelo usando o Visualizador de regras de associação da Microsoft](browse-a-model-using-the-microsoft-association-rules-viewer.md)   
 [Lição 3: Criando um cenário de cesta de mercado &#40;tutorial de mineração de dados intermediário&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
  
