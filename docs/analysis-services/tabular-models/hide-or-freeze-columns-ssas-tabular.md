---
title: Ocultar ou congelar colunas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.hideunhidecolumnsdb.f1
ms.assetid: 5407aee5-6a07-4559-a2ba-2ca00a242f02
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4a98f96292409b3a5fc23ff1727eb1ea34efdeff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="hide-or-freeze-columns"></a>Ocultar ou congelar colunas 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  No designer de modelo, se houver colunas que você não deseja exibir na tabela, será possível ocultá-las temporariamente. Ocultar uma coluna libera mais espaço na tela para adicionar novas colunas ou trabalhar somente com as colunas de dados relevantes. Você pode ocultar e reexibir colunas do menu **Coluna** no designer de modelo, e do menu de atalho disponível de cada cabeçalho de coluna. Para manter a área de um modelo visível enquanto você rola para outra área do modelo, bloqueie colunas específicas em uma área congelando-as.  
  
> [!IMPORTANT]  
>  A capacidade de ocultar colunas não visa a segurança dos dados, mas apenas a simplificação e a diminuição da lista de colunas visíveis no designer de modelo ou relatórios. Para proteger dados, você pode definir funções de segurança. As funções podem limitar metadados visíveis e dados a somente esses objetos definidos na função. Para obter mais informações, consulte [funções](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
 Ao ocultar uma coluna, você tem a opção de ocultá-la apenas enquanto trabalha no designer de modelo ou em relatórios. Se você ocultar todas as colunas, a tabela inteira aparecerá em branco no designer de modelo.  
  
> [!NOTE]  
>  Se você tiver muitas colunas a serem ocultas, poderá criar uma perspectiva em vez de ocultar e reexibir colunas. Uma perspectiva é uma exibição personalizada dos dados que facilitam o trabalho com um subconjunto de dados relacionados. Para obter mais informações, consulte [criar e gerenciar perspectivas](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)  
  
### <a name="to-hide-an-individual-column"></a>Para ocultar uma coluna individual  
  
1.  No designer de modelo, selecione a tabela que contém a coluna que você deseja ocultar.  
  
2.  Clique com o botão direito do mouse na coluna, clique em **Ocultar Colunas**e, em seguida, clique em **De Designer e Relatórios**, **De Relatórios**ou **Do Designer**.  
  
### <a name="to-hide-multiple-columns"></a>Para ocultar várias colunas  
  
1.  No designer de modelo, selecione a tabela que contém as colunas que você deseja ocultar.  
  
2.  Clique no menu **Colunas** e depois em **Ocultar e Reexibir**.  
  
3.  Na caixa de diálogo **Ocultar e Reexibir Colunas** , localize cada coluna que você deseja oculta e desmarque a seleção de **No Designer** e **Nos Relatórios**.  
  
4.  Clique em **OK**.  
  
### <a name="to-freeze-columns"></a>Para congelar colunas  
  
1.  No designer de modelo, selecione a tabela que contém as colunas que você deseja congelar.  
  
2.  Selecione um ou mais colunas a serem congeladas.  
  
3.  Clique no menu **Colunas** e depois em **Congelar**.  
  
    > [!NOTE]  
    >  Quando uma coluna é congelada, ela é movida para a esquerda (ou frente) da tabela no designer. Descongelar a coluna não a move para seu local original.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e colunas](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
