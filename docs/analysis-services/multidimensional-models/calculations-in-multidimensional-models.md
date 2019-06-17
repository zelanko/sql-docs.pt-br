---
title: Cálculos em modelos multidimensionais | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c72d43c95013074051356c690ac2d7abf0a575e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62990507"
---
# <a name="calculations-in-multidimensional-models"></a>Cálculos em modelos multidimensionais
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Use a guia **Cálculos** do Designer de Cubo para criar membros calculados, conjuntos nomeados e outros cálculos de expressões multidimensionais (MDX).  
  
 A guia **Cálculos** possui três painéis:  
  
-   O painel **Organizador de Script** lista os cálculos de um cubo. Use-o para criar, organizar e selecionar cálculos para edição.  
  
-   O painel **Ferramentas de Cálculo** fornece metadados, funções e modelos com os quais criar cálculos.  
  
-   O painel Expressões de Cálculo oferece suporte a uma exibição de formulário e de script.  
  
  
## <a name="creating-a-new-calculation"></a>Criando um novo cálculo  
 Para criar um novo cálculo, na guia **Cálculos** do Designer de Cubo, no menu **Cubo** , clique em **Novo Membro Calculado**, **Novo Conjunto Nomeado**ou **Novo Comando de Script**, de acordo com o tipo de cálculo que você deseja criar. Você também pode clicar em algum dos botões correspondentes na barra de ferramentas ou clicar com o botão direito do mouse em qualquer lugar do painel **Organizador de Script** e clique em um dos comandos do menu de atalho. Essa ação adiciona um novo cálculo ao painel **Organizador de Script** e exibe campos para ele no formulário de cálculo do painel Expressões de Cálculos. Se você criar um novo script, essa ação abrirá a exibição Script no painel Expressões de Cálculos. Para obter mais informações sobre a criação de três tipos de cálculos, consulte [Criar membros calculados](../../analysis-services/multidimensional-models/create-calculated-members.md), [Criar conjuntos nomeados](../../analysis-services/multidimensional-models/create-named-sets.md)e [Definir atribuições e outros comandos de Script](../../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md).  
  
## <a name="editing-scripts"></a>Editando scripts  
 Edite os scripts no painel Expressões de Cálculos da guia **Cálculos** . O painel Expressões de Cálculos possui duas exibições, Script e Formulário. A exibição Formulário mostra as expressões e as propriedades de um único comando. Quando você editar um script MDX, uma caixa de expressão preenche a exibição Formulário inteira.  
  
 A exibição Script fornece um editor de código no qual editar os scripts. Enquanto o painel Expressões de Cálculos estiver no modo de exibição Script, o painel **Organizador de Script** ficará oculto. A Exibição de script fornece codificação por cor, correspondência de parênteses, preenchimento automático e regiões de código MDX. As regiões de código MDX podem ser recolhidas ou expandidas para facilitar a edição.  
  
 É possível alternar entre as exibições Formulário e Script, basta clicar no menu **Cubo** , apontar para **Mostrar Cálculos em**e, em seguida, clicar em **Script** ou **Formulário**. Você também pode clicar em **Exibição de Formulário** ou **Exibição de Script** na barra de ferramentas.  
  
## <a name="changing-solve-order"></a>Alterando a ordem de resolução  
 Os cálculos são resolvidos na ordem listada no painel **Organizador de Script** . Você pode reordenar os cálculos clicando com o botão direito do mouse em qualquer cálculo e clicando em **Mover para Cima** ou em **Mover para Baixo** no menu de atalho. Você também pode clicar em um cálculo e, em seguida, clicar no botão **Mover para Cima** ou **Mover para Baixo** na barra de ferramentas.  
  
 Você pode anular essa ordem manualmente para células calculadas e membros calculados. Para obter mais informações sobre a ordem de passagem e de resolução, consulte [Entendendo a ordem de passagem e a ordem de resolução &#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
## <a name="deleting-a-calculation"></a>Excluindo um cálculo  
 Para excluir um cálculo existente, na guia **Cálculos** do painel **Organizador de Script** , selecione o cálculo que será excluído e, em seguida, clique em **Excluir** no menu **Editar** ou clique no ícone **Editar** da barra de ferramentas. Você também pode clicar com o botão direito do mouse no cálculo no painel **Organizador de Script** e selecionar **Excluir** no menu de atalho.  
  
  
