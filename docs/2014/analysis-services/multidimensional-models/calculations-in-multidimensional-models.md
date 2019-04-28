---
title: Cálculos em modelos multidimensionais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- calculations [Analysis Services], creating
- deleting calculations
- calculations [Analysis Services], scripts
- Cube Designer
- modifying scripts
- removing calculations
- calculations [Analysis Services], deleting
- scripts [Analysis Services], calculations
- cubes [Analysis Services], calculations
- solve orders [Analysis Services]
ms.assetid: c21b3459-9bef-45a2-aba5-c992eba5b66e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a132395bbd95997832e2a1df6948179cb2ffe8aa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726940"
---
# <a name="calculations-in-multidimensional-models"></a>Cálculos em modelos multidimensionais
  Use a guia **Cálculos** do Designer de Cubo para criar membros calculados, conjuntos nomeados e outros cálculos de expressões multidimensionais (MDX).  
  
 A guia **Cálculos** possui três painéis:  
  
-   O painel **Organizador de Script** lista os cálculos de um cubo. Use-o para criar, organizar e selecionar cálculos para edição.  
  
-   O painel **Ferramentas de Cálculo** fornece metadados, funções e modelos com os quais criar cálculos.  
  
-   O painel Expressões de Cálculo oferece suporte a uma exibição de formulário e de script.  
  
> [!NOTE]  
>  Para obter mais informações sobre como criar scripts MDX, consulte [Introduction to MDX Scripting in Microsoft SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=81892)e consulte a seção recursos adicionais sobre o [SQL Server 2005 - Analysis Services](https://go.microsoft.com/fwlink/?LinkId=80853) página sobre o Site da Web do Microsoft TechNet. Para obter mais informações sobre questões de desempenho relacionadas ao design de cubo, consulte o [SQL Server 2005 Analysis Services Performance Guide](https://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="creating-a-new-calculation"></a>Criando um novo cálculo  
 Para criar um novo cálculo, na guia **Cálculos** do Designer de Cubo, no menu **Cubo** , clique em **Novo Membro Calculado**, **Novo Conjunto Nomeado**ou **Novo Comando de Script**, de acordo com o tipo de cálculo que você deseja criar. Você também pode clicar em algum dos botões correspondentes na barra de ferramentas ou clicar com o botão direito do mouse em qualquer lugar do painel **Organizador de Script** e clique em um dos comandos do menu de atalho. Essa ação adiciona um novo cálculo ao painel **Organizador de Script** e exibe campos para ele no formulário de cálculo do painel Expressões de Cálculos. Se você criar um novo script, essa ação abrirá a exibição Script no painel Expressões de Cálculos. Para obter mais informações sobre a criação de três tipos de cálculos, consulte [Criar membros calculados](create-calculated-members.md), [Criar conjuntos nomeados](create-named-sets.md)e [Definir atribuições e outros comandos de Script](define-assignments-and-other-script-commands.md).  
  
## <a name="editing-scripts"></a>Editando scripts  
 Edite os scripts no painel Expressões de Cálculos da guia **Cálculos** . O painel Expressões de Cálculos possui duas exibições, Script e Formulário. A exibição Formulário mostra as expressões e as propriedades de um único comando. Quando você editar um script MDX, uma caixa de expressão preenche a exibição Formulário inteira.  
  
 A exibição Script fornece um editor de código no qual editar os scripts. Enquanto o painel Expressões de Cálculos estiver no modo de exibição Script, o painel **Organizador de Script** ficará oculto. A Exibição de script fornece codificação por cor, correspondência de parênteses, preenchimento automático e regiões de código MDX. As regiões de código MDX podem ser recolhidas ou expandidas para facilitar a edição.  
  
 É possível alternar entre as exibições Formulário e Script, basta clicar no menu **Cubo** , apontar para **Mostrar Cálculos em**e, em seguida, clicar em **Script** ou **Formulário**. Você também pode clicar em **Exibição de Formulário** ou **Exibição de Script** na barra de ferramentas.  
  
## <a name="changing-solve-order"></a>Alterando a ordem de resolução  
 Os cálculos são resolvidos na ordem listada no painel **Organizador de Script** . Você pode reordenar os cálculos clicando com o botão direito do mouse em qualquer cálculo e clicando em **Mover para Cima** ou em **Mover para Baixo** no menu de atalho. Você também pode clicar em um cálculo e, em seguida, clicar no botão **Mover para Cima** ou **Mover para Baixo** na barra de ferramentas.  
  
 Você pode anular essa ordem manualmente para células calculadas e membros calculados. Para obter mais informações sobre a ordem de passagem e de resolução, consulte [Entendendo a ordem de passagem e a ordem de resolução &#40;MDX&#41;](mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
## <a name="deleting-a-calculation"></a>Excluindo um cálculo  
 Para excluir um cálculo existente, na guia **Cálculos** do painel **Organizador de Script** , selecione o cálculo que será excluído e, em seguida, clique em **Excluir** no menu **Editar** ou clique no ícone **Editar** da barra de ferramentas. Você também pode clicar com o botão direito do mouse no cálculo no painel **Organizador de Script** e selecionar **Excluir** no menu de atalho.  
  
  
