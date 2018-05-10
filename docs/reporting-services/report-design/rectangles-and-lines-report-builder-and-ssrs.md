---
title: Retângulos e linhas (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d6226b0c-0398-4185-8565-96099876fc21
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 05fb8fc7b21ce2274c113582f7bf3f1cb1c61e4a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="rectangles-and-lines-report-builder-and-ssrs"></a>Retângulos e linhas (Construtor de Relatórios e SSRS)
  Os retângulos e as linhas podem criar efeitos visuais em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . É possível definir propriedades de exibição nesses itens de relatório na seção Borda da guia Página inicial e definir outras propriedades usando o painel Propriedades. É possível adicionar recursos como uma cor ou imagem de plano de fundo, uma dica de ferramenta ou um indicador a um retângulo.  
  
##  <a name="RectanglesLinesReportParts"></a> Retângulos e linhas como partes de relatório  
 Você pode publicar retângulos com os itens que eles contêm separadamente do relatório como partes do relatório. Partes de relatório são itens de relatório autossuficientes que são armazenados no servidor de relatório e podem ser incluídos em outros relatórios.  
  
 Não é possível publicar os itens de relatório dentro do retângulo como partes de relatório. Quando as pessoas adicionam o retângulo a um relatório, adicionam também os itens que ele contém.  Leia mais sobre as [Partes do relatório](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
##  <a name="RectangleAsContainer"></a> Usando um retângulo como um contêiner  
 É possível usar um retângulo como um contêiner para outros itens. Quando o retângulo é movido, os itens que estão contidos nele também são movidos. Um item dentro do retângulo mostra o nome do retângulo em sua propriedade **Parent** . Para obter mais informações sobre como usar um retângulo como um contêiner, consulte [Adicionar um retângulo ou contêiner &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md) e [Exibir os mesmos dados em uma matriz e um gráfico &#40;Construtor de Relatórios&#41;](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).  
  
> [!NOTE]  
>  Um retângulo é um contêiner apenas para itens que você cria no retângulo ou arrasta para dentro dele. Se você desenhar um retângulo ao redor de um item que já existe na superfície de design, o retângulo não funcionará como seu contêiner. O retângulo não será listado na propriedade Pai do item.  
  
 Ao usar retângulos para conter itens de relatório, considere a maneira como os itens serão afetados como um todo durante a renderização do relatório. Os itens de relatório que contêm linhas de dados repetidas (por exemplo, tabelas) serão expandidos para acomodar os dados retornados por uma consulta, e isso afeta o posicionamento de outros itens no retângulo. A tabela empurrará os itens para baixo, se eles estiverem posicionados abaixo da região de dados. Para fixar um item no lugar, coloque o item de relatório dentro de um retângulo que tenha uma borda superior acima da borda inferior da tabela. Para obter mais informações, consulte [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
##  <a name="ReportBorder"></a> Adicionando uma borda de relatório  
 É possível adicionar uma borda a um relatório adicionando bordas aos próprios cabeçalhos, rodapés e corpo do relatório, sem adicionar linhas ou retângulos. Para obter mais informações, consulte [Adicionar uma borda a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md).  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 [Adicionar uma borda a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md)  
  
 [Adicionar um retângulo ou um contêiner &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
 [Adicionar e modificar uma linha &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-and-modify-a-line-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar um retângulo ou um contêiner &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
  
