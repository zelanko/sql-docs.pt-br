---
title: 'Lição 9: Compilar e executar o aplicativo | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f52d3f3a-0b09-4b34-9112-0b3655271587
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 321075631a48570a80e8294f992e8ddb17d50bd3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108379"
---
# <a name="lesson-9-build-and-run-the-application"></a>Lição 9: Criar e executar o aplicativo
  Após criar um filtro de dados para a tabela de dados, a próxima etapa será criar e executar o aplicativo de site.  
  
### <a name="to-build-and-run-the-application"></a>Para criar e executar o aplicativo  
  
1.  Pressione **CTRL+F5** para executar a página Default.aspx sem depuração ou pressione F5 para executar a página com depuração.  
  
     Como parte do processo de criação, o relatório é compilado e todos os erros encontrados (por exemplo, um erro de sintaxe em uma expressão usada no relatório) são adicionados à **Lista de Tarefas** , localizada na parte inferior da janela do Visual Studio.  
  
     A página da Web aparece no navegador. O controle ReportViewer exibe o relatório. Você pode usar a barra de ferramentas para navegar pelo relatório, aplicar zoom e exportar o relatório para o Excel.  
  
2.  Passe o mouse sobre qualquer uma das linhas na coluna **Nome** . O cursor do mouse exibirá um símbolo de mão.  
  
3.  Clique em um valor na coluna **Nome** . O relatório filho é mostrado com os dados filtrados correspondentes.  
  
4.  Clique no ícone **Voltar para o relatório pai**na barra de ferramentas **ReportViewer** para retornar ao relatório **Pai** .  
  
     ![SSRS drill-through usando o ReportViewer](../../2014/tutorials/media/ssrs-drillthrough-report.png "ssrs drill-through usando o ReportViewer")  
  
5.  Feche o navegador para sair.  
  
  
