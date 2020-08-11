---
title: Personalizar o painel de parâmetros em um relatório (Construtor de Relatórios) | Microsoft Docs
description: Saiba como personalizar o painel Parâmetros durante a criação de relatórios paginados com parâmetros no Construtor de Relatórios.
ms.date: 06/15/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4ce9e8d5-911a-4422-928f-a8d005b79fc6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 29bd397d64280644394077a29a3420dbf43b5e6f
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796557"
---
# <a name="customize-the-parameters-pane-in-a-report-report-builder"></a>Personalizar o painel de parâmetros em um relatório (Construtor de Relatórios)
  Ao criar relatórios paginados com parâmetros no Construtor de Relatórios, você pode personalizar o painel Parâmetros. No modo de exibição de Design de relatório, você pode arrastar um parâmetro para uma coluna e linha específicas no painel Parâmetros. Você pode adicionar e remover colunas para alterar o layout do painel.

 Quando você arrasta um parâmetro para uma nova coluna e linha no painel, a ordem do parâmetro é alterada no painel **Dados do Relatório** . Quando você altera a ordem do parâmetro no painel de **Dados do Relatório** , o local do parâmetro no painel é alterado. Para obter mais informações sobre por que a ordem do parâmetro é importante, consulte [Alterar a ordem de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md).

## <a name="to-customize-the-parameters-pane"></a>Para personalizar o painel de parâmetros

1.  Na guia **Exibição** , marque a caixa de seleção **Parâmetros** para exibir o painel de parâmetros.

     ![Acessar painel de parâmetros na guia Exibir](../../reporting-services/report-design/media/ssrs-customparameter-accessparameterpanedesignmode.png "Acessar painel de parâmetros na guia Exibir")

     O painel aparece na parte superior da superfície de design.

2.  Para adicionar um parâmetro ao painel, siga um destes procedimentos.

    -   Clique com o botão direito do mouse em uma célula vazia no painel de parâmetros e clique em **Adicionar Parâmetro**.

         ![Adicionar novo parâmetro no painel de parâmetros](../../reporting-services/report-design/media/ssrs-customizeparameter-addnewparameter.png "Adicionar novo parâmetro no painel de parâmetros")

    -   Clique com o botão direito do mouse em **Parâmetros** no painel de **Dados do Relatório** e, depois, clique em **Adicionar Parâmetro**.

3.  Para mover um parâmetro para um novo local no painel de parâmetros, arraste o parâmetro para uma célula diferente no painel.

     Quando você altera o local do parâmetro no painel, a ordem do parâmetro na lista **Parâmetros** no painel de **Dados do Relatório** é altera automaticamente. Para obter mais informações sobre o impacto da ordem do parâmetro, consulte [Alterar a ordem de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)

4.  Para acessar as propriedades para um parâmetro, siga um dos procedimentos a seguir.

    -   No painel de parâmetros, clique com o botão direito do mouse no parâmetro e depois clique em **Propriedades do Parâmetro**.

         ![Acessar propriedades de parâmetro no painel de parâmetros](../../reporting-services/report-design/media/ssrs-customizeparameter-accessparameterproperties-composite.png "Acessar propriedades de parâmetro no painel de parâmetros")

    -   No painel de **Dados do Relatório** , clique com o botão direito do mouse no parâmetro e depois clique em **Propriedades do Parâmetro**.

5.  Para adicionar novas colunas e linhas ao painel ou para excluir colunas e linhas existentes, clique com o botão direito do mouse em qualquer lugar no painel de parâmetros e, em seguida, clique em um comando no menu exibido.

     ![Adicionar colunas e linhas ao painel de parâmetros](../../reporting-services/report-design/media/ssrs-customparameter-addcolumnsrows.png "Adicionar colunas e linhas ao painel de parâmetros")

    > [!IMPORTANT]
    >  Quando você exclui uma coluna ou linha que contém parâmetros, eles são excluídos do relatório.

6.  Para excluir um parâmetro do painel e do relatório, siga um dos procedimentos a seguir.

    -   No painel de parâmetros, clique com o botão direito do mouse no parâmetro e depois clique em  **Excluir**.

         ![Excluir parâmetros do painel de parâmetros](../../reporting-services/report-design/media/ssrs-customparameter-deleteparameter.png "Excluir parâmetros do painel de parâmetros")

    -   No painel de **Dados do Relatório** , clique com o botão direito do mouse no parâmetro e depois clique em **Excluir**.

## <a name="hiddeninternal-parameters-during-runtime"></a>Parâmetros ocultos/internos durante o runtime
Se você tiver um parâmetro oculto/interno, a lógica de se ele será renderizado como espaço vazio durante o runtime será a seguinte:

   - Se qualquer linha ou coluna contiver apenas parâmetros ocultos/internos ou células vazias, a linha ou coluna inteira não será renderizada durante o runtime
   - Caso contrário, o parâmetro oculto/interno ou a célula vazia será renderizado como espaço vazio

Por exemplo, `ReportParameter1` está oculto enquanto o restante dos parâmetros está visível:

![Exemplo 1 de Parâmetro Oculto](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-1.png "Um parâmetro oculto na grade de layout")

Isso resultará em um espaço vazio durante o runtime porque há parâmetros visíveis na primeira coluna ou primeira linha:

![Exemplo 1 de Parâmetro Oculto – runtime](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-1.png "Um parâmetro oculto na grade de layout resulta em espaço vazio no runtime")

Usando o mesmo exemplo, se você também definir `ReportParameter3` como oculto:

![Exemplo 2 de Parâmetro Oculto](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-2.png "Dois parâmetros ocultos na mesma coluna")

Em seguida, a primeira coluna não é renderizada durante o runtime porque a coluna inteira é considerada vazia:

![Exemplo 2 de Parâmetro Oculto – runtime](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-2.png "Dois parâmetros ocultos na mesma coluna no runtime")

## <a name="default-layout"></a>Definir layout
Para relatórios que foram criados antes do SQL Server Reporting Services 2016, uma grade de layout de parâmetro padrão de 2 colunas e N linhas será usada durante o runtime. Para alterar o layout padrão, abra o relatório no Construtor de Relatórios da Microsoft e salve o relatório. Depois de salvar o relatório, as informações de layout do parâmetro personalizado serão salvas no arquivo. rdl.


## <a name="see-also"></a>Confira também
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)


