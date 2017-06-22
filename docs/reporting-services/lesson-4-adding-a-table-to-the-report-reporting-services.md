---
title: "Lição 4: Adicionando uma tabela ao relatório (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
caps.latest.revision: 64
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 76224139b629d797735b88bfcc692a1e8abce336
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>Lição 4: Adicionando uma tabela ao relatório (Reporting Services)
Depois de definir o conjunto de dados, você pode começar a criar o relatório. Um layout de relatório é criado arrastando e soltando regiões de dados, caixas de texto, imagens e outros itens que você deseja incluir no relatório na superfície de design.  
  
Itens que contêm linhas de dados repetidas de conjuntos de dados subjacentes são chamados de *regiões de dados*. Um relatório básico terá apenas uma região de dados, mas é possível adicionar mais, por exemplo, se você desejar adicionar um gráfico ao relatório tabular. Depois de adicionar uma região de dados, você pode adicionar campos à região de dados.  
  
### <a name="to-add-a-table-data-region-and-fields-to-a-report-layout"></a>Para adicionar uma região de dados de Tabela e campos ao layout de um relatório  
  
1.  Na **Caixa de Ferramentas**, clique em **Tabela**, clique na superfície de design e arraste o mouse. O Designer de Relatórios desenha uma região de dados de tabela com três colunas no centro da superfície de design. A **Caixa de Ferramentas** pode aparecer como uma guia no lado esquerdo do painel **Dados do Relatório** . Para abrir a **Caixa de Ferramentas**, mova o ponteiro sobre a guia **Caixa de Ferramentas** . Se a **Caixa de Ferramentas** não estiver visível, no menu **Exibir** , clique em **Caixa de Ferramentas**.
  
     ![ssrs_ssdt_addtable](../reporting-services/media/ssrs-ssdt-addtable.png) 
  
  Você também pode adicionar uma tabela ao relatório por meio da superfície de design.  Clique com o botão direito do mouse na superfície de design, clique em **Inserir** e em **Tabela**.
2.  No painel **Dados do Relatório** , expanda o conjunto de dados **AdventureWorksDataset** para exibir os campos.  
  
3.  Arraste o campo *Data* do painel **Dados do Relatório** até a primeira coluna da tabela.  
  
    Quando você solta o campo na primeira coluna, duas coisas acontecem. Primeiro, a célula de dados exibirá o nome do campo, conhecido como a *expressão de campo*, em colchetes: `[Date]`. Em seguida, um valor de cabeçalho de coluna é adicionado automaticamente à linha Cabeçalho, exatamente acima da expressão de campo. Por padrão, a coluna é o nome do campo. Você pode selecionar o texto da linha Cabeçalho e digitar um novo nome.  
  
4.  Arraste o campo *Ordem* do painel **Dados do Relatório** até a segunda coluna da tabela.  
  
5.  Arraste o campo *Produto* do painel **Dados do Relatório** até a terceira coluna da tabela.  
  
6.  Arraste o campo Quantidade para a margem direita da terceira coluna até obter um cursor vertical e o ponteiro do mouse se tornar um sinal de mais [+]. Quando você liberar o botão do mouse, uma quarta coluna será criada para `[Qty]`.  
![ssrs_tutorial_addcolumn](../reporting-services/media/ssrs-tutorial-addcolumn.png)  
  
7.  Adicione o campo LineTotal da mesma maneira criando uma quinta coluna. O cabeçalho de coluna é Total de Linha. O Designer de Relatórios cria automaticamente um nome amigável para a coluna dividindo LineTotal em duas palavras.  
  
  
O diagrama a seguir mostra uma região de dados de tabela que foi populada com estes campos: Data, Ordem, Produto, Quantidade e Total da Linha.  
![rs_BasicTableDetailsDesign](../reporting-services/media/rs-basictabledetailsdesign.png)  
  
## <a name="preview-your-report"></a>Visualize o relatório  
A visualização de um relatório permite exibir o relatório renderizado sem que seja necessário publicá-lo primeiro em um servidor de relatório. Provavelmente, você desejará visualizar o relatório com frequência durante o tempo de design. Visualizar o relatório também executará a validação nas conexões de design e de dados, para que você possa corrigir erros e problemas antes de publicar o relatório em um servidor de relatório.  
  
#### <a name="to-preview-a-report"></a>Para visualizar um relatório  
  
-   Clique na guia **Visualização** . O Designer de Relatórios executa o relatório e exibe-o na exibição Visualização.
![ssrs_ssdt_preview](../reporting-services/media/ssrs-ssdt-preview.png)  
  
    O diagrama a seguir mostra parte do relatório na exibição Visualização.  
  
    ![Visualização, linhas de detalhes de tabela com 5 colunas](../reporting-services/media/rs-basictabledetailspreview.png "visualização, linhas de detalhes de tabela com 5 colunas")  
  
    Observe que a moeda (na coluna Total da Linha) tem seis casas decimais e a data inclui um carimbo de data/hora. Você vai corrigir essa formatação na próxima lição.  
  
> [!NOTE]  
> No menu **Arquivo** , clique em **Salvar Tudo** para salvar o relatório.  
  
## <a name="next-steps"></a>Próximas etapas  
Você adicionou uma região de dados de Tabela ao relatório, adicionou campos à região de dados e visualizou o relatório com êxito. Em seguida, você formatará cabeçalhos de colunas e valores de data e de moeda. Consulte [Lição 5: Formatando um relatório &#40;Reporting Services&#41;](../reporting-services/lesson-5-formatting-a-report-reporting-services.md).  
  
## <a name="see-also"></a>Consulte também  
[Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  

