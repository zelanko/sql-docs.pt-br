---
title: "Painel de dados do relatório | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10039"
- sql13.rtp.rptdesigner.reportdata.f1
- "10435"
helpviewer_keywords: Report Data pane
ms.assetid: aa9614a3-12e7-4e17-9de2-fafccd1f5f9d
caps.latest.revision: "28"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7cf62bd96312d0a6aa5d05afb17ae3d0f8ec8f40
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="report-data-pane"></a>painel Dados do Relatório
  Use o painel **Dados do Relatório** para exibir os parâmetros, as fontes de dados, os conjuntos de dados, as coleções de campos e as imagens definidos atualmente no relatório. O Painel Relatório mostra uma exibição hierárquica dos itens que representam dados no relatório. Os nós de nível superior representam campos, parâmetros, imagens e referências de fontes de dados internos. Expanda cada nó para exibir os itens de dados. Por exemplo, ao expandir um nó da fonte de dados, os conjuntos de dados definidos para essa fonte de dados são exibidos. Quando você expande um conjunto de dados, a coleção de campos correspondente é exibida. Arraste os itens para a superfície de design de relatório para vincular os dados aos itens de relatório na página de relatório.  
  
## <a name="options"></a>Opções  
 **Campos internos**  
 Representa campos fornecidos pelo Reporting Services que são comumente usados em um relatório, como nome do relatório ou número da página. Para obter mais informações, consulte [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **Parâmetros**  
 Representa a coleção de parâmetros do relatório, cada um dos quais pode ter um valor único ou vários valores. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 **Imagens**  
 Representa o conjunto de imagens usadas no relatório. Para obter mais informações, consulte [Imagens &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md).  
  
 **Fonte de dados**  
 Representa a referência a uma única fonte de dados para uma fonte de dados inserida ou compartilhada. No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], as fontes de dados compartilhadas são exibidas no Gerenciador de Soluções na pasta Fontes de Dados Compartilhados. A fonte de dados especifica um dos tipos de fonte de dados que têm suporte do Reporting Services. Uma fonte de dados é o nó pai da coleção de conjuntos de dados baseada nele. Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 **Conjunto de dados**  
 Representa um único conjunto de dados. Um conjunto de dados é o nó pai da coleção de campos especificados pela consulta e que inclui todos os campos calculados. O Reporting Services oferece suporte aos designers de consulta para ajudar a especificar uma consulta. Para obter mais informações, consulte [Conjuntos de dados de relatórios &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md) e [Ferramentas de Design de Consultas &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Painel Agrupamento](../../reporting-services/tools/grouping-pane.md)  
  
  
