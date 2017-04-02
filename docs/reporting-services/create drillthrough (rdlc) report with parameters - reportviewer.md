---
title: "Criar um relat&#243;rio detalhado (RDLC) com par&#226;metros usando o Visualizador de Relat&#243;rios (Tutorial do SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
caps.latest.revision: 8
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Criar um relat&#243;rio detalhado (RDLC) com par&#226;metros usando o Visualizador de Relat&#243;rios (Tutorial do SSRS)
Um relatório de [detalhamento](http://technet.microsoft.com/library/ff519554.aspx) é um relatório que pode ser aberto pelo usuário quando ele clica em um link dentro de outro relatório. Os relatórios detalhados normalmente contêm detalhes sobre um item que está em um relatório de resumo original. Este tutorial apresentará as lições a seguir sobre como criar um relatório de detalhamento com parâmetros e uma consulta, no [relatório de modo local](http://msdn.microsoft.com/library/ff487969.aspx).  
  
## Requisitos  
Para usar este passo a passo, você deverá ter acesso ao banco de dados de exemplo **AdventureWorks2014**. Para obter mais informações sobre como obter o banco de dados de exemplo **AdventureWorks2014**, consulte [Amostras de produto do Banco de Dados Microsoft SQL Server](http://msftdbprodsamples.codeplex.com/).  
  
Este passo a passo pressupõe que você esteja familiarizado com as consultas Transaction-SQL e os objetos [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) e [DataTable](http://msdn.microsoft.com/library/system.data.datatable.aspx) do ADO.NET.  
  
Use o Visual Studio 2015 e o Aplicativo Web ASP .NET para criar uma página da Web ASP.NET com um controle ReportViewer. O controle é configurado para exibir um relatório criado por você. Neste passo a passo, você cria o aplicativo no Microsoft Visual C #.  
  
## Tarefas  
[Lição 1: Criar um novo site](../reporting-services/lesson-1-create-a-new-web-site.md)  
[Lição 2: Definir uma conexão de dados e uma tabela de dados para o relatório pai](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)  
[Lição 3: Criar o relatório pai usando o Assistente de Relatório](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)  
[Lição 4: Definir uma conexão de dados e uma tabela de dados para o relatório filho](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)  
[Lição 5: Criar o relatório filho usando o Assistente de Relatório](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)  
[Lição 6: adicionar um controle ReportViewer ao aplicativo](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)  
[Lição 7: Adicionar ação de detalhamento ao relatório pai](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)  
[Lição 8: Criar um filtro de dados](../reporting-services/lesson-8-create-a-data-filter.md)  
[Lesson 9: Build and Run the Application](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## Consulte também  
[Tutoriais do Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)  
[Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](../reporting-services/tools/design-reports-with-report-designer-ssrs.md)  
  
