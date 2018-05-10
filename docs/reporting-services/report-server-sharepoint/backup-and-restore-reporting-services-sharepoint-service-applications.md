---
title: Fazer backup e restaurar aplicativos de serviço SharePoint do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 09da0857743d49cb90a074c95190dd8809e7efbb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>Fazer backup e restaurar aplicativos de serviço SharePoint do Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Este tópico descreve como fazer backup de um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e restaurá-lo usando a Administração Central do SharePoint ou o PowerShell.

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

## <a name="before-you-begin"></a>Antes de começar

### <a name="limitations-and-restrictions"></a>Limitações e restrições

> [!NOTE]
>  Os aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser parcialmente copiados em backup e restaurados usando a funcionalidade de backup e restauração do SharePoint. **São necessárias etapas adicionais** e as etapas são documentadas neste tópico. No momento, o processo de backup **não** faz backup das chaves de criptografia e credenciais para UEAs (contas de execução autônomas) ou a autenticação do Windows no banco de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

### <a name="recommendations"></a>Recomendações
  
-   Faça backup das chaves de criptografia antes de iniciar o backup do SharePoint. Se você não fizer backup das chaves de criptografia, não poderá acessar os dados criptografados, após a restauração do aplicativo de serviço. Você precisará excluir seus dados criptografados.  
  
-   Verifique se o aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando a UEA ou a autenticação do Windows para acesso ao banco de dados. Se ele estiver usando uma delas, verifique quais são as credenciais apropriadas para que você possa configurar o aplicativo de serviço após o processo de restauração.  
  
-   Verifique se o log de backup do SharePoint foi criado na mesma pasta do arquivo de backup. O arquivo é geralmente nomeado **spbackup.log**  
  
## <a name="back-up-the-service-application"></a>Fazer backup do aplicativo de serviço

 Conclua as seguintes etapas nesta ordem:  
  
1.  Fazer backup das chaves de criptografia  
  
2.  Fazer backup do aplicativo de serviço  
  
3.  Verifique se o aplicativo de serviço usa uma UEA ou uma autenticação do Windows para acesso ao banco de dados. Em caso afirmativo, anote as credenciais a fim de que você possa usá-las para configurar o aplicativo de serviço depois que ele for restaurado.  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>Fazer backup das chaves de criptografia usando a Administração Central do SharePoint

