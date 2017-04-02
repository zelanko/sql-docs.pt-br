---
title: "Adicionar uma a&#231;&#227;o de detalhamento a um relat&#243;rio (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 153729c4-d01e-4629-b78f-0cfd5a7f83da
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 9
---
# Adicionar uma a&#231;&#227;o de detalhamento a um relat&#243;rio (Construtor de Relat&#243;rios e SSRS)
  O relatório aberto quando você clica no link no relatório principal é conhecido como um *relatório detalhado*. Este link de detalhamento habilita uma ação de detalhamento.  
  
 Os relatórios detalhados devem ser publicados no mesmo servidor de relatório do relatório principal, mas podem estar em pastas diferentes. Você pode adicionar um link de detalhamento a qualquer item que tenha uma propriedade **Ação** , por exemplo, uma caixa de texto, uma imagem ou pontos de dados de um gráfico.  
  
 Para adicionar um link de detalhamento a um relatório, você deve primeiro criar o relatório detalhado a que o relatório principal será vinculado. Um relatório detalhado contém detalhes comuns sobre um item contido no relatório resumido original e normalmente contém parâmetros que filtram o relatório detalhado com base em parâmetros passados a ele do relatório principal. Para obter mais informações sobre como criar o relatório de detalhamento, consulte [Relatórios de detalhamento &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/drillthrough-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para adicionar uma ação de detalhamento  
  
1.  No modo de exibição de Design, clique com o botão direito do mouse na caixa de texto, na imagem ou no gráfico ao qual você quer adicionar um link e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades** do item, clique em **Ação**.  
  
3.  Selecione **Ir para relatório**. Serão exibidas seções adicionais na caixa de diálogo para essa opção.  
  
4.  Em **Especificar um relatório**, clique em **Procurar** para localizar o relatório desejado ou digite o nome do relatório. Como alternativa, clique no botão da expressão (**fx**) para criar uma expressão para o nome de relatório.  
  
     O formato do caminho para o relatório detalhado é diferente para os modos nativo e integrado do SharePoint. Se você procurar um relatório, um caminho no formato correto será fornecido. Para obter mais informações, consulte [Especificando caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
     Caso seja preciso especificar os parâmetros para o relatório detalhado, siga esta etapa.  
  
5.  Em **Use estes parâmetros para executar o relatório**, clique em **Adicionar**. Uma linha nova é adicionada à grade de parâmetros.  
  
    -   Na caixa de texto **Nome**, clique na lista suspensa ou digite o nome do parâmetro de relatório no relatório de detalhamento.  
  
        > [!NOTE]  
        >  Os nomes na lista de parâmetros devem corresponder exatamente aos parâmetros esperados no relatório de destino. Por exemplo, nomes de parâmetro devem ter maiúsculas e minúsculas correspondentes. Caso não correspondam ou se algum parâmetro esperado não for listado, haverá falha no relatório detalhado.  
  
    -   Em **Valor**, digite ou selecione o valor para passar para o parâmetro no relatório detalhado.  
  
        > [!NOTE]  
        >  Os valores podem conter uma expressão que seja avaliada como um valor para ser passado para o parâmetro de relatório. As expressões na lista de valores incluem a lista de campos para o relatório atual.  
  
     Para obter informações sobre como ocultar parâmetros em relatórios, consulte [Adicionar, alterar ou excluir um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md).  
  
6.  (Opcional) Para caixas de texto, é útil indicar ao usuário que o texto é um link, alterando a cor e o efeito do texto na guia **Início** da Faixa de Opções.  
  
7.  Para testar o link, execute o relatório e clique no item de relatório definido com o link.  
  
## Consulte também  
 [Caixa de diálogo Propriedades de Ação &#40;Construtor de Relatórios e SSRS&#41;](../Topic/Action%20Properties%20Dialog%20Box%20\(Report%20Builder%20and%20SSRS\).md)   
 [Formatando pontos de dados em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Mostrar dicas de ferramenta em uma série &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
  