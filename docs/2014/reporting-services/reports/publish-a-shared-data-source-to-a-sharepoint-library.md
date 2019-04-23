---
title: Publicar uma fonte de dados compartilhada em uma biblioteca do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], publishing to a SharePoint library
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 966ed425-3ce2-4e76-8237-3c1c977954ae
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3159e4b64f19410222c6f2adbbce1a1d2c8782e4
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59961192"
---
# <a name="publish-a-shared-data-source-to-a-sharepoint-library"></a>Publicar uma fonte de dados compartilhada em uma biblioteca do SharePoint
  Para publicar uma fonte de dados compartilhada em um servidor de relatório executado no modo integrado SharePoint, defina as propriedades do projeto de relatório no Designer de Relatórios. Nas propriedades do projeto, todas as referências a servidores, relatórios e fontes de dados compartilhadas devem ser URLs totalmente qualificadas.  
  
 Você deve ter permissão de **Membro** ou **Proprietário** no site do SharePoint. Para obter mais informações, consulte [Exemplos de URL para itens de relatório publicados em um Servidor de Relatório no modo do SharePoint &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### <a name="to-publish-a-shared-data-source-to-a-sharepoint-site"></a>Para publicar uma fonte de dados compartilhada em um site do SharePoint  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra um projeto do Servidor de Relatório existente ou novo.  
  
2.  No menu **Projeto** , clique em **Propriedades**. A caixa de diálogo _\<project>_**Páginas de Propriedades do**  será exibida.  
  
3.  Escolha a **Configuração** que deseja usar para publicar no site do SharePoint.  
  
4.  Para publicar fontes de dados compartilhadas no seu projeto e substituir as fontes de dados compartilhadas publicadas, defina **OverwriteDataSources** como **True**.  
  
5.  (Opcional) Para **TargetDataSourceFolder**, digite uma URL em uma biblioteca do SharePoint ou pasta de biblioteca. Por exemplo, *http://TestServer/TestSite/Documents/DataSources*.  
  
     Se você não especificar um valor, o valor **TargetReportFolder** será usado.  
  
6.  Para **TargetReportFolder**, digite uma URL em uma biblioteca ou pasta de biblioteca. Por exemplo, http:*//TestServer/TestSite/Documents/Reports*.  
  
7.  Para **TargetServerURL**, digite uma URL em um site de nível superior ou subsite do SharePoint. Se você não especificar um site, o site padrão de nível superior será usado. Por exemplo, http://*nome_do_servidor*, http://*nome_do_servidor*/*site*ou http://*nome_do_servidor*/*site*/*subsite*.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. No Gerenciador de Soluções, clique com o botão direito do mouse na fonte de dados compartilhada que você deseja publicar e, em seguida, clique em **Implantar**. A fonte de dados será publicada no local especificado em **TargetDataSourceFolder**. Erros de implantação são exibidos na janela Saída.  
  
    > [!NOTE]  
    >  Após a publicação de uma fonte de dados compartilhada em um site do SharePoint, a extensão de nome de arquivo será alterada para .rsds. Você pode editar e gerenciar uma fonte de dados compartilhada diretamente no site do SharePoint. Para obter mais informações, consulte [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Consulte também  
 [Publicar um relatório em uma biblioteca do SharePoint](publish-a-report-to-a-sharepoint-library.md)   
 [Exemplos de URL para itens de relatório publicados em um Servidor de Relatório no modo do SharePoint &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Caixa de diálogo Páginas de Propriedades do Projeto](../tools/project-property-pages-dialog-box.md)   
 [Definir propriedades de implantação &#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md)   
 [Publicando relatórios em um servidor de relatórios](publishing-reports-to-a-report-server.md)   
 [Usar uma conexão de dados do Office &#40;.odc&#41; com relatórios &#40;Reporting Services no modo integrado do SharePoint&#41;](../report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
