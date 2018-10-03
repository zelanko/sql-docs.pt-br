---
title: Renomear uma tabela ou coluna (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.renametableorcolumn.f1
ms.assetid: 88061a39-c5aa-403d-a52b-7fdb365fc235
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f9a869b4a280f8df44fce4c506c5f77afc7e8f9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085576"
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
  
-   Os seguintes caracteres (que não são válidos nos nomes de objetos do Analysis Services):., ': / \\*|? & % $! [] () de + ={}<>  
  
-   As palavras-chave reservadas do Analysis Services, incluindo nomes de função e operadores de Linguagens MDX (MDX) e DMX (Data Mining Extensions).  
  
## <a name="effect-of-renaming-on-existing-tables-columns-and-calculations"></a>Efeito de renomear tabelas, colunas e cálculos existentes  
 Sempre que altera o nome de uma tabela, você altera o nome do objeto de tabela subjacente que pode conter várias colunas ou medidas. Portanto, as colunas que estiverem na tabela e as relações que usam a tabela deverão ser atualizadas para usar o novo nome em suas definições. Essa atualização ocorre automaticamente em alguns casos. Medidas não são atualizadas automaticamente.  
  
 Além disso, qualquer cálculo que use a tabela renomeada ou as colunas da tabela renomeada também deverá ser atualizado, e os dados derivados desses cálculos deverão ser atualizados e recalculados. Dependendo da quantidade de tabelas e cálculos afetados, a conclusão dessa operação poderá demorar algum tempo. Portanto, o melhor momento para renomear tabelas é durante o processo de importação ou antes de você começar a criar relacionamentos e cálculos complexos.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e colunas &#40;Tabular do SSAS&#41;](tables-and-columns-ssas-tabular.md)   
 [Importar do PowerPivot &#40;Tabular do SSAS&#41;](import-from-power-pivot-ssas-tabular.md)   
 [Importar do Analysis Services &#40;Tabular do SSAS&#41;](import-from-analysis-services-ssas-tabular.md)  
  
  