Para obter informações sobre como fazer backup de chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte a seção "Chaves de criptografia" de [Gerenciar um aplicativo do serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>Fazer backup do aplicativo de serviço usando a Administração Central do SharePoint

Para fazer backup do aplicativo de serviço, conclua as seguintes etapas:  
  
1.  Na Administração Central do SharePoint, selecione **Executar um backup** no grupo **Backup e Restauração**.  
  
2.  No nó **Serviços Compartilhados** , expanda **Aplicativos de Serviços Compartilhados** e selecione seu aplicativo de serviço. Seu tipo será **Aplicativo de Serviço SQL Server Reporting Services**.  
  
3.  Selecione **Avançar**.  
  
4.  Digite o caminho do **Local do backup:** e selecione **Iniciar Backup**  
  
5.  Repita o processo acima, mas em vez de selecionar o aplicativo de serviço, expanda o nó **Proxies de Serviços Compartilhados** e selecione o proxy do aplicativo de serviço. Seu tipo será **Proxy do Aplicativo de Serviço SQL Server Reporting Services**.  
  
 Para obter mais informações, consulte os seguintes tópicos na documentação do SharePoint:  
  
 [Backup de um aplicativo de serviço (SharePoint Foundation 2010) na documentação do SharePoint](http://msdn.microsoft.com/library/ee748601.aspx).  
  
 [Backup de um aplicativo de serviço (SharePoint Server 2010)](http://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Verificar conta de execução e autenticação do banco de dados

 **Conta de Execução:** Para verificar se seu aplicativo de serviço está usando uma conta de execução:  
  
1.  Na Administração Central do SharePoint, selecione **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativo**.  
  
2.  Selecione o nome do aplicativo de serviço e, em seguida, **Gerenciar** na Faixa de Opções do SharePoint.  
  
3.  Selecione **Conta de Execução**.  
  
4.  Se uma conta de execução for configurada, você precisará saber as credenciais quando chegar a hora de restaurar o backup do aplicativo de serviço. Não continue com o procedimento de backup e restauração até que saiba as credenciais corretas.  
  
 **Autenticação de Banco de Dados:** Para verificar se o aplicativo de serviço está usando a Autenticação do Windows na autenticação do banco de dados:  
  
1.  Na Administração Central do SharePoint, selecione **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativo**.  
  
2.  Selecione o nome do aplicativo de serviço e, em seguida, **Propriedades** na Faixa de Opções do SharePoint.  
  
3.  Leia a seção **Banco de Dados do Serviço SQL Server Reporting Services** .  
  
4.  Se a Autenticação do Windows estiver configurada, você precisará saber as credenciais para que possa configurar o aplicativo de serviço após sua restauração. Não continue com o procedimento de backup e restauração até que saiba as credenciais corretas.  
  
## <a name="restore-the-service-application"></a>Restaurar o aplicativo de serviço

 Conclua as seguintes etapas nesta ordem:  
  
1.  Restaurar o aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
2.  Restaurar as chaves de criptografia  
  
3.  Se seu aplicativo de serviço estava usando uma conta de execução ou uma autenticação do Windows para acesso ao banco de dados, configure as credenciais.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Restaurar o aplicativo de serviço usando a Administração Central do SharePoint
  
1.  Na Administração Central do SharePoint, selecione **Restaurar de um backup** no grupo **Backup e Restauração**.  
  
2.  Digite o caminho para o arquivo de backup na caixa **Local do Diretório de Backup** e selecione **Atualizar**.  
  
3.  Selecione o backup do aplicativo de serviço na lista **Componente Superior** e, em seguida, selecione **Avançar**.  
  
4.  Selecione o aplicativo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e, em seguida, **Avançar**.  
  
5.  Na seção **Nomes e Senhas de Logon** , digite a senha para o nome de logon. A caixa de nome de logon deve ser populada com o logon que o aplicativo de serviço estava usando antes do backup.  
  
6.  Selecione **Iniciar Restauração**.  
  
7.  Repita o processo acima, mas em vez de restaurar o aplicativo de serviço, expanda o nó **Serviços Compartilhados** e selecione o nó **Aplicativos de Serviços Compartilhados** .  
  
 Para obter mais informações, consulte os seguintes tópicos na documentação do SharePoint:  
  
 [Restauração de um aplicativo de serviço (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748615.aspx).  
  
 [Restauração de um aplicativo de serviço (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx).  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>Restaurar as chaves de criptografia usando a Administração Central do SharePoint

 Para obter informações sobre como restaurar chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte a seção "Chaves de criptografia" de [Gerenciar um aplicativo do serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="configure-the-execution-account-and-database-authentication"></a>Configurar a conta de execução e a autenticação do banco de dados

 **Conta de execução:** Se seu aplicativo de serviço estiver usando uma conta de execução, execute as seguintes etapas para configurá-lo:  
  
1.  Na Administração Central do SharePoint, selecione **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativo**.  
  
2.  Selecione o nome do aplicativo de serviço e, em seguida, **Gerenciar** na Faixa de Opções do SharePoint.  
  
3.  Selecione **Conta de Execução**.  
  
4.  Digite a conta e a senha, e selecione a caixa **Especificar uma Conta de Execução** .  
  
5.  Escolha **OK**.  
  
 **Autenticação de Banco de Dados:** Se o aplicativo de serviço estiver usando a Autenticação do Windows na autenticação do banco de dados, execute as seguintes etapas:  
  
1.  Na Administração Central do SharePoint, selecione **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativo**.  
  
2.  Selecione o nome do aplicativo de serviço e, em seguida, **Propriedades** na Faixa de Opções do SharePoint.  
  
3.  Leia a seção **Banco de Dados do Serviço SQL Server Reporting Services** .  
  
4.  Selecione **Autenticação do Windows**.  
  
5.  Digite a conta e senha. Selecione **Uso como Credenciais do Windows** , se apropriado.  
  
6.  Selecione **OK**

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
