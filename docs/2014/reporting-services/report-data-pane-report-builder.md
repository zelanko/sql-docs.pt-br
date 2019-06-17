---
title: Painel de dados (construtor de relatórios) do relatório | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10435"
helpviewer_keywords:
- Report Data pane
ms.assetid: 1492aa39-aeb1-4509-ab97-b9edd0901b7e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fa8ae6d36ddd7c23b48ec65f8fab387e690f1d83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107563"
---
# <a name="report-data-pane-report-builder"></a>Painel de Dados do Relatório (Construtor de Relatórios)
  Use o painel **Dados do Relatório** para exibir os parâmetros, as fontes de dados, os conjuntos de dados, as coleções de campos e as imagens definidos atualmente no relatório. O Painel Relatório mostra uma exibição hierárquica dos itens que representam dados no relatório. Os nós de nível superior representam campos, parâmetros, imagens e referências de fontes de dados internos. Expanda cada nó para exibir os itens de dados. Por exemplo, ao expandir um nó da fonte de dados, os conjuntos de dados definidos para essa fonte de dados são exibidos. Quando você expande um conjunto de dados, a coleção de campos correspondente é exibida. Arraste itens para a superfície de design do relatório ou para o painel Agrupamento a fim de vincular dados aos itens de relatório selecionados na página de relatório. Para obter mais informações, consulte [Modo de exibição de Design de relatório &#40;Construtor de Relatórios&#41;](report-builder/report-design-view-report-builder.md).  
  
## <a name="options"></a>Opções  
 **Campos internos**  
 Representa campos comumente usados em um relatório, como o nome do relatório ou o número da página. Para obter mais informações, consulte [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **Parâmetros**  
 Representa a coleção de parâmetros do relatório, cada um dos quais pode ter um valor único ou vários valores. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](report-design/report-parameters-report-builder-and-report-designer.md).  
  
 **Imagens**  
 Representa o conjunto de imagens usadas no relatório. Para obter mais informações, consulte [Imagens &#40;Construtor de Relatórios e SSRS&#41;](report-design/images-report-builder-and-ssrs.md).  
  
 **Fontes de dados**  
 Representa uma fonte de dados inserida ou uma referência para uma fonte de dados compartilhada. Uma fonte de dados representa uma fonte de dados para o relatório. Uma fonte de dados é o nó pai da coleção de conjuntos de dados que a utiliza. Para obter mais informações, consulte [adicionar dados a um relatório &#40;construtor de relatórios e SSRS&#41; ](report-data/report-datasets-ssrs.md) e [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no construtor de relatórios](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
 **Conjuntos de dados**  
 Representa os dados recuperados de uma fonte de dados com a execução de um comando, por exemplo, uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que recupere dados de um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Um conjunto de dados é o nó pai da coleção de campos especificados pela consulta e também inclui campos calculados. O Construtor de Relatórios oferece suporte aos designers de consulta para ajudar a especificar uma consulta. Para obter mais informações, consulte [adicionar dados a um relatório &#40;construtor de relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Painel Agrupamento &#40;Construtor de Relatórios&#41;](report-design/grouping-pane-report-builder.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
