---
title: "Lição 6: Adicionar um controle ReportViewer ao aplicativo | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
caps.latest.revision: "7"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0b2fbe90e3c3f1e2f109b87de4a07b884fb49d3d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>Lição 6: adicionar um controle ReportViewer ao aplicativo
Depois que você criar o relatório filho usando o Assistente de Relatório, a próxima etapa será adicionar um controle ReportViewer ao aplicativo de site. Se você estiver usando o Site de Relatórios ASP.NET, ele terá adicionado o controle ReportViewer à página default.aspx.   
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>Para adicionar um controle ReportViewer ao aplicativo  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Default.aspx**e clique em **Designer de Exibição**.  
  
2.  Se default.aspx já tiver o Controle ReportViewer, vá para a **Etapa 4**. Se preferir, no grupo **Extensões AJAX** da janela **Caixa de Ferramentas** , arraste um controle **ScriptManager** até a superfície de design.  
  
3.  No grupo **Relatórios** , arraste um controle **ReportViewer** para a superfície de design abaixo do controle **ScriptManager** .  
  
4.  Abra a janela **Tarefas do ReportViewer** clicando na seta no canto superior direito do controle de **ReportViewer** .  
  
5.  Na caixa **Escolher Relatório** , selecione o relatório pai que você criou.  
  
    Quando você seleciona um relatório, as instâncias das fontes de dados usadas no relatório são criadas automaticamente. O código é gerado para criar uma instância de cada DataTable (e de seu contêiner [DataSet](http://msdn.microsoft.com/library/system.data.dataset.aspx) ). Um controle [ObjectDataSource](http://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx) é adicionado à superfície de design, correspondente a cada fonte de dados usada no relatório. Esse controle do código-fonte é configurado automaticamente.  
  
6.  No menu Criar, clique em Criar site.  
  
    O relatório é compilado e quaisquer erros como um erro de sintaxe em uma expressão de relatório aparecem na área de **Lista de Erros** . Clique em **Lista de Erros** na parte inferior da janela do Visual Studio para exibir a área **Lista de Erros** .  
  
## <a name="next-task"></a>Próxima tarefa  
Você adicionou um controle ReportViewer ao aplicativo de site. Em seguida, você adicionar uma ação de detalhamento ao relatório pai. Consulte [Lição 7: Adicionar ação de detalhamento ao relatório pai](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md).  
  

