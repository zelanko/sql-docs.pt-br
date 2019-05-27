---
title: Adicionar caixa de diálogo de dimensão de cubo (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.addcubedimensiondialog.f1
helpviewer_keywords:
- Add Cube Dimension dialog box
ms.assetid: 625a3b1f-183b-445f-9bb7-96945c324767
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f147c438e16c00e0e1b979f2d3e2fe6e16cf7428
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062951"
---
# <a name="add-cube-dimension-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Adicionar Dimensão do Cubo (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Adicionar Dimensão do Cubo** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para adicionar uma referência a uma dimensão de banco de dados em um cubo. Você pode exibir a caixa de diálogo **Adicionar Dimensão do Cubo** procedendo de uma das seguintes maneiras:  
  
-   Clique em **Adicionar Dimensão do Cubo** no painel **Barra de Ferramentas** na guia **Estrutura do Cubo** ou **Uso da Dimensão** no Designer de Cubo.  
  
-   Clique com o botão direito do mouse no painel **Dimensões** na guia **Estrutura do Cubo** no Designer de Cubo e selecione **Adicionar Dimensão do Cubo** no menu de contexto.  
  
-   Clique com o botão direito do mouse no painel **Grade** na guia **Uso da Dimensão** no Designer de Cubo e selecione **Adicionar Dimensão do Cubo** no menu de contexto.  
  
> [!NOTE]  
>  Cada dimensão de cubo pode ter apenas uma relação com um grupo de medidas. No entanto é possível criar mais de uma dimensão de cubo e adicioná-la ao cubo, se a dimensão do banco de dados no qual a dimensão do cubo é baseada estiver relacionada a grupos de medidas através de mais de uma relação na exibição da fonte de dados. Essas dimensões são referenciadas como dimensões com função múltipla e normalmente ocorrem com dimensões de tempo.  
  
## <a name="options"></a>Opções  
 **Selecionar Dimensão**  
 Selecione uma dimensão de banco de dados existente para adicionar uma dimensão de cubo baseada nessa dimensão ao cubo selecionado. Várias dimensões de cubo podem ser definidas a partir da mesma dimensão de banco de dados.  
  
> [!NOTE]  
>  Se mais de uma dimensão de cubo baseadas na mesma dimensão de banco de dados forem adicionadas a um cubo, as dimensões de cubo adicionais serão chamadas de dimensões com função múltipla.  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
