---
title: Criar um relatório de detalhamento (RDLC) com parâmetros usando o ReportViewer (tutorial do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7efb713b5dbf9a3f19118bb3572ccd35778aad19
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109645"
---
# <a name="create-a-drillthrough-rdlc-report-with-parameters-using-reportviewer-ssrs-tutorial"></a>Criar um relatório detalhado (RDLC) com parâmetros usando o Visualizador de Relatórios (Tutorial do SSRS)
  Um relatório de [detalhamento](https://technet.microsoft.com/library/ff519554.aspx) é um relatório que pode ser aberto pelo usuário quando ele clica em um link dentro de outro relatório. Os relatórios detalhados normalmente contêm detalhes sobre um item que está em um relatório de resumo original. Este tutorial apresentará as lições a seguir sobre como criar um relatório de detalhamento com parâmetros e uma consulta, no [relatório de modo local](local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md).  
  
## <a name="requirements"></a>Requisitos  
 Para usar este passo a passos, você deve ter acesso ao banco de dados de exemplo **AdventureWorks2008** . A consulta usada nesta explicação também funcionará com o banco de dados **AdventureWorks2012** . Para obter mais informações sobre como obter o banco de dados de exemplo **AdventureWorks2008** , consulte [Walkthrough: Installing the AdventureWorks database](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx) for Microsoft Visual Studio 2010.  
  
 Este passo a passo pressupõe que você esteja familiarizado com as consultas Transaction-SQL e os objetos [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) e [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) do ADO.NET.  
  
 Use o Visual Studio 2010 ou o Visual Studio 2012 e o modelo de site ASP.NET para criar uma página da Web ASP.NET com um controle ReportViewer. O controle é configurado para exibir um relatório criado por você. Neste passo a passo, você cria o aplicativo no Microsoft Visual C #.  
  
## <a name="tasks"></a>Tarefas  
 [Lição 1: criar um novo site](../reporting-services/lesson-1-create-a-new-web-site.md)   
 [Lição 2: definir uma conexão de dados e uma tabela de dados para o relatório pai](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)   
 [Lição 3: criar o relatório pai usando o assistente de relatório](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)   
 [Lição 4: definir uma conexão de dados e uma tabela de dados para o relatório filho](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)   
 [Lição 5: criar o relatório filho usando o assistente de relatório](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)   
 [Lição 6: adicionar um controle ReportViewer ao aplicativo](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)   
 [Lição 7: Adicionar ação de detalhamento ao relatório pai](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)   
 [Lição 8: criar um filtro de dados](../reporting-services/lesson-8-create-a-data-filter.md)   
 [Lição 9: Criar e executar o aplicativo](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Reporting Services tutoriais &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)   
 [Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
