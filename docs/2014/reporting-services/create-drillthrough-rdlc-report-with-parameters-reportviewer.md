---
title: Criar um relatório de detalhamento (RDLC) com parâmetros usando o ReportViewer (Tutorial SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bb5bb2c0a02de9d4be433203996072bb218b8c0f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157817"
---
# <a name="create-a-drillthrough-rdlc-report-with-parameters-using-reportviewer-ssrs-tutorial"></a>Criar um relatório detalhado (RDLC) com parâmetros usando o Visualizador de Relatórios (Tutorial do SSRS)
  Um relatório de [detalhamento](http://technet.microsoft.com/library/ff519554.aspx) é um relatório que pode ser aberto pelo usuário quando ele clica em um link dentro de outro relatório. Os relatórios detalhados normalmente contêm detalhes sobre um item que está em um relatório de resumo original. Este tutorial apresentará as lições a seguir sobre como criar um relatório de detalhamento com parâmetros e uma consulta, no [relatório de modo local](http://msdn.microsoft.com/library/ff487969.aspx).  
  
## <a name="requirements"></a>Requisitos  
 Para usar este passo a passo, você deve ter acesso para o **AdventureWorks2008** banco de dados de exemplo. A consulta usada neste passo a passo também funcionarão com **AdventureWorks2012** banco de dados. Para obter mais informações sobre como obter o **AdventureWorks2008** banco de dados de exemplo, consulte [Walkthrough: Installing the AdventureWorks Database](http://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx) para Microsoft Visual Studio 2010.  
  
 Este passo a passo pressupõe que você esteja familiarizado com consultas Transaction-SQL e ADO.NET [DataSet](http://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) e [DataTable](http://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) objetos.  
  
 Use o Visual Studio 2010 ou o Visual Studio 2012 e o modelo de site ASP.NET para criar uma página da Web ASP.NET com um controle ReportViewer. O controle é configurado para exibir um relatório criado por você. Neste passo a passo, você cria o aplicativo no Microsoft Visual C #.  
  
## <a name="tasks"></a>Tarefas  
 [Lição 1: Criar um novo Site](../reporting-services/lesson-1-create-a-new-web-site.md)   
 [Lição 2: Definir uma Conexão de dados e uma tabela de dados para o relatório pai](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)   
 [Lição 3: Criar o relatório pai usando o Assistente de relatório](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)   
 [Lição 4: Definir uma Conexão de dados e uma tabela de dados para o relatório filho](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)   
 [Lição 5: Criar o relatório filho usando o Assistente de relatório](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)   
 [Lição 6: Adicionar um controle ReportViewer ao aplicativo](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)   
 [Lição 7: Adicionar ação de detalhamento ao relatório pai](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)   
 [Lição 8: Criar um filtro de dados](../reporting-services/lesson-8-create-a-data-filter.md)   
 [Lição 9: Criar e executar o aplicativo](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)   
 [Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
