---
title: Importar relatórios do Microsoft Access (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Access reports [Reporting Services]
- importing reports
ms.assetid: 4f29d5b8-b77d-4714-a84a-05523df55646
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 862d8b90f3c91dffda35971677db7fdc231c1b63
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108927"
---
# <a name="import-reports-from-microsoft-access-reporting-services"></a>Importar relatórios do Microsoft Access (Reporting Services)
  No Report Designer, você pode importar relatórios de um [!INCLUDE[msCoName](../includes/msconame-md.md)] banco de dados ou projeto do Access. O Access 2002 ou uma versão posterior deve estar instalado no mesmo computador no qual o Designer de Relatórios está instalado.  
  
 Quando você usar o recurso de importação, todos os relatórios no arquivo de banco de dados ou de projeto serão importados. Se o seu arquivo do Access contiver muitos relatórios, é possível criar um projeto de relatório separado, para o qual importar os relatórios, e abrir os arquivos RDL individuais no projeto de relatório principal. É possível editar os relatórios depois de importá-los para o Designer de Relatórios.  
  
> [!NOTE]  
>  O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não oferece suporte a todos os objetos de relatório do Access. Os itens que não são convertidos são exibidos na janela **lista de tarefas** . Para obter mais informações, consulte [recursos de relatório de acesso com suporte &#40;SSRS&#41;](../../2014/reporting-services/supported-access-report-features-ssrs.md).  
  
### <a name="to-import-reports-from-microsoft-access"></a>Para importar relatórios do Microsoft Access  
  
1.  Abra ou crie um projeto no qual devem ser importados os relatórios.  
  
2.  No menu **projeto** , aponte para **importar relatórios**e clique em **Microsoft Access**. Como alternativa, clique com o botão direito do mouse no projeto no Gerenciador de Soluções, aponte para **importar relatórios**e clique em **Microsoft Access**.  
  
3.  Na caixa de diálogo **abrir** , selecione o banco de dados do Access (. mdb,. accdb) ou o projeto (. adp) que contém os relatórios e clique em **abrir**. Todos os relatórios no banco de dados ou arquivo de projeto são importados e listados na pasta Relatórios do Gerenciador de Soluções.  
  
4.  Verifique a janela de **lista de tarefas** em busca de erros de compilação. Para exibir a janela **lista de tarefas** , abra o menu **Exibir** , aponte para **outras janelas**e clique em **lista de tarefas**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
