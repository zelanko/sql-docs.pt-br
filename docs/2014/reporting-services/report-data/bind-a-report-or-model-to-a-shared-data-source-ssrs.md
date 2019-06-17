---
title: Associar um relatório ou modelo a uma fonte de dados compartilhada (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b6d973d4628e9c80b47c4fea0ef3476dbd05131f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107448"
---
# <a name="bind-a-report-or-model-to-a-shared-data-source-ssrs"></a>Associar um relatório ou modelo a uma fonte de dados compartilhada (SSRS)
  Em algumas situações, por exemplo, quando você move um relatório ou modelo de um servidor de teste para um servidor de produção, talvez seja necessário salvar o arquivo no computador local e carregá-lo em um servidor de relatório diferente. Ao carregar o relatório ou modelo no novo servidor, você precisa associá-lo novamente a uma fonte de dados compartilhados que está armazenada no novo servidor de relatório. Se o relatório ou modelo não for associado novamente, ele não funcionará corretamente quando for acessado a partir do novo servidor de relatório.  
  
> [!IMPORTANT]  
>  Antes de associar um relatório ou modelo novamente a uma fonte de dados compartilhada, a fonte de dados já deve existir no servidor de relatório ou na biblioteca do SharePoint. Para obter mais informações sobre fontes de dados, consulte [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md).  
  
### <a name="to-bind-a-report-or-model-to-a-shared-data-source-on-a-report-server-running-in-native-mode"></a>Para associar um relatório ou modelo a uma fonte de dados compartilhada em um servidor de relatório em execução no modo nativo  
  
1.  No **Gerenciador de Relatórios**, clique no nome do relatório ou modelo carregado no servidor.  
  
     A guia Propriedades é exibida.  
  
2.  Clique em **Fontes de Dados**.  
  
3.  Clique em **Procurar**e navegue até a fonte de dados à qual deseja associar o relatório ou modelo.  
  
4.  Selecione a fonte de dados e clique em **OK**.  
  
5.  Clique em **Aplicar**.  
  
     O relatório ou modelo é associado à fonte de dados selecionada.  
  
### <a name="to-bind-a-report-or-model-to-a-shared-data-source-on-a-report-server-running-in-sharepoint-integrated-mode"></a>Para associar um relatório ou modelo a uma fonte de dados compartilhada em um servidor de relatório em execução no modo integrado do SharePoint  
  
1.  Se a biblioteca ainda não estiver aberta, clique no nome dela na barra Início Rápido. Se o nome da biblioteca não for exibido, clique em **Exibir Todo o Conteúdo do Site**e, em seguida, clique no nome da biblioteca.  
  
2.  Aponte para o relatório ou modelo e clique na seta para baixo.  
  
3.  Clique em **Gerenciar Fontes de Dados**.  
  
4.  Clique em **dataSource1**.  
  
5.  Na área **Tipo de Conexão** , verifique se a opção **Fonte de dados compartilhada** está selecionada.  
  
6.  Na área **Vínculo da Fonte de Dados**, clique no botão de reticências (...).  
  
7.  Localize a fonte de dados que deseja usar.  
  
8.  Selecione a fonte de dados e clique em **OK**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Clique em **Fechar**.  
  
## <a name="see-also"></a>Consulte também  
 [Carregar um arquivo ou relatório &#40;Gerenciador de Relatórios&#41;](../reports/upload-a-file-or-report-report-manager.md)   
 [Carregar documentos em uma biblioteca do SharePoint &#40;Reporting Services no modo do SharePoint&#41;](../upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)   
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
