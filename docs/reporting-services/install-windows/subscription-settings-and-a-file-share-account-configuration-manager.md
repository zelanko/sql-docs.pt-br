---
title: Configurações de assinatura e uma conta de compartilhamento de arquivos (Gerenciador de Configurações) | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
f1_keywords:
- SQL13.rsconfigtool.subscriptionsettings.F1
ms.assetid: fefa7bdb-b5f2-4db7-b91c-b58869279f3c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9e8dfea342f4545313035869f8c2e12367e62aed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651960"
---
# <a name="subscription-settings-and-a-file-share-account-configuration-manager"></a>Configurações de Assinatura e uma Conta de Compartilhamento de Arquivos (Gerenciador de Configurações)
  Use a página **Configurações de Assinatura** do Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para configurar uma conta de compartilhamento de arquivos para servidores de relatório no modo nativo e assinaturas de compartilhamento de arquivos. A conta de compartilhamento de arquivos permite que você use um único conjunto de credenciais em várias assinaturas que enviam relatórios para um compartilhamento de arquivos. Quando for o momento de alterar as credenciais, você configura a alteração da conta de compartilhamento de arquivos e não precisa atualizar cada assinatura individual.  
  
 Existem dois fluxos de trabalho com as assinaturas de compartilhamento de arquivos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Uma novidade do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] é que o seu administrador do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode configurar uma conta única de compartilhamento de arquivos, que é usada para várias assinaturas. Configure **Especificar uma conta de compartilhamento de arquivos**e nas páginas de configuração de assinaturas individuais, os usuários selecionam **Usar conta de compartilhamento de arquivos**.  
  
-   Configure assinaturas individuais com credenciais específicas para o compartilhamento de arquivos de destino.  
  
-   Você também pode combinar as duas abordagens e fazer com que algumas assinaturas de compartilhamento de arquivos usem a conta de compartilhamento de arquivos central, enquanto outras assinaturas usam credenciais específicas.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="specify-a-file-share-account"></a>Especificar uma conta de compartilhamento de arquivos  
 Se essa opção for marcada, você poderá fornecer uma conta a ser usada para acessar compartilhamentos de arquivos por meio do servidor de relatório. Se você configurar a conta de compartilhamento de arquivos, todos os usuários poderão selecionar a conta para qualquer assinatura configurada para enviar relatórios para um compartilhamento de arquivos. Se essa opção não for selecionada, a conta de compartilhamento de arquivos **não** estará disponível nas assinaturas.  
  
 Observe que você precisa verificar se a conta configurada como a conta de compartilhamento de arquivos tem permissões de leitura e gravação para que os usuários de compartilhamentos de arquivos usem para o envio de compartilhamento de arquivos.  
  
 A imagem a seguir é o que os usuários veem em assinaturas configuradas para o envio de compartilhamento de arquivos. A opção **Usar conta de compartilhamento de arquivos** fica desabilitada se uma conta de compartilhamento de arquivos não for configurada.  
  
 ![Conta de compartilhamento de arquivos do Gerenciador do Configurações](../../reporting-services/install-windows/media/ssrs-fileshare-account.png "Conta de compartilhamento de arquivos do Gerenciador do Configurações")  
  
## <a name="prevent-privilege-escalation-or-elevated-privileges"></a>Impedir o escalonamento de privilégios ou privilégios elevados  
  
> [!IMPORTANT]
> O conta de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] controla o envio de assinaturas e interage com a conta usada para assinaturas de compartilhamento de arquivos. Recursos de segurança do Windows restringem combinações de 1) a conta de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e 2) a conta usada para contas de compartilhamento de arquivos. Por exemplo, se uma conta interna do sistema operacional for usada para a conta de compartilhamento de arquivos, a conta de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] deve ser outra conta de serviço com permissões de representação. Se uma conta de compartilhamento de arquivos explícita e uma senha foram configuradas, a conta de compartilhamento de arquivos exigirá o direito de fazer logon no computador que executa o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se a conta de compartilhamento de arquivos não tiver as permissões necessárias, as assinaturas que usam essa conta receberão uma mensagem de erro similar a:  
>   
>  `"Failure writing file {file} : An impersonation error occurred using the security context of the current user."`  
  
## <a name="powershell-sample-to-audit-use-of-the-file-share-account"></a>Exemplo do PowerShell para auditar o uso da conta de compartilhamento de arquivos  
 Execute o seguinte script do Windows PowerShell para listar todas as assinaturas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configuradas para usar a **Conta de compartilhamento de arquivos**. Atualize o `SERVERNAME` para obter um valor apropriado para seu servidor de relatórios.  
  
```  
# get all file share subscriptions using the default file share account  
$extensionNameMatch = "Report Server FileShare"  
$extensionSettingMatch = "DEFAULTCREDENTIALS"  
$valueMatch = "True"  
  
# filter for subscriptions that have a given extension setting  
filter script:extensionSettingFilter  
{  
    # subscription must match the extension name  
    if($_.DeliverySettings.Extension -eq $extensionNameMatch)  
    {  
        # locate the extension parameter of interest  
        ForEach($extensionParameter in $_.DeliverySettings.ParameterValues)  
        {  
            # if the setting has the desired value, return the subscription  
            if($extensionParameter.Name -eq $extensionSettingMatch -and $extensionParameter.Value -eq $valueMatch)  
            {  
                $_  
                break  
            }  
        }  
    }  
}  
  
$rs2010 = New-WebServiceProxy -Uri "https:// SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
  
Write-Host "----- File share subscriptions using the default file share account ----";  
Write-Host "-------------------------------------------------------------------------- ";  
$subscriptions | extensionSettingFilter | select report, owner, status, lastexecuted, description, subscriptionid | format-table -auto  
  
```  
  
 A saída do script é semelhante a:  
  
 `----- File share subscriptions using the default file share account ----`  
  
 `-----------------------------------------------------------------------------------------------------`  
  
 `Report                    Owner          Status   LastExecuted         SubscriptionID`  
  
 `------------------------  -------------- -------- -------------------- ------------------------------------`  
  
 `Aworks_sales_by_territory DOMAIN\UserName Disabled 10/5/2014 1:04:04 PM e843bc2b-023e-45a3-ba23-22f9dc9a0934`  
  
## <a name="see-also"></a>Consulte Também  
 [Entrega de compartilhamento de arquivos no Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)   
 [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)
  
  
