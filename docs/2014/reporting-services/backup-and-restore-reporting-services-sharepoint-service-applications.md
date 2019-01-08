---
title: Fazer backup e restaurar aplicativos de serviço SharePoint de serviços de emissão de relatórios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: dfb4ed77-90e5-4273-b690-89a945508ed2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 63511e175a98e366bfeb4d02ba3085d8e9943813
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368398"
---
# <a name="backup-and-restore-reporting-services-sharepoint-service-applications"></a>Aplicativos de serviço Sharepoint de backup e restauração do Reporting Services
  Este tópico descreve como fazer backup de um aplicativo de serviços [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e restaurá-lo usando a Administração Central do SharePoint ou o PowerShell. O tópico contém:  
  
-   [Limitações e restrições](#bkmk_Restrictions)  
  
-   [Backup do aplicativo de serviço](#bkmk_backup)  
  
-   [Restaurar o aplicativo de serviço](#bkmk_restore)  
  
##  <a name="bkmk_BeforeYouBegin"></a> Antes de começar  
  
###  <a name="bkmk_Restrictions"></a> Limitações e restrições  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] podem ser parcialmente submetidos a backup e restaurados usando a funcionalidade de backup e restauração do SharePoint. **São necessárias etapas adicionais** e as etapas são documentadas neste tópico. No momento, o processo de backup **não** faz backup das chaves de criptografia e das credenciais para UEAs (contas de execução autônomas) ou autenticação de janelas no banco de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
###  <a name="bkmk_recommendations"></a> Recomendações  
  
-   Faça backup das chave de criptografia antes de iniciar o backup do SharePoint. Se você não fizer backup das chave de criptografia, não poderá acessar os dados criptografados, seguindo a restauração do aplicativo de serviço. Você precisará excluir seus dados criptografados.  
  
-   Verifique se o aplicativo de serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] está usando a UEA ou a autenticação do Windows para acesso ao banco de dados. Se ele estiver usando uma delas, verifique quais são as credenciais apropriadas para que você possa configurar o aplicativo de serviço após o processo de restauração.  
  
-   Verifique se o log de backup do SharePoint foi criado na mesma pasta do arquivo de backup. O arquivo é geralmente nomeado **spbackup.log**  
  
##  <a name="bkmk_backup"></a> Backup do aplicativo de serviço  
 Conclua as seguintes etapas nesta ordem:  
  
1.  Backup das chaves de criptografia  
  
2.  Backup do aplicativo de serviço  
  
3.  Verifique se o aplicativo de serviço usa uma UEA ou uma autenticação do Windows para acesso ao banco de dados. Em caso afirmativo, anote as credenciais a fim de que você possa usá-las para configurar o aplicativo de serviço depois que ele for restaurado.  
  
### <a name="backup-the-encryption-keys-using-central-administration"></a>Backup das chaves de criptografia usando a Administração Central  
 Para obter informações sobre como fazer backup de chaves de criptografia do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], confira a seção "Chaves de criptografia" de [Gerenciar um aplicativo do serviço SharePoint do Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).  
  
###  <a name="bkmk_centraladmin"></a> Backup do aplicativo de serviço usando a Administração Central do SharePoint  
 Para fazer backup do aplicativo de serviço, conclua as seguintes etapas:  
  
1.  Na Administração Central do SharePoint, clique em **Executar um backup** no grupo **Backup e restauração** .  
  
2.  No nó **Serviços Compartilhados** , expanda **Aplicativos de Serviços Compartilhados** e selecione seu aplicativo de serviço. Seu tipo será **Aplicativo de Serviço SQL Server Reporting Services**.  
  
3.  Clique em **Avançar**.  
  
4.  Digite o caminho do **Local do backup:** e clique em **Iniciar Backup**  
  
5.  Repita o processo acima, mas em vez de selecionar o aplicativo de serviço, expanda o nó **Proxies de Serviços Compartilhados** e selecione o proxy do aplicativo de serviço. Seu tipo será **Proxy do Aplicativo de Serviço SQL Server Reporting Services**.  
  
 Para obter mais informações, consulte os seguintes tópicos na documentação do SharePoint:  
  
 [Backup de um aplicativo de serviço (SharePoint Foundation 2010) na documentação do SharePoint](https://msdn.microsoft.com/library/ee748601.aspx).  
  
 [Backup de um aplicativo de serviço (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Verificar conta de execução e autenticação do banco de dados  
 **Conta de execução:** Para verificar se seu aplicativo de serviço está usando uma conta de execução:  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativos** .  
  
2.  Clique no nome do aplicativo de serviço e, em seguida, clique em **Gerenciar** na faixa de opções do SharePoint.  
  
3.  Clique em **Conta de Execução**.  
  
4.  Se uma conta de execução for configurada, você precisará saber as credenciais quando chegar a hora de restaurar o backup do aplicativo de serviço. Não continue com o procedimento de backup e restauração até que saiba as credenciais corretas.  
  
 **Autenticação de banco de dados:** Para verificar se o aplicativo de serviço está usando a Autenticação do Windows para a autenticação do banco de dados:  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativos** .  
  
2.  Clique no nome do aplicativo de serviço e, em seguida, clique em **Propriedades** na faixa de opções do SharePoint.  
  
3.  Leia a seção **Banco de Dados do Serviço SQL Server Reporting Services** .  
  
4.  Se a Autenticação do Windows estiver configurada, você precisará saber as credenciais para que possa configurar o aplicativo de serviço após sua restauração. Não continue com o procedimento de backup e restauração até que saiba as credenciais corretas.  
  
##  <a name="bkmk_restore"></a> Restaurar o aplicativo de serviço  
 Conclua as seguintes etapas nesta ordem:  
  
1.  Restaurar o aplicativo de serviço [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  
  
2.  Restaurar as chaves de criptografia  
  
3.  Se seu aplicativo de serviço estava usando uma conta de execução ou uma autenticação do Windows para acesso ao banco de dados, configure as credenciais.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Restaurar o aplicativo de serviço usando a Administração Central do SharePoint  
  
1.  Na Administração Central do SharePoint, clique em **Restaurar de um backup** no grupo **Backup e Restauração** .  
  
2.  Digite o caminho para o arquivo de backup na caixa **Local do Diretório de Backup** e clique em **Atualizar**.  
  
3.  Selecione o backup de aplicativo de serviço na lista **Componente Superior** e clique **Avançar**.  
  
4.  Selecione o aplicativo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e clique em **Avançar**.  
  
5.  Na seção **Nomes e Senhas de Logon** , digite a senha para o nome de logon. A caixa de nome de logon deve ser preenchida com o logon que o aplicativo de serviço estava usando antes do backup.  
  
6.  Clique em **Iniciar Restauração**.  
  
7.  Repita o processo acima, mas em vez de restaurar o aplicativo de serviço, expanda o nó **Serviços Compartilhados** e selecione o nó **Aplicativos de Serviços Compartilhados** .  
  
 Para obter mais informações, consulte os seguintes tópicos na documentação do SharePoint:  
  
 [Restauração de um aplicativo de serviço (SharePoint Foundation 2010)](https://msdn.microsoft.com/library/ee748615.aspx).  
  
 [Restauração de um aplicativo de serviço (SharePoint Server 2010)](ttp://technet.microsoft.com/library/ee428305.aspx).  
  
### <a name="restore-the-encryption-keys-using-central-administration"></a>Restauração das chaves de criptografia usando a Administração Central  
 Para obter informações sobre como restaurar chaves de criptografia do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], confira a seção "Chaves de criptografia" de [Gerenciar um aplicativo do serviço SharePoint do Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).  
  
### <a name="configure-the-execution-account-and-database-authentication"></a>Configurar a conta de execução e a autenticação do banco de dados  
 **Conta de execução:** Se seu aplicativo de serviço estiver usando uma conta de execução, execute as seguintes etapas para configurá-lo:  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativos** .  
  
2.  Clique no nome do aplicativo de serviço e, em seguida, clique em **Gerenciar** na faixa de opções do SharePoint.  
  
3.  Clique em **Conta de Execução**.  
  
4.  Digite a conta e a senha, e selecione a caixa **Especificar uma Conta de Execução** .  
  
5.  Clique em **OK**.  
  
 **Autenticação de banco de dados:** Se o aplicativo de serviço estiver usando a Autenticação do Windows para autenticação do banco de dados, execute as seguintes etapas:  
  
1.  Na Administração Central do SharePoint, clique em **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativos** .  
  
2.  Clique no nome do aplicativo de serviço e, em seguida, clique em **Propriedades** na faixa de opções do SharePoint.  
  
3.  Leia a seção **Banco de Dados do Serviço SQL Server Reporting Services** .  
  
4.  Selecione **Autenticação do Windows**.  
  
5.  Digite a conta e senha. Selecione **Uso como Credenciais do Windows** , se apropriado.  
  
6.  Clique em **Ok**  
  
  
