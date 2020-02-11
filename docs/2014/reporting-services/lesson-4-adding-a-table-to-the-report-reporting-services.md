---
title: 'Lição 4: Adicionando uma tabela ao relatório (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3bb152b749041451cdb3a3294c24d8b172c49a99
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108447"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>Lição 4: Adicionando uma tabela ao relatório (Reporting Services)
  Depois de definir o conjunto de dados, você pode começar a criar o relatório. Um layout de relatório é criado arrastando e soltando regiões de dados, caixas de texto, imagens e outros itens que você deseja incluir no relatório na superfície de design.  
  
 Itens que contêm linhas de dados repetidas de conjuntos de dados subjacentes são chamados de *regiões de dados*. Um relatório básico terá apenas uma região de dados, mas é possível adicionar mais, por exemplo, se você desejar adicionar um gráfico ao relatório tabular. Depois de adicionar uma região de dados, você pode adicionar campos à região de dados.  
  
### <a name="to-add-a-table-data-region-and-fields-to-a-report-layout"></a>Para adicionar uma região de dados de Tabela e campos ao layout de um relatório  
  
1.  Na **Caixa de Ferramentas**, clique em **Tabela**, clique na superfície de design e arraste o mouse. O Designer de Relatórios desenha uma região de dados de tabela com três colunas no centro da superfície de design.  
  
    > [!NOTE]  
    >  A **Caixa de Ferramentas** pode aparecer como uma guia no lado esquerdo do painel **Dados do Relatório** . Para abrir a **caixa de ferramentas**, mova o ponteiro sobre a guia **caixa de ferramentas** . Se a **caixa de ferramentas** não estiver visível, no menu **Exibir** , clique em **caixa de ferramentas**.  
  
2.  No painel **data do relatório** , expanda o conjunto de dados **AdventureWorksDataSet** para exibir os campos.  
  
3.  Arraste o campo Data do painel **Dados do Relatório** até a primeira coluna da tabela.  
  
     Quando você solta o campo na primeira coluna, duas coisas acontecem. Primeiro, a célula de dados exibirá o nome do campo, conhecido como a *expressão de campo*, em colchetes: `[Date]`. Em seguida, um valor de cabeçalho de coluna é adicionado automaticamente à linha Cabeçalho, exatamente acima da expressão de campo. Por padrão, a coluna é o nome do campo. Você pode selecionar o texto da linha Cabeçalho e digitar um novo nome.  
  
4.  Arraste o campo Ordem do painel **Dados do Relatório** até a segunda coluna da tabela.  
  
5.  Arraste o campo Produto do painel **Dados do Relatório** até a terceira coluna da tabela.  
  
6.  Arraste o campo Quantidade para a margem direita da terceira coluna até obter um cursor vertical e o ponteiro do mouse se tornar um sinal de mais [+]. Quando você liberar o botão do mouse, uma quarta coluna será criada para `[Qty]`.  
  
7.  Adicione o campo LineTotal da mesma maneira criando uma quinta coluna.  
  
    > [!NOTE]  
    >  O cabeçalho de coluna é Total de Linha. O Designer de Relatórios cria automaticamente um nome amigável para a coluna dividindo LineTotal em duas palavras.  
  
     O diagrama a seguir mostra uma região de dados de tabela que foi populada com estes campos: Data, Ordem, Produto, Quantidade e Total da Linha.  
  
     ![Design, Tabela com linha de cabeçalho e linha de detalhes](../../2014/tutorials/media/rs-basictabledetailsdesign.gif "Design, Tabela com linha de cabeçalho e linha de detalhes")  
  
## <a name="preview-your-report"></a>Visualize o relatório  
 A visualização de um relatório permite exibir o relatório renderizado sem que seja necessário publicá-lo primeiro em um servidor de relatório. Provavelmente, você desejará visualizar o relatório com frequência durante o tempo de design. Visualizar o relatório também executará a validação nas conexões de design e de dados, para que você possa corrigir erros e problemas antes de publicar o relatório em um servidor de relatório.  
  
#### <a name="to-preview-a-report"></a>Para visualizar um relatório  
  
-   Clique na guia **Visualizar** . Report Designer executa o relatório e o exibe no modo de exibição de visualização.  
  
     O diagrama a seguir mostra parte do relatório na exibição Visualização.  
  
     ![Visualização, Linhas de detalhes da tabela com 5 colunas](../../2014/tutorials/media/rs-basictabledetailspreview.gif "Visualização, Linhas de detalhes da tabela com 5 colunas")  
  
     Observe que a moeda (na coluna Total da Linha) tem seis casas decimais e a data inclui um carimbo de data/hora. Você vai corrigir essa formatação na próxima lição.  
  
> [!NOTE]  
>  No menu **Arquivo** , clique em **Salvar Tudo** para salvar o relatório.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você adicionou uma região de dados de Tabela ao relatório, adicionou campos à região de dados e visualizou o relatório com êxito. Em seguida, você formatará cabeçalhos de colunas e valores de data e de moeda. Consulte [Lição 5: Formatando um relatório &#40;Reporting Services&#41;](../reporting-services/lesson-5-formatting-a-report-reporting-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)   
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
