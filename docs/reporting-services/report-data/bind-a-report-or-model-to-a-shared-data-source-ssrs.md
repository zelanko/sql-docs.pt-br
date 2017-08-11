---
title: "Associar um relatório ou modelo a uma fonte de dados compartilhados (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 50893ee7140f33086d432fdc00f660f6371fe282
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="bind-a-report-or-model-to-a-shared-data-source-ssrs"></a>Associar um relatório ou modelo a uma fonte de dados compartilhada (SSRS)
  Em algumas situações, por exemplo, quando você move um relatório ou modelo de um servidor de teste para um servidor de produção, talvez seja necessário salvar o arquivo no computador local e carregá-lo em um servidor de relatório diferente. Ao carregar o relatório ou modelo no novo servidor, você precisa associá-lo novamente a uma fonte de dados compartilhados que está armazenada no novo servidor de relatório. Se o relatório ou modelo não for associado novamente, ele não funcionará corretamente quando for acessado a partir do novo servidor de relatório.  
  
> [!IMPORTANT]  
>  Antes de associar um relatório ou modelo novamente a uma fonte de dados compartilhada, a fonte de dados já deve existir no servidor de relatório ou na biblioteca do SharePoint. Para obter mais informações sobre fontes de dados, consulte [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
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
  
6.  Na área **Vínculo da Fonte de Dados** , clique no botão de reticências (...).  
  
7.  Localize a fonte de dados que deseja usar.  
  
8.  Selecione a fonte de dados e clique em **OK**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Clique em **Fechar**.  
  
## <a name="see-also"></a>Consulte também  
 [Carregar um arquivo ou relatório &#40; Gerenciador de relatórios &#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)   
 [Carregar documentos em uma biblioteca do SharePoint &#40; Reporting Services no modo do SharePoint &#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [Criar e gerenciar fontes de dados compartilhadas &#40; O Reporting Services no SharePoint integrado modo &#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)   
 [Criar, excluir ou modificar uma fonte de dados &#40; Gerenciador de relatórios &#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Fontes de dados com suporte no Reporting Services &#40; SSRS &#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
  
