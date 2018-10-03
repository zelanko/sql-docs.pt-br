---
title: Alinhar os dados de um gráfico em uma tabela ou matriz (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 7277e8a0b50fb8e67a6601218190241c11efbd74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102406"
---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>Alinhar os dados de um gráfico em uma tabela ou matriz (Construtor de Relatórios e SSRS)
  Minigráficos e barras de dados são gráficos simples que transmitem muitas informações com poucos detalhes externos. Quando você marca essa opção, os valores nos minigráficos e nas barras de dados são alinhados nas diferentes células da tabela ou matriz, mesmo que valores estejam faltando nos dados nos quais eles se baseiam.  
  
 ![rs_SparklineAlignData](../media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 Nesta imagem, o gráfico de coluna mostra vendas diárias para cada funcionário. Observe que para os dias em que um funcionário não tem vendas, o gráfico deixa um espaço em branco e alinha os dias seguintes horizontalmente. Também alinha os gráficos verticalmente tornando os tamanhos dos diferentes gráficos relativos uns aos outros. Para obter mais informações, consulte [Sparklines and Data Bars &#40;Report Builder and SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="align-the-data-in-a-sparkline-or-data-bar"></a>Alinhar os dados em um minigráfico ou barra de dados  
  
1.  Clique no minigráfico ou na barra de dados e clique em **Propriedades do Eixo Horizontal** ou **Propriedades do Eixo Vertical**.  
  
2.  Na guia **Opções do Eixo** , marque a caixa **Alinhar eixos em** e, na caixa suspensa, selecione o grupo no qual alinhar o eixo.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Adicionar minigráficos e barras de dados &#40;relatórios e SSRS&#41;](add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
