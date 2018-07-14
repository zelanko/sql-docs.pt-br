---
title: (Guia estrutura da dimensão, Designer de dimensão) de exibição da fonte de dados (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.datasourcepane.f1
ms.assetid: c4bd3c5e-8986-448f-b9db-3551f50f0696
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa82d94a6e034c514b173e623f8c6d0ab9932880
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246152"
---
# <a name="data-source-view-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a>Exibição da Fonte de Dados (guia Estrutura da Dimensão, Designer de Dimensão) (Analysis Services - Dados Multidimensionais)
  Use o painel **Exibição da Fonte de Dados** para exibir tabelas e colunas da exibição da fonte de dados associada à dimensão selecionada. Esse painel é usado para criar atributos, propriedades de membros, hierarquias e níveis arrastando colunas do painel **Exibição da Fonte de Dados** para o painel **Atributos** ou **Hierarquias e Níveis** .  
  
## <a name="options"></a>Opções  
 **Exibição da fonte de dados**  
 Mostra a exibição da fonte de dados associada à dimensão selecionada.  
  
 **(Mover ponto de Vista)**  
 Clique no canto inferior direito do painel, entre as barras de rolagem, para selecionar uma área do painel **Exibição da Fonte de Dados** para exibição.  
  
## <a name="diagram-context-menu"></a>Menu de Contexto de Diagrama  
 As opções listadas na tabela a seguir estão disponíveis no menu de contexto que é exibido quando você clica com o botão direito do mouse na tela de fundo do diagrama do painel **Exibição da Fonte de Dados** .  
  
 **Mostrar tabelas**  
 Exibe a caixa de diálogo **Mostrar Tabelas**. Para obter mais informações sobre a caixa de diálogo **Mostrar Tabela**, consulte [Caixa de diálogo Mostrar Tabela &#40;Analysis Services – Dados Multidimensionais&#41;](show-table-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Mostrar todas as tabelas**  
 Exibe no painel todas as tabelas incluídas na exibição da fonte de dados associada à dimensão.  
  
 **Mostrar somente tabelas usadas**  
 Exibe no painel somente as tabelas usadas pela dimensão da exibição da fonte de dados associada.  
  
 **Mostrar nomes amigáveis**  
 Selecione para mostrar nomes amigáveis dos objetos no painel.  
  
 **Selecionar Tudo**  
 Seleciona todos os objetos no painel.  
  
 **Localizar Tabela**  
 Exibe a caixa de diálogo **Localizar Tabela**. Para obter mais informações sobre a caixa de diálogo **Localizar Tabela**, consulte [Caixa de diálogo Localizar Tabela &#40;Analysis Services – Dados Multidimensionais&#41;](find-table-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Organizar tabelas**  
 Organiza os objetos no painel de acordo com o layout especificado selecionando **Alternar para Layout Diagonal** ou **Alternar para Layout Retangular**.  
  
 **Alternar para Layout Diagonal**  
 Selecione para organizar objetos em um padrão diagonal.  
  
> [!NOTE]  
>  Esta opção será exibida somente se a opção **Alternar para Layout Retangular** estiver selecionada.  
  
 **Alternar para Layout retangular**  
 Selecione para organizar objetos em um padrão retangular.  
  
> [!NOTE]  
>  Esta opção será exibida somente se a opção **Alternar para Layout Diagonal** estiver selecionada.  
  
 **Editar exibição da fonte de dados**  
 Exibe o **Designer da Exibição da Fonte de Dados** da exibição da fonte de dados associada à dimensão. Para obter mais informações sobre o **Designer de Exibição da Fonte de Dados**, consulte [Designer de Exibição da Fonte de Dados &#40;Analysis Services – Dados Multidimensionais&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Mostrar exibição de fonte de dados em**  
 Selecione uma das seguintes opções para ativar/desativar a exibição do painel **Exibição da Fonte de Dados** nos seguintes modos:  
  
-   Diagrama  
  
     Exibe um diagrama das tabelas e colunas associadas à dimensão atual.  
  
-   trEE  
  
     Exibe uma árvore que contém tabelas e colunas associadas à dimensão atual.  
  
 **Copiar diagrama de**  
 Selecione um dos diagramas incluídos na exibição da fonte de dados associada à dimensão para exibi-lo no painel **Exibição da Fonte de Dados** .  
  
 **Zoom**  
 Selecione uma opção de zoom disponível.  
  
 **Propriedades**  
 Exibe a janela **Propriedades** no **SQL Server Data Tools** para a exibição da fonte de dados associada à dimensão.  
  
## <a name="table-context-menu"></a>Menu de Contexto da Tabela  
 As opções listadas na tabela a seguir estão disponíveis no menu de contexto exibido quando você clica com o botão direito do mouse no nome de uma tabela ou exibição no painel **Exibição da Fonte de Dados** .  
  
 **Mostrar tabelas relacionadas**  
 Exibe no painel as tabelas relacionadas à tabela selecionada na exibição da fonte de dados.  
  
 **Ocultar tabela**  
 Remove a tabela do painel.  
  
 **Explorar Dados**  
 Exibe a caixa de diálogo **Explorar Dados** para a tabela selecionada.  
  
 **Editar exibição da fonte de dados**  
 Exibe o **Designer da Exibição da Fonte de Dados** da exibição da fonte de dados que contém a tabela selecionada. Para obter mais informações sobre o **Designer de Exibição da Fonte de Dados**, consulte [Designer de Exibição da Fonte de Dados &#40;Analysis Services – Dados Multidimensionais&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Propriedades**  
 Exibe a janela **Propriedades** no **SQL Server Data Tools** da tabela selecionada.  
  
## <a name="column-context-menu"></a>Menu de Contexto da Coluna  
 As opções listadas na tabela a seguir estão disponíveis no menu de contexto exibido quando você clica com o botão direito do mouse no nome de uma coluna em uma tabela ou exibição no painel **Exibição da Fonte de Dados** .  
  
 **Novo atributo da coluna**  
 Exibe no painel as tabelas relacionadas à tabela selecionada na exibição da fonte de dados.  
  
 **Explorar Dados**  
 Exiba a caixa de diálogo **Explorar Dados** da tabela que contém a coluna selecionada.  
  
 **Editar exibição da fonte de dados**  
 Exibe o **Designer de Exibição da Fonte de Dados** da exibição da fonte de dados que contém a coluna selecionada. Para obter mais informações sobre o **Designer de Exibição da Fonte de Dados**, consulte [Designer de Exibição da Fonte de Dados &#40;Analysis Services – Dados Multidimensionais&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Propriedades**  
 Exibe a janela **Propriedades** no **SQL Server Data Tools** da coluna selecionada.  
  
## <a name="relationship-context-menu"></a>Menu de Contexto da Relação  
 As opções listadas na tabela a seguir são disponíveis no menu de contexto que é exibido quando você clica com o botão direito do mouse em uma relação no painel **Exibição da Fonte de Dados** .  
  
 **Editar exibição da fonte de dados**  
 Exibe o **Designer de Exibição da Fonte de Dados** que contém a relação selecionada. Para obter mais informações sobre o **Designer de Exibição da Fonte de Dados**, consulte [Designer de Exibição da Fonte de Dados &#40;Analysis Services – Dados Multidimensionais&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Propriedades**  
 Exibe a janela **Propriedades** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] da relação selecionada.  
  
## <a name="see-also"></a>Consulte também  
 [Estrutura da dimensão &#40;Designer de dimensão&#41; &#40;Analysis Services - dados multidimensionais&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia estrutura da dimensão, Designer de dimensão&#41; &#40;Analysis Services - dados multidimensionais&#41;](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)   
 [Atributos &#40;guia estrutura da dimensão, Designer de dimensão&#41; &#40;Analysis Services - dados multidimensionais&#41;](attributes-dimension-designer-analysis-services-multidimensional-data.md)   
 [Hierarquias &#40;guia estrutura da dimensão, Designer de dimensão&#41; &#40;Analysis Services - dados multidimensionais&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
