---
title: Associar um relatório a uma fonte de dados compartilhada | Microsoft Docs
description: Saiba como associar um relatório a uma fonte de dados compartilhada em um servidor de relatório em execução no modo nativo ou no modo integrado do SharePoint.
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c35e3d48167ecba74f18fa0ed13461a5165cec42
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458918"
---
# <a name="bind-a-report-to-a-shared-data-source-ssrs"></a>Associar um relatório a uma fonte de dados compartilhada (SSRS)
  Em algumas situações, por exemplo, quando você move um relatório de um servidor de teste para um servidor de produção, talvez seja necessário salvar o arquivo no computador local e carregá-lo em um servidor de relatório diferente. Ao carregar o relatório no novo servidor, você precisa associá-lo novamente a uma fonte de dados compartilhados que está armazenada no novo servidor de relatório. Se o relatório não for associado novamente, ele não funcionará corretamente quando for acessado do novo servidor de relatório.  
  
> [!IMPORTANT]  
>  Antes de associar um relatório novamente a uma fonte de dados compartilhada, a fonte de dados já deve existir no servidor de relatório ou na biblioteca do SharePoint. Para obter mais informações sobre fontes de dados, consulte [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
## <a name="to-bind-a-report-to-a-shared-data-source-on-a-report-server-running-in-native-mode"></a>Para associar um relatório a uma fonte de dados compartilhada em um servidor de relatório em execução no modo nativo  
  
1.  No portal da Web, clique nas reticências (...) no canto superior direito do bloco de relatório > **Gerenciar**.  

2.  Clique em **Fontes de Dados**.  
  
3.  Clique em **Uma fonte de dados compartilhada** e navegue até a fonte de dados à qual deseja associar o relatório.  
  
4.  Selecione a fonte de dados e clique em **Salvar**.  
  
5.  Clique em **Aplicar**.  
  
     Agora o relatório está associado à fonte de dados selecionada.  
  
## <a name="to-bind-a-report-to-a-shared-data-source-on-a-report-server-running-in-sharepoint-integrated-mode"></a>Para associar um relatório a uma fonte de dados compartilhada em um servidor de relatório em execução no modo integrado do SharePoint  
  
1.  Se a biblioteca ainda não estiver aberta, clique no nome dela na barra Início Rápido. Se o nome da biblioteca não for exibido, clique em **Exibir Todo o Conteúdo do Site**e, em seguida, clique no nome da biblioteca.  
  
2.  Aponte para o relatório e clique na seta para baixo.  
  
3.  Clique em **Gerenciar Fontes de Dados**.  
  
4.  Clique em **dataSource1**.  
  
5.  Na área **Tipo de Conexão** , verifique se a opção **Fonte de dados compartilhada** está selecionada.  
  
6.  Na área **Vínculo da Fonte de Dados**, clique no botão de reticências (...).  
  
7.  Localize a fonte de dados que deseja usar.  
  
8.  Selecione a fonte de dados e clique em **OK**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Clique em **fechar**  
  
## <a name="see-also"></a>Consulte Também  
 [Carregar documentos em uma biblioteca do SharePoint &#40;Reporting Services no modo do SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)   
 [Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
  
