---
title: 'Lição 4: Adicionando uma tabela ao relatório (Reporting Services) | Microsoft Docs'
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e925dec5eb14365a6c313349599a77ffe1d7ab13
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106014"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>Lição 4: Adicionando uma tabela ao relatório (Reporting Services)

Depois de definir o conjunto de dados, você pode começar a criar o relatório. Crie um layout de relatório arrastando e soltando *objetos de relatório* do painel **Caixa de Ferramentas** para a **Área de design**. Alguns dos tipos de objetos de relatório incluem:

- Table
- Caixa de texto
- image
- Linha
- Retângulo
- Gráfico
- Mapeamento

Itens que contêm linhas de dados repetidas de conjuntos de dados subjacentes são chamados de *regiões de dados*. Depois de adicionar uma região de dados, você pode adicionar campos à região de dados. Um relatório básico terá apenas uma região de dados. Você pode incluir outras adicionais para exibir mais informações, como um gráfico.

## <a name="add-a-table-data-region-and-fields-to-a-report-layout"></a>Adicionar campos e região de dados de tabela ao layout de um relatório

1. Selecione a guia **Caixa de Ferramentas** no painel esquerdo do Designer de Relatórios. Com o mouse, selecione o objeto **Tabela** e arraste-o para a superfície de design do relatório. O Designer de Relatórios desenha uma região de dados de tabela com três colunas no centro da superfície de design. Se você não vir a guia **Caixa de Ferramentas**, selecione o menu **Exibição** > **Caixa de Ferramentas**.

    ![ssrs_ssdt_addtable](media/ssrs-ssdt-addtable.png)

    Você também pode adicionar uma tabela ao relatório por meio da superfície de design. Clique com o botão direito do mouse na área de design e, em seguida, selecione **Inserir** > **Tabela**.

2. No painel **Dados do Relatório**, expanda o conjunto de dados AdventureWorksDataset para exibir os campos.

3. Arraste o campo `[Date]` no painel **Dados do Relatório** para a primeira coluna da tabela.

    > [!IMPORTANT]
    > Quando você solta o campo na primeira coluna, duas coisas acontecem. Primeiro, o Designer de Relatórios exibe o nome do campo, chamado de *expressão de campo*, em colchetes: `[Date]` na célula de dados. Depois ele adiciona um rótulo de coluna na linha do cabeçalho, logo acima da expressão de campo. Por padrão, o rótulo da coluna é o nome do campo. Você pode selecionar o rótulo e o tipo da coluna e digitar um novo valor se quiser alterá-lo.

4. Arraste o campo `[Order]` do painel **Dados do Relatório** para a segunda coluna da tabela.

5. Arraste o campo `[Product]` do painel **Dados do Relatório** para a terceira coluna da tabela.

6. Arraste o campo `[Qty]` para a borda direita da terceira coluna até obter um cursor vertical e o ponteiro do mouse apresentar um sinal de mais [+]. Quando você liberar o botão do mouse, uma quarta coluna será criada para a expressão de campo `[Qty]`.

    ![ssrs_tutorial_addcolumn](media/ssrs-tutorial-addcolumn.png)

7. Adicione o campo `[LineTotal]` da mesma maneira para criar uma quinta coluna. O rótulo da coluna é adicionado como "Total de Linha". O Designer de Relatórios cria automaticamente um nome amigável para a coluna ao dividir o "Total da Linha" em duas palavras.

O diagrama a seguir mostra uma região de dados de tabela que foi populada com estes campos: Data, Ordem, Produto, Quantidade e Total da Linha.
![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

## <a name="preview-your-report"></a>Visualizar o relatório

A visualização de um relatório permite exibir o relatório renderizado sem que seja necessário publicá-lo primeiro em um servidor de relatório. Visualize o relatório com frequência ao criá-lo. Ao fazer isso, você valida as conexões de dados e o design, permitindo corrigir os erros e problemas conforme você avança.

### <a name="to-preview-a-report"></a>Para visualizar um relatório

- Clique na guia **Visualização**. O Designer de Relatórios executa o relatório e o exibe na exibição **Visualização**.

    ![ssrs_ssdt_preview](media/ssrs-ssdt-preview.png)

O diagrama a seguir mostra parte do relatório na exibição **Visualização**.

   ![Visualização, linhas de detalhes da tabela com cinco colunas](media/rs-basictabledetailspreview.png "Visualização, linhas de detalhes da tabela com cinco colunas")

Examine os valores de Data e a Total da Linha. Na próxima lição, você aprenderá como formatá-los para uma exibição mais organizada.

> [!NOTE]
> No menu **Arquivo**, selecione **Salvar Tudo** para salvar o relatório.

## <a name="next-steps"></a>Próximas etapas

Você adicionou uma região de dados de tabela ao relatório, adicionou campos à região de dados e visualizou o relatório com êxito. Na próxima lição, você aprenderá como formatar os cabeçalhos de colunas e expressões de campo. Continue a seguir na [Lição 5: Formatando um relatório &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md).
  
## <a name="see-also"></a>Confira também

[Tabelas &#40;Construtor de Relatórios e SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)  
[Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
