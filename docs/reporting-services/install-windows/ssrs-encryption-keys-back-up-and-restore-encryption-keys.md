---
description: Chaves de criptografia do SSRS – Fazer backup e restaurar chaves de criptografia
title: Fazer backup e restaurar as chaves de criptografia do Reporting Services | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- backing up encryption keys [Reporting Services]
- restoring encryption keys [Reporting Services]
- encryption keys [Reporting Services]
- symmetric keys [Reporting Services]
ms.assetid: 6773d5df-03ef-4781-beb7-9f6825bac979
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5da541204707bc3ad3b47a8ade5f1f1af6506ad5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454556"
---
# <a name="ssrs-encryption-keys---back-up-and-restore-encryption-keys"></a>Chaves de criptografia do SSRS – Fazer backup e restaurar chaves de criptografia
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Um parte importante da configuração do servidor de relatório é a criação de uma cópia de backup da chave simétrica usada para criptografar informações confidenciais. Uma cópia de backup da chave é necessária para várias operações rotineiras, possibilitando que você reutilize um banco de dados de servidor de relatório existente em uma nova instalação.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modo do SharePoint para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
 Será necessário restaurar a cópia de backup da chave de criptografia quando ocorrer quaisquer dos seguintes eventos:  
  
-   Alteração do nome da conta de serviço do Windows Servidor de Relatório ou redefinição da senha. Quando você usa o Gerenciador de configurações do Reporting Services, o backup da chave faz parte de uma operação de alteração de nome da conta de serviço.  
  
    > [!NOTE]
    > Redefinir a senha não é o mesmo que alterar a senha. Uma redefinição de senha requer permissão para substituir informações de conta no controlador de domínio. As redefinições de senha são executadas por um administrador de sistema quando você esquecer ou não souber uma senha específica. Somente redefinições de senha requerem a restauração da chave simétrica. A alteração periódica da senha de uma conta não requer a redefinição da chave simétrica.  
  
-   Renomeação do computador ou da instância que hospeda o servidor de relatório (uma instância de servidor de relatório tem como base um nome de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ).  
  
-   Migração de uma instalação do servidor de relatório ou configuração de um servidor de relatório para usar um banco de dados de servidor de relatório diferente.  
  
-   Recuperação de uma instalação do servidor de relatório devido a uma falha de hardware.  
  
 Você precisa fazer o backup somente de uma cópia da chave simétrica. Há uma correspondência um para um entre um banco de dados do servidor de relatório e uma chave simétrica. Embora você precise fazer o backup de uma cópia apenas, poderá ser necessário restaurar a chave várias vezes se você estiver executando vários servidores de relatório em um modelo de implantação de expansão. Cada instância do servidor de relatório precisa de sua cópia da chave simétrica a fim de bloquear e desbloquear dados no banco de dados do servidor de relatório.

 O backup da chave simétrica é um processo que grava a chave em um arquivo especificado e codifica a chave usando uma senha que você fornecer. A chave simétrica nunca pode ser armazenada em um estado não criptografado, portanto você deve fornecer uma senha para codificar a chave ao salvá-la em disco. Depois que o arquivo for criado, você deverá armazená-lo em um local seguro **e lembrar-se da senha** usada para desbloquear o arquivo. Para fazer backup da chave simétrica, você pode usar as seguintes ferramentas:  
  
 **Modo nativo:** Gerenciador de configurações do Reporting Services ou o utilitário **rskeymgmt** .  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
 **O modo do SharePoint:** Páginas do PowerShell ou Administração Central do SharePoint.  
  
##  <a name="backup-sharepoint-mode-report-servers"></a><a name="bkmk_backup_sharepoint"></a> Fazer backup dos servidores de relatório do modo SharePoint  
 Para servidores de relatório do modo do SharePoint, você pode usar os comandos do PowerShell ou as páginas de gerenciamento para o aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, confira a seção “Gerenciamento de chaves” de [Gerenciar um aplicativo de serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  

::: moniker-end
  
##  <a name="back-up-encryption-keys--reporting-services-configuration-manager-native-mode"></a><a name="bkmk_backup_configuration_manager"></a> Fazer backup das chaves de criptografia - Gerenciador de configurações do Reporting Services (Modo Nativo)  
  
1.  Inicie o Gerenciador de Configuração do Servidor de Relatório e conecte-se à instância do servidor de relatório que você deseja configurar.  
  
2.  Clique em **Chaves de Criptografia**e selecione **Fazer Backup**.  
  
3.  Digite uma senha forte.  
  
4.  Especifique um arquivo para conter a chave armazenada. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] acrescenta uma extensão .snk ao arquivo. Considere o armazenamento do arquivo em um disco separado do servidor de relatório.  
  
