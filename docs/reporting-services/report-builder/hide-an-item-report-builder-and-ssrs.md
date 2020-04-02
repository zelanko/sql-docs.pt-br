---
title: Ocultar um item (Construtor de Relatórios) | Microsoft Docs
description: No Construtor de Relatórios, você pode configurar a visibilidade de um item de relatório. Você pode especificar um parâmetro do relatório ou outra expressão para ocultar um item condicionalmente.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.shared.visibility.f1
- "10503"
ms.assetid: 9d78f8de-959b-456f-8947-687fa6e2ba91
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dab0377e1f558c48be751b523c7129feefb18e66
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80342783"
---
# <a name="hide-an-item-report-builder-and-ssrs"></a>Ocultar um item (Construtor de Relatórios e SSRS)
  Defina a visibilidade de um item de relatório quando quiser ocultar condicionalmente um item com base em um parâmetro de relatório ou alguma outra expressão que você especificar.  
  
 Você também pode desenvolver um relatório para permitir que o usuário alterne a visibilidade dos itens de relatório clicando nas caixas de texto no relatório, por exemplo, em um relatório de busca detalhada. Para obter mais informações, consulte [Adicionar uma ação de expandir/recolher a um item &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md).  
  
 Os procedimentos a seguir descrevem como mostrar ou ocultar um item de relatório em um relatório renderizado com base em uma constante ou expressão.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-a-report-item"></a>Para ocultar um item de relatório  
  
1.  No modo de exibição de Design do relatório, clique com o botão direito do mouse no item de relatório e abra a página **Propriedades** .  
  
    > [!NOTE]  
    >  Para selecionar uma tabela ou uma região de dados tablix inteira, clique na região de dados para selecioná-la, clique com o botão direito do mouse em uma linha, coluna ou alça de canto e, em seguida, clique em **Propriedades do Tablix**.  
  
2.  Clique em **Visibilidade**.  
  
3.  Em **Quando o relatório for executado inicialmente**, especifique se deseja ocultar o item quando exibir o relatório pela primeira vez:  
  
    -   Para exibir o item, clique em **Mostrar**.  
  
    -   Para ocultar o item, clique em **Ocultar**.  
  
    -   Para especificar uma expressão que seja avaliada em tempo de execução, clique em **Mostrar ou ocultar com base em uma expressão**. Digite a expressão ou clique no botão de expressão (**fx**) para criar a expressão na caixa de diálogo **Expressão** .  
  
        > [!NOTE]  
        >  Quando você especifica uma expressão para visibilidade, você está configurando a propriedade Hidden do item de relatório, conforme mostrado na imagem a seguir. A expressão avaliada mostra o item de relatório quando o valor é False e oculta o item de relatório quando o valor é True.   
        > ![Caixa de diálogo Properties_Visibility e propriedade oculta](../../reporting-services/report-builder/media/hiddenproperty-propertiesvisibility.png "Caixa de diálogo Properties_Visibility e propriedade oculta")  
  
4.  Clique duas vezes em **OK** .  
  
### <a name="to-hide-static-rows-in-a-table-matrix-or-list"></a>Para ocultar linhas estáticas em uma tabela, matriz ou lista  
  
1.  Na modo Design do relatório, clique na tabela, matriz ou lista para exibir as alças de coluna e linha.  
  
2.  Clique com o botão direito do mouse na alça da linha e clique em **Visibilidade da Linha**. A caixa de diálogo **Visibilidade da Linha** é aberta.  
  
3.  Para definir a visibilidade, siga as etapas 3 e 4 do primeiro procedimento.  
  
### <a name="to-hide-static-columns-in-a-table-matrix-or-list"></a>Para ocultar colunas estáticas em uma tabela, matriz ou lista  
  
1.  Na exibição Design, selecione a tabela, matriz ou lista para exibir as alças de coluna e linha.  
  
2.  Clique com o botão direito do mouse na alça da coluna e clique em **Visibilidade da Coluna**.  
  
3.  Na caixa de diálogo **Visibilidade da Coluna** , siga as etapas 3 e 4 do primeiro procedimento.  
  
## <a name="see-also"></a>Consulte Também  
 [Ação de análise detalhada &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [Adicionar uma ação de expandir/recolher a um item &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
