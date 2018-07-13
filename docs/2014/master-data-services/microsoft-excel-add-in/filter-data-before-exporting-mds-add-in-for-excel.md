---
title: Filtrar dados antes de carregar (suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 56cec33d57fc78122bdae7fd6d64a774919b18f5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37182887"
---
# <a name="filter-data-before-loading-mds-add-in-for-excel"></a>Filtrar dados antes de carregar (suplemento MDS para Excel)
  Na [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], filtre os dados quando você deseja limitar o tamanho ou o escopo dos dados que você está carregando no Excel.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
### <a name="to-filter-data-before-loading"></a>Para filtrar dados antes de carregar  
  
1.  Abra o Excel e, na guia **Dados Mestre** , conecte-se a um repositório do MDS. Para obter mais informações, consulte [Conectar-se a um repositório do MDS &#40;Suplemento MDS para Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  No painel do **Master Data Explorer** , selecione um modelo e uma versão. A lista de entidades será preenchida.  
  
    -   Se o painel do **Master Data Explorer** não estiver visível, no grupo **Conectar e Carregar** , clique em **Mostrar Explorer**.  
  
    -   Se o painel **Master Data Explorer** estiver desabilitado, isso significará que a planilha existente já contém dados gerenciados pelo MDS. Para habilitar o painel, abra uma nova planilha.  
  
3.  No painel do **Master Data Explorer** , na lista de entidades, clique na entidade que você deseja filtrar.  
  
4.  Na faixa de opções, no grupo **Conectar e Carregar** , clique em **Filtrar**.  
  
5.  Preencha a caixa de diálogo **Filtrar** selecionando os atributos (colunas) a serem exibidos, definindo a ordem das colunas e, se necessário, filtrando os dados para que menos linhas sejam retornadas. Abra o painel **Resumo** para saber a quantidade de dados que será retornada. Para obter mais informações, consulte [Caixa de diálogo Filtrar &#40;Suplemento MDS para Excel&#41;](filter-dialog-box-mds-add-in-for-excel.md).  
  
6.  Clique em **Carregar Dados**. A planilha será preenchida com os dados gerenciados no MDS.  
  
    > [!NOTE]  
    >  -   Somente os primeiros um milhão de membros serão carregados no Excel.  
    > -   Nas colunas que são listas restritas (atributos baseados em domínio), somente os primeiros 1000 valores são carregados.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Publicar dados do Excel no MDS &#40;suplemento do MDS para Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Consulte também  
 [Carregamento de dados &#40;suplemento do MDS para Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Caixa de diálogo Filtrar &#40;Suplemento MDS para Excel&#41;](filter-dialog-box-mds-add-in-for-excel.md)   
 [Reordenar colunas &#40;suplemento do MDS para Excel&#41;](reorder-columns-mds-add-in-for-excel.md)  
  
  
