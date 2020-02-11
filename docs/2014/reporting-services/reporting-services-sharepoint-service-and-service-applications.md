---
title: Serviços do Reporting Services SharePoint e aplicativos de serviço | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 501aa9ee-8c13-458c-bf6f-24e00c82681b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93a8092dc9ed731349a1948a74e3950eb32f4f47
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783156"
---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Serviço SharePoint do Reporting Services e aplicativos de serviço
  
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint foi arquitetado com base na arquitetura do serviço do SharePoint e utiliza um serviço do SharePoint e aplicativos de serviço um para muitos. Criar um aplicativo de serviço torna o serviço disponível e gera o banco de dados de aplicativo de serviço. Você pode criar vários aplicativos de serviço Reporting Services, mas um aplicativo de serviço é suficiente para a maioria dos cenários de implantação.  
  
 Este tópico aborda as seguintes informações:  
  
-   [Criando um aplicativo de serviço de Reporting Services](#bkmk_createapp)  
  
-   [Modificar as associações do aplicativo de serviço com um grupo de proxy](#bkmk_associations)  
  
-   [Editar propriedades do aplicativo de serviço](#bkmk_editserviceapplication)  
  
-   [Para criar um aplicativo de serviço de Reporting Services usando o PowerShell](#bkmk_powershell_create_ssrs_serviceapp)  
  
-   [Tarefas relacionadas](#bkmk_related)  
  
##  <a name="bkmk_createapp"></a>Criando um aplicativo de serviço de Reporting Services  
 Você pode usar a Administração Central do SharePoint ou scripts PowerShell para criar aplicativos de serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Para obter mais informações sobre como usar a Administração Central do SharePoint, confira a seção "Criar um aplicativo de serviço do Reporting Services" em [Instalar o Reporting Services no modo do SharePoint para SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md). Consulte a seção PowerShell posteriormente neste tópico para obter um exemplo de script PowerShell para criar aplicativos de serviço.  
  
##  <a name="bkmk_associations"></a>Modificar as associações do aplicativo de serviço com um grupo de proxy  
 A página Nova para criar um aplicativo de serviço contém a seção **Associação de Aplicativo Web**. Esta seção permite a você associar seu aplicativo de serviço conforme criá-lo. Use as etapas a seguir para alterar a associação e atribuir uma configuração de cliente ao aplicativo de serviço. O mesmo processo geral também pode ser usado para adicionar o proxy ao grupo padrão em vez de alterar a associação do aplicativo de serviço com um grupo personalizado.  
  
1.  Na Administração Central do SharePoint, em Gerenciamento de Aplicativo, clique em **Configurar Associações de Aplicativo de Serviço**.  
  
2.  Na página Associações de Aplicativos de Serviço, altere a exibição para **Aplicativos de Serviço**.  
  
3.  Localize e clique no nome do novo aplicativo de serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Você também pode clicar no nome do grupos de proxies de aplicativos **padrão** para adicionar o proxy ao grupo padrão em vez de concluir as etapas a seguir.  
  
4.  Selecione **Personalizado** na caixa de seleção **Editar o seguinte grupo de conexões**.  
  
5.  Marque a caixa do proxy e clique em **Ok**.  
  
##  <a name="bkmk_editserviceapplication"></a>Editar propriedades do aplicativo de serviço  
 Você pode reabrir a página de propriedades do aplicativo de serviço para modificar as propriedades.  
  
1.  Na administração central do SharePoint, no grupo Gerenciamento de aplicativos, clique em **gerenciar aplicativos de serviço**.  
  
2.  Selecione o aplicativo de serviço clicando na coluna de tipo para selecionar a linha inteira. Se você clicar no nome do aplicativo, a página de opções de Gerenciamento do serviço será aberta em vez das propriedades do aplicativo de serviço.  
  
3.  Na faixa de opções Aplicativos de Serviço, clique em **Propriedades**.  
  
##  <a name="bkmk_powershell_create_ssrs_serviceapp"></a>Para criar um aplicativo de serviço de Reporting Services usando o PowerShell  
 Você pode usar o PowerShell para criar o aplicativo de serviço e o proxy. O exemplo a seguir presume que você saiba qual pool de aplicativos deseja para configurar o aplicativo de serviço a ser usado.  
  
1.  Adicione o objeto do pool de aplicativos do nome do pool de aplicativos a uma variável que será passada para a ação Novo.  
  
    ```powershell
    $appPoolName = Get-SPServiceApplicationPool "<application pool name>"  
    ```  
  
2.  Crie o aplicativo de serviço com um nome e um nome de pool de aplicativos fornecidos.  
  
    ```powershell
    New-SPRSServiceApplication -Name 'MyServiceApplication' -ApplicationPool $appPoolName -DatabaseName 'MyServiceApplicationDatabase' -DatabaseServer '<Server Name>'  
    ```  
  
3.  Obtenha o novo objeto do aplicativo de serviço e redirecione o objeto para o Pipe do novo cmdlet de proxy.  
  
    ```powershell
    Get-SPRSServiceApplication -name MyServiceApplication | New-SPRSServiceApplicationProxy "MyServiceApplicationProxy"  
    ```  
  
##  <a name="bkmk_related"></a> Tarefas relacionadas  
  
|Tarefa|Link|  
|----------|----------|  
|Gerenciar as configurações de seu aplicativo de serviço.|[Gerenciar um aplicativo de serviço do SharePoint Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)|  
|Faça backup e restaure o aplicativo de serviço e os componentes relacionados, como chaves de criptografia e proxy.|[Aplicativos de serviço Sharepoint de backup e restauração do Reporting Services](../../2014/reporting-services/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  
