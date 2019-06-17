---
title: Modificando medidas | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9a9d0559a0421d8badd5e939a85947a53e0f6e8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403948"
---
# <a name="lesson-3-1---modifying-measures"></a>Lição 3-1: modificando medidas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Você pode usar a propriedade **FormatString** para definir configurações de formatação que controlam como as medidas são exibidas aos usuários. Nesta tarefa, você especificará propriedades de formatação para as medidas moeda e porcentagem do cubo do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
### <a name="to-modify-the-measures-of-the-cube"></a>Para modificar as medidas do cubo  
  
1.  Mude para a guia **Estrutura do Cubo** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , expanda o grupo de medidas **Vendas pela Internet** no painel **Medidas** , clique com o botão direito do mouse em **Quantidade de Pedidos**e clique em **Propriedades**.  
  
2.  Na janela Propriedades, clique no ícone de pino **Ocultar Automaticamente** para manter a janela Propriedades aberta.  
  
    É mais fácil alterar as propriedades de vários itens no cubo quando a janela Propriedades permanece aberta.  
  
3.  Na janela Propriedades, clique na lista **FormatString** e digite **#,#** .  
  
4.  Na barra de ferramentas da guia **Estrutura do Cubo** , clique no ícone **Mostrar Grade de Medidas** à esquerda.  
  
    A exibição das grades permite que você selecione várias medidas ao mesmo tempo.  
  
5.  Selecione as medidas a seguir. Você pode selecionar várias medidas clicando em cada uma enquanto mantém pressionada a tecla CTRL.  
  
    -   **Preço Unitário**  
  
    -   **Valor Ampliado**  
  
    -   **Valor de desconto**  
  
    -   **Custo Padrão do Produto**  
  
    -   **Custo Total do Produto**  
  
    -   **Valor das Vendas**  
  
    -   **Valor dos Impostos**  
  
    -   **Freight**  
  
6.  Na janela Propriedades, na lista **FormatString** , selecione **Moeda**.  
  
7.  Na lista suspensa na parte superior da janela Propriedades (logo abaixo da barra de título), selecione a medida **Percentual de Desconto no Preço Unitário**e **Percentual** na lista **FormatString** .  
  
8.  Na janela Propriedades, altere a propriedade **Name** da medida **Porcentagem de Desconto no Preço Unitário** para **Porcentagem de Desconto no Preço Unitário**.  
  
9. No painel **Medidas** , clique em **Valor dos Impostos** e altere o nome dessa medida para **Valor dos Impostos**.  
  
10. Na janela Propriedades, clique no ícone **Ocultar Automaticamente** para ocultar a janela Propriedades. Depois, clique em **Mostrar Árvore de Medidas** na barra de ferramentas da guia **Estrutura do Cubo** .  
  
11. No menu **Arquivo** , clique em **Salvar Tudo**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Modificando a dimensão Cliente](lesson-3-2-modifying-the-customer-dimension.md)  
  
## <a name="see-also"></a>Consulte também  
[Definir as dimensões do banco de dados](../multidimensional-models/define-database-dimensions.md)  
[Configurar propriedades de medida](../multidimensional-models/configure-measure-properties.md)  
  
  
  
