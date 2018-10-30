---
title: Criar um relatório de detalhamento (RDLC) com parâmetros – ReportViewer | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 68ea91137c584959c53ee8de010dbff92106c119
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50028055"
---
# <a name="create-drillthrough-rdlc-report-with-parameters---reportviewer"></a>Criar um relatório de detalhamento (RDLC) com parâmetros – ReportViewer
Um relatório de [detalhamento](https://technet.microsoft.com/library/ff519554.aspx) é um relatório que pode ser aberto pelo usuário quando ele clica em um link dentro de outro relatório. Os relatórios detalhados normalmente contêm detalhes sobre um item que está em um relatório de resumo original. Este tutorial apresentará as lições a seguir sobre como criar um relatório de detalhamento com parâmetros e uma consulta, no [relatório de modo local](report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md).  
  
## <a name="requirements"></a>Requisitos  
Para usar este passo a passo, você deverá ter acesso ao banco de dados de exemplo **AdventureWorks2014** . Para obter mais informações sobre como obter o banco de dados de exemplo **AdventureWorks2014**, consulte [Bancos de dados de exemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases).  
  
Este passo a passo pressupõe que você esteja familiarizado com as consultas Transaction-SQL e os objetos [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) e [DataTable](https://msdn.microsoft.com/library/system.data.datatable.aspx) do ADO.NET.  
  
Use o Visual Studio 2015 e o Aplicativo Web ASP .NET para criar uma página da Web ASP.NET com um controle ReportViewer. O controle é configurado para exibir um relatório criado por você. Neste passo a passo, você cria o aplicativo no Microsoft Visual C #.  
  
## <a name="tasks"></a>Tarefas  
[Lição 1: Criar um novo site](../reporting-services/lesson-1-create-a-new-web-site.md)  
[Lição 2: Definir uma conexão de dados e uma tabela de dados para o relatório pai](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)  
[Lição 3: Criar o relatório pai usando o Assistente de Relatório](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)  
[Lição 4: Definir uma conexão de dados e uma tabela de dados para o relatório filho](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)  
[Lição 5: Criar o relatório filho usando o Assistente de Relatório](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)  
[Lição 6: Adicionar um controle ReportViewer ao aplicativo](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)  
[Lição 7: Adicionar ação de detalhamento ao relatório pai](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)  
[Lição 8: Criar um filtro de dados](../reporting-services/lesson-8-create-a-data-filter.md)  
[Lesson 9: Build and Run the Application](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>Consulte Também  
[Tutoriais do Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)  
[Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  