5.  Selecione **OK**.  
  
###  <a name="back-up-encryption-keys--rskeymgmt-native-mode"></a><a name="bkmk_backup_rskeymgmt"></a> Fazer backup das chaves de criptografia – rskeymgmt (Modo Nativo)  
  
1.  Execute **rskeymgmt.exe** localmente no computador que hospeda o servidor de relatório. É necessário usar o argumento de extração **-e** para copiar a chave, fornecer um nome de arquivo e especificar uma senha. O exemplo a seguir ilustra os argumentos que você deve especificar:  
  
    ```  
    rskeymgmt -e -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="restore-encryption-keys"></a>Restaurar as chaves de criptografia  
 A restauração da chave simétrica substitui a chave simétrica existente que está armazenada no banco de dados do servidor de relatório. A restauração de uma chave de criptografia substitui uma chave inutilizável por uma cópia que você salvou em disco anteriormente. A restauração de chaves de criptografia resulta nas seguintes ações:  
  
-   A chave simétrica é aberta a partir do arquivo de backup protegido por senha.  
  
-   A chave simétrica é criptografada usando-se a chave pública do serviço do Windows Servidor de Relatório.  
  
-   A chave simétrica criptografada é armazenada no banco de dados do servidor de relatório.  
  
-   Os dados da chave simétrica armazenada anteriormente (por exemplo, informações de chave que já estavam no banco de dados do servidor de relatório de uma implantação anterior) serão excluídos.  
  
 Para restaurar a chave de criptografia, você deve ter uma cópia da chave de criptografia em arquivo. Você também deve saber a senha que desbloqueia a cópia armazenada. Se você tiver a chave e a senha, poderá executar a ferramenta Configuração do Reporting Services ou o utilitário **rskeymgmt** para restaurar a chave. A chave simétrica deve ser a mesma que bloqueia e desbloqueia os dados criptografados atualmente armazenados no banco de dados do servidor de relatório. Se você restaurar uma cópia que não seja válida, o servidor de relatório não poderá acessar os dados criptografados atualmente armazenados no banco de dados do servidor de relatório. Se isso ocorrer, poderá ser necessário excluir todos os valores criptografados se você não puder restaurar uma chave válida. Se por alguma razão você não puder restaurar a chave de criptografia (por exemplo, se você não tiver uma cópia de backup), você deverá excluir a chave existente e o conteúdo criptografado. Para obter mais informações, consulte [Excluir e recriar chaves de criptografia &#40; 	Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md). Para obter mais informações sobre como criar chaves simétricas, veja [Inicializar um servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
###  <a name="restore-encryption-keys--reporting-services-configuration-manager-native-mode"></a><a name="bkmk_restore_configuration_manager"></a> Restaurar as chaves de criptografia - Gerenciador de configurações do Reporting Services (Modo Nativo)  
  
1.  Inicie o Gerenciador de configurações do Reporting Services e conecte-se à instância do servidor de relatório que deseja configurar.  
  
2.  Na página Chaves de Criptografia, selecione em **Restaurar**.  
  
3.  Selecione o arquivo .snk que contém a cópia de backup.  
  
4.  Digite a senha que desbloqueia o arquivo.  
  
5.  Selecione **OK**. 
  
###  <a name="restore-encryption-keys---rskeymgmt-native-mode"></a><a name="bkmk_restore_rskeymgmt"></a> Restaurar as chaves de criptografia – rskeymgmt (Modo Nativo)  
  
1.  Execute **rskeymgmt.exe** localmente no computador que hospeda o servidor de relatório. Use o argumento **-a** para restaurar as chaves. Você deve fornecer um nome de arquivo totalmente qualificado e especificar uma senha. O exemplo a seguir ilustra os argumentos que você deve especificar:  
  
    ```  
    rskeymgmt -a -f d:\rsdbkey.snk -p<password>  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
