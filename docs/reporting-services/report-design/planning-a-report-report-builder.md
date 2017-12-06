---
title: "Planejando um relatório (Construtor de Relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- getting started
- report design
ms.assetid: 79113505-1ce8-4f8c-9260-d861838f7813
caps.latest.revision: "19"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: ed5e5031c00a8a4f638f3d3226ae331896e4a35d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="planning-a-report-report-builder"></a>Planejando um relatório (Construtor de Relatórios)
  O Construtor de Relatórios permite que você crie muitos tipos de relatórios paginados. Por exemplo, você pode criar relatórios que mostram dados de vendas resumidos ou detalhados, tendências de marketing e vendas, relatórios operacionais ou painéis. Você também pode criar relatórios que aproveitam texto ricamente formatado, tais como pedidos de vendas, catálogos de produtos ou letras de formulário. Todos esses relatórios são criados usando combinações diferentes dos mesmos blocos de construção básicos no Construtor de Relatórios. Para criar um relatório útil, de fácil compreensão, convém primeiro fazer um planejamento. Antes de começar, considere algumas questões como:  
  
-   **Em qual formato você deseja que o relatório apareça?**  
  
     Você pode renderizar relatórios online em um navegador como o portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou pode exportá-los para outros formatos como Excel, Word ou PDF. A forma final de seu relatório é uma consideração importante porque nem todos os recursos estão disponíveis em todos os formatos de exportação. Para obter mais informações, consulte [Export Reports &#40;Report Builder and SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
-   **Que estrutura você deseja usar para apresentar os dados no relatório?**  
  
     Para apresentar dados, você pode optar entre tabular, matriz (semelhante a uma tabela de referência cruzada ou relatório de Tabela Dinâmica), gráfico, estruturas de formato livre ou qualquer combinação desses itens. Para obter mais informações, consulte [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md) [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
-   **Que aparência você deseja para seu relatório?**  
  
     O Construtor de Relatórios fornece muitos itens de relatório que você pode adicionar ao relatório para tornar sua leitura mais fácil, realçar informações-chave, ajudar o público a navegar no relatório e assim por diante. Saber a aparência desejada para o relatório pode determinar se são necessários itens de relatório tais como caixas de texto, retângulos, imagens e linhas. Talvez você também queira mostrar ou ocultar itens, adicionar um mapa do documento, incluir relatórios detalhados ou sub-relatórios ou vincular a outros relatórios. Para obter mais informações, consulte [Imagens, caixas de texto, retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md) e [Classificação interativa, mapas de documentos e links &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md).  
  
-   **Que dados você deseja que seus leitores vejam? Os dados ou o formato devem ser filtrados para públicos diferentes?**  
  
     Talvez você queira limitar o escopo do relatório a usuários ou locais específicos, ou a um período de tempo específico. Para filtrar os dados de relatório, use parâmetros para recuperar e exibir somente os dados desejados. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
-   **Você precisa criar seus próprios cálculos?**  
  
     Às vezes, sua fonte de dados e conjuntos de dados não contêm os campos exatos de que você precisa no relatório. Nesse caso, é provável que você precise criar seus próprios campos calculados. Por exemplo, talvez você queira multiplicar o preço por unidade pela quantidade para obter a quantidade de vendas de um item de linha. Expressões também são usadas para fornecer formatação condicional e outros recursos avançados. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
-   **Você deseja ocultar itens de relatório inicialmente?**  
  
     Considere se você deseja ocultar itens de relatório, inclusive regiões de dados, grupos e colunas, quando o relatório for executado pela primeira vez. Por exemplo, você pode apresentar uma tabela resumida inicialmente e, depois, detalhar os dados. Para obter mais informações, consulte [Ação de análise detalhada &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md).  
  
-   **Como você vai entregar seu relatório?**  
  
     Você pode salvar o relatório no computador local e continuar trabalhando nele, ou executá-lo localmente para obter suas próprias informações. No entanto, para compartilhar seu relatório com outros, é necessário salvá-lo em um servidor de relatório configurado no modo nativo ou em um servidor de relatório no modo integrado do SharePoint. Salvá-lo em um servidor permite que outros o executem sempre que desejarem. Alternativamente, o administrador do servidor de relatório pode configurar uma assinatura para o relatório ou configurar a entrega do relatório por email para outros indivíduos. Você poderá ter o relatório entregue em um formato de exportação específico se preferir. Para obter mais informações, consulte [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Construtor de Relatórios no SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [Conceitos de criação de relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [Tutoriais do Construtor de Relatórios](../../reporting-services/report-builder-tutorials.md)  
  
  
