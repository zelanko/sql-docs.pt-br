---
title: Alinhar os dados de um gráfico em uma tabela ou matriz (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d639e686251effc19e445a39c97860a3336c8ff2
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65581881"
---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>Alinhar os dados de um gráfico em uma tabela ou matriz (Construtor de Relatórios e SSRS)
  Minigráficos e barras de dados são gráficos simples que transmitem muitas informações com poucos detalhes externos. Em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , quando você marca essa opção, os valores nos minigráficos e nas barras de dados são alinhados nas diferentes células da tabela ou matriz, mesmo que valores estejam faltando nos dados nos quais eles se baseiam.  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 Nesta imagem, o gráfico de coluna mostra vendas diárias para cada funcionário. Observe que para os dias em que um funcionário não tem vendas, o gráfico deixa um espaço em branco e alinha os dias seguintes horizontalmente. Também alinha os gráficos verticalmente tornando os tamanhos dos diferentes gráficos relativos uns aos outros. Para obter mais informações, consulte [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="align-the-data-in-a-sparkline-or-data-bar"></a>Alinhar os dados em um minigráfico ou barra de dados  
  
1.  [Adicionar um minigráfico ou uma barra de dados](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md) a uma tabela ou matriz.  
  
2. Clique no minigráfico ou na barra de dados e clique em **Propriedades do Eixo Horizontal** ou **Propriedades do Eixo Vertical**.  
  
2.  Na guia **Opções do Eixo** , marque a caixa **Alinhar eixos em** e, na caixa suspensa, selecione o grupo no qual alinhar o eixo.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Adicionar minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
