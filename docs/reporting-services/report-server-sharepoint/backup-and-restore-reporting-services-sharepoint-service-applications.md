---
title: "Fazer backup e restaurar aplicativos de serviço do SharePoint do Reporting Services | Microsoft Docs"
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: b6dcd64d6f9662ae592474053e6cc9bbce53a83e
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>Fazer backup e restaurar aplicativos de serviço do SharePoint do Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Este tópico descreve como fazer backup e restaurar um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativo services usando a Administração Central do SharePoint ou PowerShell.

> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

## <a name="before-you-begin"></a>Antes de começar

### <a name="limitations-and-restrictions"></a>Limitações e restrições

> [!NOTE]
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]aplicativos de serviço parcialmente podem ser feitos backup e restaurados usando o SharePoint de backup e restaurar a funcionalidade. **São necessárias etapas adicionais** e as etapas são documentadas neste tópico. Atualmente o processo de backup **não** fazer backup de chaves de criptografia e credenciais de contas de execução autônoma (UEA) ou autenticação do windows para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] banco de dados.

### <a name="recommendations"></a>Recomendações
  
-   Fazer backup das chaves de criptografia antes de iniciar o backup do SharePoint. Se você não fizer backup das chaves de criptografia, em seguida, você não poderá acessar os dados criptografados, após a restauração do aplicativo de serviço. Você precisará excluir seus dados criptografados.  
  
-   Verifique se o aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando a UEA ou a autenticação do Windows para acesso ao banco de dados. Se ele estiver usando uma delas, verifique quais são as credenciais apropriadas para que você possa configurar o aplicativo de serviço após o processo de restauração.  
  
-   Examine se o log de backup do SharePoint é criado na mesma pasta que o arquivo de backup. O arquivo é geralmente nomeado **spbackup.log**  
  
## <a name="back-up-the-service-application"></a>Fazer backup do aplicativo de serviço

 Conclua as seguintes etapas nesta ordem:  
  
1.  Fazer backup das chaves de criptografia  
  
2.  Fazer backup do aplicativo de serviço  
  
3.  Verifique se o aplicativo de serviço usa uma UEA ou uma autenticação do Windows para acesso ao banco de dados. Em caso afirmativo, anote as credenciais a fim de que você possa usá-las para configurar o aplicativo de serviço depois que ele for restaurado.  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>Fazer backup das chaves de criptografia usando a Administração Central do SharePoint

