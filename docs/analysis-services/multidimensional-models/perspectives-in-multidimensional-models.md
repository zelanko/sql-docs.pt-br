---
title: "Perspectivas em modelos multidimensionais | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "membros padrão"
  - "ocultando objetos de perspectiva"
  - "renomeando perspectivas"
  - "atributos [Analysis Services], membros padrão"
  - "removendo perspectivas"
  - "perspectivas [Analysis Services]"
  - "nomes [Analysis Services], perspectivas"
  - "cubos [Analysis Services], perspectivas"
  - "excluindo perspectivas"
ms.assetid: 5a3d6577-6833-4c24-820c-b65bb856157b
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 28
---
# Perspectivas em modelos multidimensionais
  Uma perspectiva é um subconjunto de um cubo criado para um determinado aplicativo ou grupo de usuários. O próprio cubo é a perspectiva padrão. Uma perspectiva é exposta a um cliente como um cubo. Quando um usuário exibe uma perspectiva, ela aparece como outro cubo. Toda alteração feita nos dados do cubo por meio de write-back da perspectiva é aplicada ao cubo original. Para obter mais informações sobre exibições no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Perspectivas](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md).  
  
 Use a guia **Perspectivas** do Designer de Cubo para criar ou modificar perspectivas em um cubo. A primeira coluna da guia **Perspectivas** é **Objetos Cubo** , que lista todos os objetos do cubo. Corresponde à perspectiva padrão do cubo, que é o próprio cubo.  
  
## Criando ou excluindo perspectivas  
 Você pode adicionar uma perspectiva à guia **Perspectivas** clicando em **Nova Perspectiva** no menu **Cubo** . Pode também clicar no botão **Nova Perspectiva** na barra de ferramentas ou clicar com o botão direito do mouse no painel e clicar em **Nova Perspectiva** no menu de atalho. É possível adicionar qualquer número de perspectivas a um cubo.  
  
 Para remover uma perspectiva, primeiro clique em qualquer célula da coluna da perspectiva que você deseja excluir. Em seguida, no menu **Cubo** , clique em **Excluir Perspectiva**. Você também pode clicar no botão **Excluir Perspectiva** na barra de ferramentas ou clicar com o botão direito do mouse em uma célula da perspectiva que deseja excluir e, em seguida, clicar em **Excluir Perspectiva** no menu de atalho.  
  
## Renomeando perspectivas  
 A primeira linha de cada perspectiva mostra seu nome. Quando você cria uma perspectiva, inicialmente, o nome é Perspectiva (seguido por um número ordinal, começando em 1, se já existir uma perspectiva chamada Perspectiva). Clique no nome se quiser editá-lo.  
  
## Ocultando objetos de uma perspectiva  
 Para ocultar um objeto de uma perspectiva, desmarque a caixa de seleção da linha correspondente ao objeto na coluna da perspectiva. Os objetos de cubo que podem ser ocultados de uma perspectiva são:  
  
-   Grupos de medidas  
  
-   Medidas  
  
-   Dimensões  
  
-   Hierarquias  
  
-   Conjuntos nomeados  
  
-   KPIs  
  
-   Ações  
  
-   Membros calculados  
  
 Para exibir algum dos objetos, expanda a categoria (**Grupos de Medidas**, **Dimensões**, **KPIs**, **Cálculos** ou **Ações**) de qualquer tipo de objeto de **Objetos Cubo**. Para exibir hierarquias ou atributos de uma dimensão, primeiro expanda a dimensão e, em seguida, expanda a linha **Hierarquias** ou **Atributos** . Para exibir medidas de um grupo de medidas, expanda o grupo de medidas.  
  
## Consulte também  
 [Cubos em modelos multidimensionais](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  