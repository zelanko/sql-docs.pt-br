---
title: 'Lição 9: Criar e executar o aplicativo | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f52d3f3a-0b09-4b34-9112-0b3655271587
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: fdb619e98fe28742ac6b96acc6419513addfae25
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008847"
---
# <a name="lesson-9-build-and-run-the-application"></a>Lesson 9: Build and Run the Application
  Após criar um filtro de dados para a tabela de dados, a próxima etapa será criar e executar o aplicativo de site.  
  
### <a name="to-build-and-run-the-application"></a>Para criar e executar o aplicativo  
  
1.  Pressione **CTRL+F5** para executar a página Default.aspx sem depuração ou pressione F5 para executar a página com depuração.  
  
     Como parte do processo de criação, o relatório é compilado e todos os erros encontrados (por exemplo, um erro de sintaxe em uma expressão usada no relatório) são adicionados à **Lista de Tarefas** , localizada na parte inferior da janela do Visual Studio.  
  
     A página da Web aparece no navegador. O controle ReportViewer exibe o relatório. Você pode usar a barra de ferramentas para navegar pelo relatório, aplicar zoom e exportar o relatório para o Excel.  
  
2.  Passe o mouse sobre qualquer uma das linhas na coluna **Nome** . O cursor do mouse exibirá um símbolo de mão.  
  
3.  Clique em um valor na coluna **Nome** . O relatório filho é mostrado com os dados filtrados correspondentes.  
  
4.  Clique no ícone **Voltar para o relatório pai**na barra de ferramentas **ReportViewer** para retornar ao relatório **Pai** .  
  
     ![SSRS Detalhar usando o ReportViewer](../../2014/tutorials/media/ssrs-drillthrough-report.png "ssrs Detalhar usando o ReportViewer")  
  
5.  Feche o navegador para sair.  
  
  