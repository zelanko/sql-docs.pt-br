---
title: painel Dados do Relatório
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 24c11796a758d4cbf3b1da35af16565e0e607535
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74190750"
---
# <a name="report-data-pane-in-sql-server-reporting-services-ssrs"></a>Painel Relatório de Dados no SSRS (SQL Server Reporting Services)

  Use o painel **Dados do Relatório** para exibir os parâmetros, as fontes de dados, os conjuntos de dados, as coleções de campos e as imagens definidos atualmente no relatório. O painel de Dados do Relatório mostra uma exibição hierárquica dos itens que representam dados no relatório. Os nós de nível superior representam campos, parâmetros, imagens e referências de fontes de dados internos. Expanda cada nó para exibir os itens de dados. Por exemplo, ao expandir um nó da fonte de dados, os conjuntos de dados definidos para essa fonte de dados são exibidos. Quando você expande um conjunto de dados, a coleção de campos correspondente é exibida. Arraste os itens para a superfície de design de relatório para vincular os dados aos itens de relatório na página de relatório.  
  
## <a name="options"></a>Opções

 **Campos internos**  
 Representa campos fornecidos pelo Reporting Services que são comumente usados em um relatório, como nome do relatório ou número da página. Para obter mais informações, consulte [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **Parâmetros**  
 Representa a coleção de parâmetros do relatório, cada um dos quais pode ter um valor único ou vários valores. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 **Imagens**  
 Representa o conjunto de imagens usadas no relatório. Para obter mais informações, consulte [Imagens &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md).  
  
 **Fonte de dados**  
 Representa a referência a uma única fonte de dados para uma fonte de dados inserida ou compartilhada. No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], as fontes de dados compartilhadas são exibidas no Gerenciador de Soluções na pasta Fontes de Dados Compartilhados. A fonte de dados especifica um dos tipos de fonte de dados que têm suporte do Reporting Services. Uma fonte de dados é o nó pai da coleção de conjuntos de dados baseada nele. Para saber mais, confira [Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 **Conjunto de dados**  
 Representa um único conjunto de dados. Um conjunto de dados é o nó pai da coleção de campos especificados pela consulta e que inclui todos os campos calculados. O Reporting Services oferece suporte aos designers de consulta para ajudar a especificar uma consulta. Para obter mais informações, consulte [Conjuntos de dados de relatórios &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md) e [Ferramentas de Design de Consultas &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md).  
  
## <a name="next-steps"></a>Próximas etapas

 - [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)
 - [Painel Agrupamento](../../reporting-services/tools/grouping-pane.md)