---
title: Renomear uma tabela ou coluna (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.renametableorcolumn.f1
ms.assetid: 88061a39-c5aa-403d-a52b-7fdb365fc235
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: edfd1fe4e353f74f9729325b40865905a1907dc2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="rename-a-table-or-column-ssas-tabular"></a>Renomear uma tabela ou coluna (SSAS tabular)
  É possível alterar o nome de uma tabela durante o processo de importação por meio da digitação de um **Nome Amigável** na página **Selecionar Tabelas e Exibições** do **Assistente de Importação de Tabela**. Você também poderá alterar tabela e nomes de coluna se importar dados especificando uma consulta na página **Especificar uma Consulta SQL** do **Assistente de Importação de Tabela**.  
  
 Depois de adicionar os dados ao modelo, o nome (ou título) da tabela aparece na guia da tabela, na parte inferior da janela do designer de modelo. É possível alterar o nome da tabela para um nome mais apropriado. Você também poderá renomear uma coluna depois que os dados forem adicionados ao modelo. Essa opção é especialmente importante quando você importa dados de várias fontes e deseja assegurar que as colunas nas diferentes tabelas tenham nomes fáceis de distinguir.  
  
### <a name="to-rename-a-table"></a>Para renomear uma tabela  
  
1.  No designer de modelo, clique com o botão direito do mouse na guia que contém a tabela que você deseja renomear e clique em **Renomear**.  
  
2.  Digite o novo nome.  
  
    > [!NOTE]  
    >  Você pode alterar outras propriedades de uma tabela, inclusive as informações de conexão e mapeamento de colunas, usando a caixa de diálogo **Editar Propriedades da Tabela** . No entanto, você não pode alterar o nome nessa caixa de diálogo.  
  
### <a name="to-rename-a-column"></a>Para renomear uma coluna  
  
1.  No designer do modelo, clique duas vezes no cabeçalho da coluna que você deseja renomear, ou clique com o botão direito do mouse no cabeçalho e selecione **Renomear Coluna** no menu de contexto.  
  
2.  Digite o novo nome.  
  
## <a name="naming-requirements-for-columns-and-tables"></a>Requisitos de nomenclatura para colunas e tabelas  
 As seguintes palavras e caracteres não podem ser usadas no nome de uma tabela ou coluna:  
  
-   Espaços à esquerda ou à direita  
  
-   Caracteres de controle  
  
-   Os seguintes caracteres (que não são válidos nos nomes de objetos do Analysis Services): .,;':/\\*|?&%$!+=()[]{}<>  
  
-   As palavras-chave reservadas do Analysis Services, incluindo nomes de função e operadores de Linguagens MDX (MDX) e DMX (Data Mining Extensions).  
  
## <a name="effect-of-renaming-on-existing-tables-columns-and-calculations"></a>Efeito de renomear tabelas, colunas e cálculos existentes  
 Sempre que altera o nome de uma tabela, você altera o nome do objeto de tabela subjacente que pode conter várias colunas ou medidas. As colunas que estão na tabela e as relações que usam a tabela devem ser atualizadas para usar o novo nome em suas definições. Essa atualização ocorre automaticamente na maioria dos casos.
  
 Qualquer cálculo que use a tabela renomeada ou as colunas da tabela renomeada também deverá ser atualizado, e os dados derivados desses cálculos devem ser atualizados e recalculados. Dependendo da quantidade de tabelas e cálculos afetados, a conclusão dessa operação poderá demorar algum tempo. Portanto, o melhor momento para renomear tabelas é durante o processo de importação ou antes de você começar a criar relacionamentos e cálculos complexos.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e colunas](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Importar do PowerPivot](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)   
 [Importar do Analysis Services](../../analysis-services/tabular-models/import-from-analysis-services-ssas-tabular.md)  
  
  
