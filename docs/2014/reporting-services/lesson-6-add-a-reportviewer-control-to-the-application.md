---
title: 'Lição 6: Adicionar um controle ReportViewer ao aplicativo | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: afb73e5dc93efdadb0754072d652b7328aaa2151
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103996"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>Lição 6: adicionar um controle ReportViewer ao aplicativo
  Depois que você criar o relatório filho usando o Assistente de Relatório, a próxima etapa será adicionar um controle ReportViewer ao aplicativo de site.  
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>Para adicionar um controle ReportViewer ao aplicativo  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Default.aspx**e clique em **Designer de Exibição**.  
  
2.  No grupo **Extensões AJAX** na janela **Caixa de Ferramentas** , arraste um controle **ScriptManager** à superfície de design.  
  
3.  No grupo **Relatórios** , arraste um controle **ReportViewer** para a superfície de design abaixo do controle **ScriptManager** .  
  
4.  Abra a janela **Tarefas do ReportViewer** clicando na seta no canto superior direito do controle de **ReportViewer** .  
  
5.  Na caixa **Escolher Relatório** , selecione o relatório pai que você criou.  
  
     Quando você seleciona um relatório, as instâncias das fontes de dados usadas no relatório são criadas automaticamente. O código é gerado para criar uma instância de cada DataTable (e de seu contêiner [DataSet](http://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) .) Um controle [ObjectDataSource](http://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource\(v=vs.100\).aspx) é adicionado à superfície de design, correspondente a cada fonte de dados usada no relatório. Esse controle do código-fonte é configurado automaticamente.  
  
     Se você estiver usando o Microsoft Visual Studio 2012, verifique se o controle ObjectDataSource está associado ao DataSet1 totalmente qualificado com o namespace do projeto, caso o nome totalmente qualificado esteja listado na caixa de listagem suspensa **Escolher o objeto comercial** (por exemplo, Projectnamespace.DataSet1TableAdapters.ProductTableAdapter). Acesse a caixa de listagem clicando com o botão direito do mouse em ObjectDataSource e clicando em **Configurar Fonte de Dados**.  
  
6.  No menu Criar, clique em Criar site.  
  
     O relatório é compilado e quaisquer erros como um erro de sintaxe em uma expressão de relatório aparecem na área de **Lista de Erros** . Clique em **Lista de Erros** na parte inferior da janela do Visual Studio para exibir a área **Lista de Erros** .  
  
## <a name="next-task"></a>Próxima tarefa  
 Você adicionou um controle ReportViewer ao aplicativo de site. Em seguida, você adicionar uma ação de detalhamento ao relatório pai.  
  
  
