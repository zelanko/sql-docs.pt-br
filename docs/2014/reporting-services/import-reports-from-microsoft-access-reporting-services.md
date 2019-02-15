---
title: Importar relatórios do Microsoft Access (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Access reports [Reporting Services]
- importing reports
ms.assetid: 4f29d5b8-b77d-4714-a84a-05523df55646
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7458de1c7424bf3c5b856c263e5180e33e207f76
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56286344"
---
# <a name="import-reports-from-microsoft-access-reporting-services"></a>Importar relatórios do Microsoft Access (Reporting Services)
  No Designer de relatórios, você pode importar relatórios a partir de um [!INCLUDE[msCoName](../includes/msconame-md.md)] banco de dados ou projeto. O Access 2002 ou uma versão posterior deve estar instalado no mesmo computador no qual o Designer de Relatórios está instalado.  
  
 Quando você usar o recurso de importação, todos os relatórios no arquivo de banco de dados ou de projeto serão importados. Se o seu arquivo do Access contiver muitos relatórios, é possível criar um projeto de relatório separado, para o qual importar os relatórios, e abrir os arquivos RDL individuais no projeto de relatório principal. É possível editar os relatórios depois de importá-los para o Designer de Relatórios.  
  
> [!NOTE]  
>  O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não oferece suporte a todos os objetos de relatório do Access. Itens que não são convertidos são exibidos na **lista de tarefas** janela. Para obter mais informações, consulte [suporte para recursos de relatório de acesso &#40;SSRS&#41;](../../2014/reporting-services/supported-access-report-features-ssrs.md).  
  
### <a name="to-import-reports-from-microsoft-access"></a>Para importar relatórios do Microsoft Access  
  
1.  Abra ou crie um projeto no qual devem ser importados os relatórios.  
  
2.  Sobre o **Project** , aponte para **importar relatórios**e, em seguida, clique em **Microsoft Access**. Como alternativa, clique com botão direito no projeto no Gerenciador de soluções, aponte para **importar relatórios**e, em seguida, clique em **Microsoft Access**.  
  
3.  No **aberto** caixa de diálogo, selecione o banco de dados do Access (. mdb,. accdb) ou um projeto (. adp) que contém os relatórios e, em seguida, clique em **abrir**. Todos os relatórios no banco de dados ou arquivo de projeto são importados e listados na pasta Relatórios do Gerenciador de Soluções.  
  
4.  Verifique as **lista de tarefas** janela para erros de compilação. Para exibir o **lista de tarefas** janela, abra o **exibição** , aponte para **Other Windows**e, em seguida, clique em **lista de tarefas**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
