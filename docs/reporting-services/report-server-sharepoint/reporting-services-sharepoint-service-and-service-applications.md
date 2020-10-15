---
title: Serviço SharePoint do Reporting Services e aplicativos de serviço | Microsoft Docs
description: A criação de um aplicativo de serviço no modo do SharePoint do SQL Server Reporting Services torna o serviço disponível e gera o banco de dados de aplicativo do serviço.
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 1d1a544f300e6e49e5355294a1e0f99515482113
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934637"
---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Serviço SharePoint do Reporting Services e aplicativos de serviço

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  O modo do SharePoint do Reporting Services foi projetado com base na arquitetura do serviço SharePoint e utiliza um serviço SharePoint e aplicativos de serviço um para muitos. Criar um aplicativo de serviço torna o serviço disponível e gera o banco de dados de aplicativo de serviço. Você pode criar vários aplicativos de serviço Reporting Services, mas um aplicativo de serviço é suficiente para a maioria dos cenários de implantação.  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
## <a name="creating-a-reporting-services-service-application"></a>Criando um aplicativo do serviço Reporting Services

 Use a Administração Central do SharePoint ou scripts do PowerShell para criar aplicativos do serviço Reporting Services. Para obter mais informações sobre como usar a Administração Central do SharePoint, confira a seção "Criar um aplicativo de serviço do Reporting Services" em [Instalar o Reporting Services no modo do SharePoint para SharePoint 2010](../install-windows/install-the-first-report-server-in-sharepoint-mode.md). Consulte a seção PowerShell posteriormente neste tópico para obter um exemplo de script PowerShell para criar aplicativos de serviço.  
  
## <a name="modify-the-associations-of-the-service-application-with-a-proxy-group"></a>Modificar as associações do aplicativo de serviço com um grupo proxy

 A página Nova para criar um aplicativo de serviço contém a seção **Associação de Aplicativo Web**. Esta seção permite a você associar seu aplicativo de serviço conforme criá-lo. Use as etapas a seguir para alterar a associação e atribuir uma configuração de cliente ao aplicativo de serviço. O mesmo processo geral também pode ser usado para adicionar o proxy ao grupo padrão em vez de alterar a associação do aplicativo de serviço com um grupo personalizado.  
  
1.  Na Administração Central do SharePoint, em Gerenciamento de Aplicativo, clique em **Configurar Associações de Aplicativo de Serviço**.  
  
2.  Na página Associações de Aplicativos de Serviço, altere a exibição para **Aplicativos de Serviço**.  
  
3.  Localize e clique no nome do novo aplicativo do Serviço Reporting Services. Você também pode clicar no nome do grupos de proxies de aplicativos **padrão** para adicionar o proxy ao grupo padrão em vez de concluir as etapas a seguir.  
  
4.  Selecione **Personalizado** na caixa de seleção **Editar o seguinte grupo de conexões**.  
  
5.  Marque a caixa do proxy e clique em **Ok**.  
  
## <a name="edit-service-application-properties"></a>Editar as propriedades do aplicativo de serviço

 Você pode reabrir a página de propriedades do aplicativo de serviço para modificar as propriedades.  
  
1.  Na Administração Central do SharePoint, no grupo Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Selecione o aplicativo de serviço clicando na coluna de tipo para selecionar a linha inteira. Se você clicar no nome do aplicativo, a página de opções de Gerenciamento do serviço será aberta em vez das propriedades do aplicativo de serviço.  
  
3.  Na faixa de opções Aplicativos de Serviço, clique em **Propriedades**.  
  
## <a name="create-a-reporting-services-service-application-using-powershell"></a>Criar um aplicativo do serviço Reporting Services usando o PowerShell

 Você pode usar o PowerShell para criar o aplicativo de serviço e o proxy. O exemplo a seguir presume que você saiba qual pool de aplicativos deseja para configurar o aplicativo de serviço a ser usado.  
  
1.  Adicione o objeto do pool de aplicativos do nome do pool de aplicativos a uma variável que será passada para a ação Novo.  
  
    ```  
    $appPoolName = get-spserviceapplicationpool "<application pool name>"  
    ```  
  
2.  Crie o aplicativo de serviço com um nome e um nome de pool de aplicativos fornecidos.  
  
    ```  
    New-SPRSServiceApplication -Name 'MyServiceApplication' -ApplicationPool $appPoolName -DatabaseName 'MyServiceApplicationDatabase' -DatabaseServer '<Server Name>'  
    ```  
  
3.  Obtenha o novo objeto do aplicativo de serviço e redirecione o objeto para o Pipe do novo cmdlet de proxy.  
  
    ```  
    Get-SPRSServiceApplication -name MyServiceApplication | New-SPRSServiceApplicationProxy "MyServiceApplicationProxy"  
    ```  
  
## <a name="related-tasks"></a>Tarefas relacionadas
  
|Tarefa|Link|  
|----------|----------|  
|Gerenciar as configurações de seu aplicativo de serviço.|[Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)|  
|Faça backup e restaure o aplicativo de serviço e os componentes relacionados, como chaves de criptografia e proxy.|[Aplicativos de serviço SharePoint de backup e restauração do Reporting Services](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)