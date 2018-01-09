---
title: Perspectivas em modelos multidimensionais | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- default members
- hiding objects from perspective
- renaming perspectives
- attributes [Analysis Services], default members
- removing perspectives
- perspectives [Analysis Services]
- names [Analysis Services], perspectives
- cubes [Analysis Services], perspectives
- deleting perspectives
ms.assetid: 5a3d6577-6833-4c24-820c-b65bb856157b
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 94508cf2bb7347d3b8cef15ce5c743f33c04a018
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="perspectives-in-multidimensional-models"></a>Perspectivas em modelos multidimensionais
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Uma perspectiva é um subconjunto de um cubo criado para um determinado aplicativo ou grupo de usuários. O próprio cubo é a perspectiva padrão. Uma perspectiva é exposta a um cliente como um cubo. Quando um usuário exibe uma perspectiva, ela aparece como outro cubo. Toda alteração feita nos dados do cubo por meio de write-back da perspectiva é aplicada ao cubo original. Para obter mais informações sobre exibições no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Perspectivas](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md).  
  
 Use a guia **Perspectivas** do Designer de Cubo para criar ou modificar perspectivas em um cubo. A primeira coluna da guia **Perspectivas** é **Objetos Cubo** , que lista todos os objetos do cubo. Corresponde à perspectiva padrão do cubo, que é o próprio cubo.  
  
## <a name="creating-or-deleting-perspectives"></a>Criando ou excluindo perspectivas  
 Você pode adicionar uma perspectiva à guia **Perspectivas** clicando em **Nova Perspectiva** no menu **Cubo** . Pode também clicar no botão **Nova Perspectiva** na barra de ferramentas ou clicar com o botão direito do mouse no painel e clicar em **Nova Perspectiva** no menu de atalho. É possível adicionar qualquer número de perspectivas a um cubo.  
  
 Para remover uma perspectiva, primeiro clique em qualquer célula da coluna da perspectiva que você deseja excluir. Em seguida, no menu **Cubo** , clique em **Excluir Perspectiva**. Você também pode clicar no botão **Excluir Perspectiva** na barra de ferramentas ou clicar com o botão direito do mouse em uma célula da perspectiva que deseja excluir e, em seguida, clicar em **Excluir Perspectiva** no menu de atalho.  
  
## <a name="renaming-perspectives"></a>renomeando perspectivas  
 A primeira linha de cada perspectiva mostra seu nome. Quando você cria uma perspectiva, inicialmente, o nome é Perspectiva (seguido por um número ordinal, começando em 1, se já existir uma perspectiva chamada Perspectiva). Clique no nome se quiser editá-lo.  
  
## <a name="hiding-objects-from-a-perspective"></a>Ocultando objetos de uma perspectiva  
 Para ocultar um objeto de uma perspectiva, desmarque a caixa de seleção da linha correspondente ao objeto na coluna da perspectiva. Os objetos de cubo que podem ser ocultados de uma perspectiva são:  
  
-   Grupos de medidas  
  
-   medidas  
  
-   Dimensões  
  
-   Hierarquias  
  
-   Conjuntos nomeados  
  
-   KPIs  
  
-   Ações  
  
-   Membros calculados  
  
 Para exibir algum dos objetos, expanda a categoria (**Grupos de Medidas**, **Dimensões**, **KPIs**, **Cálculos**ou **Ações**) de qualquer tipo de objeto de **Objetos Cubo**. Para exibir hierarquias ou atributos de uma dimensão, primeiro expanda a dimensão e, em seguida, expanda a linha **Hierarquias** ou **Atributos** . Para exibir medidas de um grupo de medidas, expanda o grupo de medidas.  
  
## <a name="see-also"></a>Consulte Também  
 [Cubos em modelos multidimensionais](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
