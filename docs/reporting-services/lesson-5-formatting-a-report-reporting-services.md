---
title: 'Lição 5: Formatando um relatório (Reporting Services) | Microsoft Docs'
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a8bf8b6814f7989a904507cd89fbea397b8b6930
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105934"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>Lição 5: Formatando um relatório (Reporting Services)

Agora que já adicionou uma região de dados e alguns campos ao relatório de ordens de venda, você pode formatar os campos de data e moeda, além dos cabeçalhos da coluna.

## <a name="bkmk_format_date"></a>Formatar a data

Por padrão, a expressão Data exibe informações de data e hora. É possível formatá-lo para exibir apenas a data.

1. Selecione a guia **Design**.
2. Clique com o botão direito do mouse na célula com a expressão de campo `[Date]` e selecione **Propriedades da Caixa de Texto**.
3. Selecione o **Número** e, no campo **Categoria**, selecione a **Data**.
4. Na caixa **Tipo** , selecione **31 de janeiro de 2000**.
5. Selecione **OK** para aplicar o formato.
6. Visualize o relatório para ver a alteração na formatação do campo `[Date]` e, em seguida, retorne para a exibição de design.

## <a name="bkmk_format_currency"></a>Formatar a moeda

O campo Total da Linha exibe um número geral. É possível formatá-lo para exibir o número como moeda.

1. Clique com o botão direito do mouse na célula com a expressão `[LineTotal]` e selecione **Propriedades da Caixa de Texto**.
2. Selecione **Número**, na caixa de listagem da coluna à extrema esquerda, e **Moeda** na caixa de listagem **Categoria**.
3. Caso a configuração regional esteja em português (Brasil), os padrões na caixa de listagem **Tipo** devem ser:
    - **Casas decimais: 2**
    - **Números negativos: (R$ 1.2345,00)**
    - **Símbolo: R$ português (Brasil)**
4. Selecione **Usar separador de milhar (.)**. Caso o texto de exemplo seja **R$ 12.345,00**, as configurações estão corretas.
5. Selecione **OK** para aplicar o formato.
6. Visualize o relatório para ver a alteração na coluna da expressão `[LineTotal]` e depois retorne para a exibição de design.  

## <a name="bkmk_change_textstyle"></a>Alterar estilo do texto e larguras da coluna

Você pode adicionar outra formatação ao relatório, realce a linha de cabeçalho e ajuste as larguras das colunas de dados.

### <a name="to-format-header-rows-and-table-columns"></a>Para formatar as linhas do cabeçalho e as colunas da tabela

1. Selecione a tabela de forma que os identificadores de coluna e linha sejam exibidos acima e ao lado da tabela. As barras em cinza ao longo da parte superior e ao lado da tabela são os identificadores de coluna e de linha.

2. Aponte para a linha entre os identificadores de coluna para que o cursor seja alterado para uma seta dupla. Arraste as colunas de acordo com o tamanho desejado.
    ![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

3. Selecione a linha que contém rótulos de cabeçalho de coluna e, no menu **Formatar**, selecione **Fonte** > **Negrito**.

4. Visualize o relatório. Deve estar como mostrado a seguir:

    ![Visualização de tabela com cabeçalhos de coluna em negrito](media/rs-basictabledetailsformattedpreview.png "Visualização de tabela com cabeçalhos de coluna em negrito")  

5. No menu **Arquivo**, selecione **Salvar Tudo** para salvar o relatório.

## <a name="next-steps"></a>Próximas etapas

Nesta lição, você formatou com êxito os cabeçalhos de coluna e as expressões de campo. Agora você adicionará os agrupamentos e totais ao relatório. Continue na [Lição 6: Adicionando agrupamentos e totais &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md).

## <a name="see-also"></a>Confira também

[Formatando números e datas &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)
[Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](report-design/rendering-behaviors-report-builder-and-ssrs.md)
