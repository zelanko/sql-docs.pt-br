---
title: 'Lição 6: Adicionar um controle ReportViewer ao aplicativo | Microsoft Docs'
description: Saiba como adicionar um controle ReportViewer ao aplicativo de site depois de criar o relatório filho usando o Assistente de Relatório.
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3a1874b3253136a12973a60e6619e199995b5314
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891546"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>Lição 6: Adicionar um controle ReportViewer ao aplicativo
Depois que você criar o relatório filho usando o Assistente de Relatório, a próxima etapa será adicionar um controle ReportViewer ao aplicativo de site. Se você estiver usando o Site de Relatórios ASP.NET, ele terá adicionado o controle ReportViewer à página default.aspx.   
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>Para adicionar um controle ReportViewer ao aplicativo  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Default.aspx**e clique em **Designer de Exibição**.  
  
2.  Se default.aspx já tiver o Controle ReportViewer, vá para a **Etapa 4**. Se preferir, no grupo **Extensões AJAX** da janela **Caixa de Ferramentas** , arraste um controle **ScriptManager** até a superfície de design.  
  
3.  No grupo **Relatórios** , arraste um controle **ReportViewer** para a superfície de design abaixo do controle **ScriptManager** .  
  
4.  Abra a janela **Tarefas do ReportViewer** clicando na seta no canto superior direito do controle de **ReportViewer** .  
  
5.  Na caixa **Escolher Relatório** , selecione o relatório pai que você criou.  
  
    Quando você seleciona um relatório, as instâncias das fontes de dados usadas no relatório são criadas automaticamente. O código é gerado para criar uma instância de cada DataTable (e de seu contêiner [DataSet](/dotnet/api/system.data.dataset) ). Um controle [ObjectDataSource](/dotnet/api/system.web.ui.webcontrols.objectdatasource) é adicionado à superfície de design, correspondente a cada fonte de dados usada no relatório. Esse controle do código-fonte é configurado automaticamente.  
  
6.  No menu Criar, clique em Criar site.  
  
    O relatório é compilado e quaisquer erros como um erro de sintaxe em uma expressão de relatório aparecem na área de **Lista de Erros** . Clique em **Lista de Erros** na parte inferior da janela do Visual Studio para exibir a área **Lista de Erros** .  
  
## <a name="next-task"></a>Próxima tarefa  
Você adicionou um controle ReportViewer ao aplicativo de site. Em seguida, você adicionar uma ação de detalhamento ao relatório pai. Confira a [Lição 7: Adicionar ação de detalhamento ao relatório pai](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md).  
