---
title: Adicionar um indicador a um relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: f130562e-5673-40e3-8e01-de7227a21d41
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 73268c03ef80b13a28d8011f9b6860abcfac79e2
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50030365"
---
# <a name="add-a-bookmark-to-a-report-report-builder-and-ssrs"></a>Adicionar um indicador a um relatório (Construtor de Relatórios e SSRS)
  Adicione indicadores e links de indicadores a um relatório quando quiser fornecer um sumário personalizado ou links de navegação internos personalizados no relatório. Geralmente, os indicadores são adicionados aos relatórios para conduzir os usuários aos locais para os quais deseja direcioná-los, como tabelas, gráficos ou os valores de grupo exclusivos exibidos em uma tabela ou matriz. Você pode criar suas próprias cadeias de caracteres para usar como indicadores, ou, em grupos, pode definir o indicador para uma expressão de grupo.  
  
 Depois de criar os indicadores, é possível adicionar os itens de relatórios em que o usuário pode clicar para ir ser conduzido a cada um dos indicadores. Geralmente, esses itens são caixas de texto ou imagens.  
  
 Por exemplo, se o seu relatório exibe uma tabela agrupada por cor, você poderia adicionar um indicador ao cabeçalho do grupo com base na expressão do grupo. Em seguida, você poderia adicionar uma tabela com uma caixa de texto simples no começo do relatório que exibiu os valores de cor e definir o link de indicador nessa caixa de texto. Ao clicar na cor, o relatório é direcionado para a página que exibe a linha de cabeçalho do grupo daquela cor.  
  
 O indicador pode ser adicionado a qualquer item do relatório e o link de indicador pode ser adicionado a qualquer item que tenha uma propriedade **Ação** , como uma caixa de texto, uma imagem ou uma séria calculada em um gráfico. Para obter mais informações, consulte [Caixa de diálogo Propriedades da Ação &#40;Construtor de Relatórios e SSRS&#41;](https://msdn.microsoft.com/library/2c5d915b-4f97-42cf-b8f1-49ca3ff3d0f9).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-bookmark"></a>Para adicionar um indicador  
  
1.  Na exibição de design de relatório, selecione a caixa de texto, imagem, gráfico ou outro item de relatório ao qual você deseja adicionar um indicador. As propriedades do item selecionado aparecem no painel Propriedades.  
  
2.  Na caixa de texto ao lado de **Indicador**, digite uma cadeia de caracteres que sirva como rótulo para esse indicador. Por exemplo, você pode digitar **BikePhoto** como o indicador de uma imagem em seu relatório. Se preferir, clique no botão Expressão (**fx**) para abrir a caixa de diálogo **Expressão** para especificar uma expressão que seja avaliada como um rótulo. Em um grupo, a expressão que você digitar deve estar na expressão de grupo.  
  
    > [!NOTE]  
    >  O indicador pode ser qualquer cadeia de caracteres, mas ele deve ser exclusivo no relatório. Caso ele não seja exclusivo, o link para o indicador em questão localizará apenas a primeiro indicador correspondente.  
  
### <a name="to-add-a-bookmark-link"></a>Para adicionar um link de indicador  
  
1.  No modo de exibição de Design, clique com o botão direito do mouse na caixa de texto, na imagem ou no gráfico ao qual você deseja adicionar um link e, em seguida, clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades** desse item de relatório, clique em **Ação**.  
  
3.  Selecione **Ir para indicador**. Aparecerá uma seção adicional na caixa de diálogo para essa opção.  
  
4.  Na caixa **Selecionar indicador** , digite ou selecione um indicador ou uma expressão que seja avaliada como um indicador. Usando o exemplo anterior, digite **BikePhoto** para criar um link para a imagem em seu relatório.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (Opcional) O texto não é formatado automaticamente como um link. Para textos, é recomendável alterar sua cor e seu efeito para indicar que ele é um link. Por exemplo, altere a cor para azul e o efeito para sublinhado na seção **Fonte** da guia Página Inicial da Faixa de Opções.  
  
7.  Para testar o link, clique em **Executar** para visualizar o relatório e, em seguida, no item de relatório no qual você definiu esse link.  
  
## <a name="see-also"></a>Consulte Também  
 [Classificação interativa, mapas de documentos e links &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