Para obter informações sobre como fazer backup de chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte a seção "Chaves de criptografia" de [Gerenciar um aplicativo do serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>Fazer backup do aplicativo de serviço usando a Administração Central do SharePoint

Para fazer backup do aplicativo de serviço, conclua as seguintes etapas:  
  
1.  No, selecione Administração Central do SharePoint **executar um backup** no **de Backup e restauração** grupo.  
  
2.  No nó **Serviços Compartilhados** , expanda **Aplicativos de Serviços Compartilhados** e selecione seu aplicativo de serviço. Seu tipo será **Aplicativo de Serviço SQL Server Reporting Services**.  
  
3.  Selecione **Avançar**.  
  
4.  Digite o caminho para o **local do Backup:** e selecione **iniciar Backup**  
  
5.  Repita o processo acima, mas em vez de selecionar o aplicativo de serviço, expanda o nó **Proxies de Serviços Compartilhados** e selecione o proxy do aplicativo de serviço. Seu tipo será **Proxy do Aplicativo de Serviço SQL Server Reporting Services**.  
  
 Para obter mais informações, consulte os seguintes tópicos na documentação do SharePoint:  
  
 [Backup de um aplicativo de serviço (SharePoint Foundation 2010) na documentação do SharePoint](http://msdn.microsoft.com/library/ee748601.aspx).  
  
 [Backup de um aplicativo de serviço (SharePoint Server 2010)](http://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Verifique se a autenticação de banco de dados e a conta de execução

 **Conta de Execução:** Para verificar se seu aplicativo de serviço está usando uma conta de execução:  
  
1.  Na Administração Central do SharePoint, selecione **gerenciar aplicativos de serviço** no **gerenciamento de aplicativos** grupo.  
  
2.  Selecione o nome do seu aplicativo de serviço e, em seguida, selecione **gerenciar** na faixa de opções do SharePoint.  
  
3.  Selecione **conta de execução**.  
  
4.  Se uma conta de execução for configurada, você precisará saber as credenciais quando chegar a hora de restaurar o backup do aplicativo de serviço. Não continue com o procedimento de backup e restauração até que saiba as credenciais corretas.  
  
 **Autenticação de Banco de Dados:** Para verificar se o aplicativo de serviço está usando a Autenticação do Windows na autenticação do banco de dados:  
  
1.  Na Administração Central do SharePoint, selecione **gerenciar aplicativos de serviço** no **gerenciamento de aplicativos** grupo.  
  
2.  Selecione o nome do seu aplicativo de serviço e, em seguida, selecione **propriedades** na faixa de opções do SharePoint.  
  
3.  Leia a seção **Banco de Dados do Serviço SQL Server Reporting Services** .  
  
4.  Se a Autenticação do Windows estiver configurada, você precisará saber as credenciais para que possa configurar o aplicativo de serviço após sua restauração. Não continue com o procedimento de backup e restauração até que saiba as credenciais corretas.  
  
## <a name="restore-the-service-application"></a>Restaurar o aplicativo de serviço

 Conclua as seguintes etapas nesta ordem:  
  
1.  Restaurar o aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
2.  Restaurar as chaves de criptografia  
  
3.  Se seu aplicativo de serviço estava usando uma conta de execução ou uma autenticação do Windows para acesso ao banco de dados, configure as credenciais.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Restaurar o aplicativo de serviço usando a Administração Central do SharePoint
  
1.  No, selecione Administração Central do SharePoint **restaurar de um backup** no **de Backup e restauração** grupo.  
  
2.  Digite o caminho para o arquivo de backup em **Backup local do diretório** caixa e selecione **atualizar**.  
  
3.  Selecione o backup do aplicativo de serviço do **componente superior** e, em seguida, selecione **próximo**.  
  
4.  Selecione seu [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicativo e, em seguida, selecione **próximo**.  
  
5.  Na seção **Nomes e Senhas de Logon** , digite a senha para o nome de logon. A caixa de nome de logon deve ser preenchida com o logon que o aplicativo de serviço estava usando antes de fazer backup.  
  
6.  Selecione **Iniciar restauração**.  
  
7.  Repita o processo acima, mas em vez de restaurar o aplicativo de serviço, expanda o nó **Serviços Compartilhados** e selecione o nó **Aplicativos de Serviços Compartilhados** .  
  
 Para obter mais informações, consulte os seguintes tópicos na documentação do SharePoint:  
  
 [Restauração de um aplicativo de serviço (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748615.aspx).  
  
 [Restauração de um aplicativo de serviço (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx).  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>Restaurar as chaves de criptografia usando a Administração Central do SharePoint

 Para obter informações sobre como restaurar chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte a seção "Chaves de criptografia" de [Gerenciar um aplicativo do serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="configure-the-execution-account-and-database-authentication"></a>Configurar a autenticação de banco de dados e a conta de execução

 **Conta de execução:** Se seu aplicativo de serviço estiver usando uma conta de execução, execute as seguintes etapas para configurá-lo:  
  
1.  Na Administração Central do SharePoint, selecione **gerenciar aplicativos de serviço** no **gerenciamento de aplicativos** grupo.  
  
2.  Selecione o nome do seu aplicativo de serviço e, em seguida, selecione **gerenciar** na faixa de opções do SharePoint.  
  
3.  Selecione **conta de execução**.  
  
4.  Digite a conta e a senha, e selecione a caixa **Especificar uma Conta de Execução** .  
  
5.  Escolha **OK**.  
  
 **Autenticação de Banco de Dados:** Se o aplicativo de serviço estiver usando a Autenticação do Windows na autenticação do banco de dados, execute as seguintes etapas:  
  
1.  No, selecione Administração Central do SharePoint **gerenciar aplicativos de serviço** no **gerenciamento de aplicativos** grupo.  
  
2.  Selecione o nome do seu aplicativo de serviço e, em seguida, selecione **propriedades** na faixa de opções do SharePoint.  
  
3.  Leia a seção **Banco de Dados do Serviço SQL Server Reporting Services** .  
  
4.  Selecione **Autenticação do Windows**.  
  
5.  Digite a conta e senha. Selecione **Uso como Credenciais do Windows** , se apropriado.  
  
6.  Selecione **Okey**

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)

