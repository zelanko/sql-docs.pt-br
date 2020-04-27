---
title: Adicionar, alterar ou excluir valores disponíveis para um parâmetro de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportparameters.availablevalues.f1
- "10455"
- "10071"
ms.assetid: 0e03264c-523f-4c59-b71b-ceef600f75f6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e9944e437be03dd7cfac3cbe6bad7c5224f3b462
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106674"
---
# <a name="add-change-or-delete-available-values-for-a-report-parameter-report-builder-and-ssrs"></a>Adicionar, alterar ou excluir valores disponíveis para um parâmetro de relatório (Construtor de Relatórios e SSRS)
  Depois de criar um parâmetro de relatório, você poderá especificar uma lista de valores disponíveis a ser exibida para o usuário. Uma lista de valores disponíveis limita as escolhas do usuário aos valores válidos para o parâmetro.  
  
 Os valores disponíveis são exibidos em uma lista suspensa ao lado do parâmetro de relatório na barra de ferramentas quando o relatório é executado. Os parâmetros de relatório podem representar um valor ou diversos valores. No caso de diversos valores, a lista começa com um recurso **Selecionar Tudo** , através do qual o usuário pode selecionar ou desmarcar todos os valores com um só clique.  
  
 É possível fornecer uma lista de valores estática ou uma lista baseada em um conjunto de dados de relatório. Se preferir, você pode especificar um nome amigável para os valores usando um campo de rótulo. Por exemplo, no caso de um parâmetro baseado em um campo `ProductID` , você pode exibir o campo `ProductName` no rótulo do parâmetro. Quando o relatório é executado, o usuário pode escolher uma opção entre os nomes de produto, mas o valor efetivamente escolhido é o `ProductID`correspondente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Depois de publicar um relatório, você poderá sobrescrever os valores que você definiu no relatório na ferramenta de criação de relatório, configurando os valores de propriedade de parâmetro no servidor de relatórios. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](report-parameters-report-builder-and-report-designer.md).  
  
### <a name="to-add-or-change-the-available-values-for-a-report-parameter"></a>Para adicionar ou alterar os valores disponíveis para um parâmetro de relatório  
  
1.  No painel de dados do relatório, expanda o nó Parâmetros. Clique com o botão direito do mouse no parâmetro e clique em **Propriedades do Parâmetro**. A caixa de diálogo **Propriedades do Parâmetro do Relatório** é aberta.  
  
    > [!NOTE]  
    >  Se o painel Dados do Relatório não estiver visível, clique em **Exibir** e em **Dados do Relatório**.  
  
2.  Clique em **Valores Disponíveis**. Selecione uma opção de valores disponíveis:  
  
    -   Clique em **Especificar valores** para fornecer a lista de valores manualmente e, se desejar, nomes amigáveis (rótulos) para os valores.  
  
         Clique em **Adicionar** , insira o valor na caixa de texto **Valor** e, opcionalmente, o rótulo na caixa de texto **Rótulo** . Se você não fornecer um rótulo, será usado o valor. Você pode gravar uma expressão para um valor. O tipo de dados deve coincidir com o tipo de dados do parâmetro. Os nomes de campo não podem ser usados em uma expressão para um parâmetro. Para obter exemplos, consulte [Filtros geralmente usados &#40;Construtor de Relatórios e SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md).  
  
         Repita esta etapa para todos os valores quantos você deseja fornecer. A ordem dos itens que você vê nesta lista determina a ordem em que o usuário os vê na lista suspensa. Para alterar a ordem de um item da lista, clique em uma caixa de texto **Valor** ou **Rótulo** para selecionar o item desejado e use os botões de seta para cima e para baixo para colocar o item no início ou no final da lista.  
  
    -   Clique em **Obter valores de uma consulta** para fornecer o nome de um conjunto de dados existente que recupera os valores e, opcionalmente, os nomes amigáveis deste parâmetro.  
  
        > [!IMPORTANT]  
        >  Se o mesmo conjunto de dados contiver o parâmetro de consulta correspondente ao parâmetro de relatórios, o relatório exibirá uma mensagem de erro quando tentar executá-lo. Você pode solucionar esse erro usando um conjunto de dados diferente para recuperar os valores.  
  
         Em **Conjunto de dados**, escolha o nome do conjunto de dados.  
  
         No campo **Valor**, escolha o nome do campo que fornece os valores de parâmetro.  
  
         No **campo Rótulo**, escolha o nome do campo que fornece os nomes amigáveis do parâmetro. Se não houver um campo separado para nomes amigáveis, escolha o mesmo campo escolhido para **Valor** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Quando visualiza o relatório, você vê uma lista suspensa dos valores disponíveis para o parâmetro.  
  
### <a name="to-remove-the-available-values-for-a-report-parameter"></a>Para remover os valores disponíveis para um parâmetro de relatório  
  
1.  No painel de dados do relatório, expanda o nó Parâmetros. Clique com o botão direito do mouse no parâmetro e clique em **Propriedades do Parâmetro**. A caixa de diálogo **Parâmetros de Relatório** é exibida.  
  
2.  Clique em **Valores Disponíveis**.  
  
3.  Em **Selecione uma das seguintes opções**, clique em **Nenhuma**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Quando você visualiza o relatório, a lista suspensa dos valores disponíveis para o parâmetro não aparece mais.  
  
## <a name="see-also"></a>Consulte Também  
 [Alterar a ordem de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Adicionar, alterar ou excluir um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Adicionar parâmetros em cascata a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Adicionar, alterar ou excluir valores padrão de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](add-change-or-delete-default-values-for-a-report-parameter.md)   
 [Referências de coleção de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)   
 [Tutorial: Adicionar um parâmetro ao relatório &#40;Construtor de Relatórios&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
