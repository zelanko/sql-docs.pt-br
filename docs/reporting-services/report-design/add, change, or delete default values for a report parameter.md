---
title: "Adicionar, alterar ou excluir valores padr&#227;o de um par&#226;metro de relat&#243;rio (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "10460"
  - "sql13.rtp.rptdesigner.reportparameters.defaultvalues.f1"
  - "10072"
ms.assetid: 6a87e069-b3a9-47b6-bcec-afcdd8aff65f
caps.latest.revision: 11
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Adicionar, alterar ou excluir valores padr&#227;o de um par&#226;metro de relat&#243;rio (Construtor de Relat&#243;rios e SSRS)
  Depois de criar um parâmetro de relatório, você poderá fornecer uma lista de valores padrão. Se todos os parâmetros tiverem um valor padrão válido, o relatório será executado automaticamente na primeira vez em que ele for exibido ou visualizado.  
  
 Os parâmetros de relatório podem representar um valor ou diversos valores. Para valores únicos, é possível fornecer um literal ou expressão. Para vários valores, é possível fornecer uma lista estática ou uma lista de um conjunto de dados de relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Depois de publicar um relatório, você poderá sobrescrever os valores padrão que você definiu no relatório na ferramenta de criação de relatório, configurando os valores de propriedade de parâmetro no servidor de relatórios. Você também pode fornecer vários conjuntos de valores de parâmetros padrão criando relatórios vinculados. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
### Para adicionar ou alterar valores padrão de um parâmetro de relatório  
  
1.  No painel de dados do relatório, expanda o nó **Parâmetros** . Clique com o botão direito do mouse no parâmetro e escolha **Editar**. A caixa de diálogo **Propriedades do Parâmetro do Relatório** é aberta.  
  
    > [!NOTE]  
    >  Se o painel Dados do Relatório não estiver visível, clique em **Exibir** e em **Dados do Relatório**.  
  
2.  Clique em **Valores Padrão**.  
  
3.  Selecione uma opção padrão:  
  
    -   Para fornecer manualmente um valor ou uma lista de valores, clique em **Especificar valores**. Clique em **Adicionar** e na caixa de texto **Valor** , digite um valor. Você pode gravar uma expressão para um valor. O tipo de dados deve coincidir com o tipo de dados do parâmetro. Os nomes de campo não podem ser usados em uma expressão para um parâmetro.  
  
         Para parâmetros de vários valores, repita esta etapa para todos os valores que deseja fornecer. A ordem dos itens que você vê nesta lista determina a ordem em que o usuário os vê na lista suspensa. Para alterar a ordem de um item na lista, clique na caixa de texto **Valor** para selecionar o item desejado e use os botões de seta para cima e para baixo para movê-lo para cima ou para baixo na lista.  
  
    -   Para fornecer o nome de um conjunto de dados existente que recupera os valores, clique em **Obter valores de uma consulta**. Em **Conjunto de dados**, escolha o nome do conjunto de dados.  
  
         No campo **Valor**, escolha o nome do campo que fornece os valores de parâmetro.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### Para remover ou alterar valores padrão de um parâmetro de relatório  
  
1.  No painel de dados do relatório, expanda o nó **Parâmetros** . Clique com o botão direito do mouse no parâmetro e escolha **Editar**. A caixa de diálogo **Propriedades do Parâmetro do Relatório** é aberta.  
  
2.  Clique em **Valores Padrão**.  
  
3.  Em **Selecione uma das seguintes opções**, clique em **Nenhum valor padrão**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Consulte também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Adicionar parâmetros em cascata a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um parâmetro ao relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add dataset filters, data region filters, and group filters.md)   
 [Referências de coleções de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/parameters-collection-references-report-builder-and-ssrs.md)   
 [Alterar a ordem de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Adicionar, alterar ou excluir um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  