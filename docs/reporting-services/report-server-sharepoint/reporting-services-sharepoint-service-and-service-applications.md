---
title: "Reporting Services SharePoint service e aplicativos de serviço | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 3b0351819369c0c17a5f97318b1132c69ec71432
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Serviço de relatório do SharePoint de serviços e aplicativos de serviço

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Modo do SharePoint Services Reporting foi arquitetado com base na arquitetura de serviço do SharePoint e utiliza um serviço do SharePoint e um para muitos aplicativos de serviço. Criar um aplicativo de serviço torna o serviço disponível e gera o banco de dados de aplicativo de serviço. Você pode criar vários aplicativos de serviço Reporting Services, mas um aplicativo de serviço é suficiente para a maioria dos cenários de implantação.  

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.
  
## <a name="creating-a-reporting-services-service-application"></a>Criando um aplicativo de serviço do Reporting Services

 Você pode usar a Administração Central do SharePoint ou scripts do PowerShell para criar os aplicativos de serviços do Reporting Services. Para obter mais informações sobre como usar a Administração Central do SharePoint, consulte a seção "Criar um aplicativo Reporting Services Service" [instalar o Reporting Services SharePoint Mode para SharePoint 2010](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c). Consulte a seção PowerShell posteriormente neste tópico para obter um exemplo de script PowerShell para criar aplicativos de serviço.  
  
## <a name="modify-the-associations-of-the-service-application-with-a-proxy-group"></a>Modificar as associações do aplicativo de serviço com um grupo de proxy

 A página Nova para criar um aplicativo de serviço contém a seção **Associação de Aplicativo Web**. Esta seção permite a você associar seu aplicativo de serviço conforme criá-lo. Use as etapas a seguir para alterar a associação e atribuir uma configuração de cliente ao aplicativo de serviço. O mesmo processo geral também pode ser usado para adicionar o proxy ao grupo padrão em vez de alterar a associação do aplicativo de serviço com um grupo personalizado.  
  
1.  Na Administração Central do SharePoint, em Gerenciamento de Aplicativo, clique em **Configurar Associações de Aplicativo de Serviço**.  
  
2.  Na página Associações de Aplicativos de Serviço, altere a exibição para **Aplicativos de Serviço**.  
  
3.  Localize e clique no nome do seu novo aplicativo de serviço do Reporting Services. Você também pode clicar no nome do grupos de proxies de aplicativos **padrão** para adicionar o proxy ao grupo padrão em vez de concluir as etapas a seguir.  
  
4.  Selecione **Personalizado** na caixa de seleção **Editar o seguinte grupo de conexões**.  
  
5.  Marque a caixa do proxy e clique em **Ok**.  
  
## <a name="edit-service-application-properties"></a>Editar propriedades do aplicativo de serviço

 Você pode reabrir a página de propriedades do aplicativo de serviço para modificar as propriedades.  
  
1.  Na Administração Central do SharePoint, no grupo Gerenciamento de Aplicativo, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Selecione o aplicativo de serviço clicando na coluna de tipo para selecionar a linha inteira. Se você clicar no nome do aplicativo, a página de opções de Gerenciamento do serviço será aberta em vez das propriedades do aplicativo de serviço.  
  
3.  Na faixa de opções Aplicativos de Serviço, clique em **Propriedades**.  
  
## <a name="create-a-reporting-services-service-application-using-powershell"></a>Criar um aplicativo de serviço do Reporting Services usando o PowerShell

 Você pode usar o PowerShell para criar o aplicativo de serviço e o proxy. O exemplo a seguir presume que você saiba qual pool de aplicativos deseja para configurar o aplicativo de serviço a ser usado.  
  
1.  Adicione o objeto do pool de aplicativos do nome do pool de aplicativos a uma variável que será passada para a ação Novo.  
  
    ```  
    $appPoolName = get-spserviceapplicationpool “<application pool name>”  
    ```  
  
2.  Crie o aplicativo de serviço com um nome e um nome de pool de aplicativos fornecidos.  
  
    ```  
    New-SPRSServiceApplication –Name ‘MyServiceApplication’ –ApplicationPool $appPoolName –DatabaseName ‘MyServiceApplicationDatabase’ –DatabaseServer ‘<Server Name>’  
    ```  
  
3.  Obtenha o novo objeto do aplicativo de serviço e redirecione o objeto para o Pipe do novo cmdlet de proxy.  
  
    ```  
    Get-SPRSServiceApplication –name MyServiceApplication | New-SPRSServiceApplicationProxy “MyServiceApplicationProxy”  
    ```  
  
## <a name="related-tasks"></a>Tarefas relacionadas
  
|Tarefa|Link|  
|----------|----------|  
|Gerenciar as configurações de seu aplicativo de serviço.|[Manage a Reporting Services SharePoint Service Application](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)|  
|Faça backup e restaure o aplicativo de serviço e os componentes relacionados, como chaves de criptografia e proxy.|[Aplicativos de serviço SharePoint de backup e restauração do Reporting Services](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
