---
title: "Power Pivot privilégios mínimos exemplo - do SharePoint 2013 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1e09e6c-52d3-48ab-8c70-818d5d775087
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9583847e375cf3deb030319dce8b77dab3e5e609
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="power-pivot-minimum-privilege-example---sharepoint-2013"></a>Power Pivot privilégios mínimos exemplo - do SharePoint 2013
  Este tópico descreve um exemplo da configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013 com privilégios mínimos. A configuração utiliza uma conta diferente para cada um dos três componentes e cada conta tem o nível mínimo de privilégios.  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013|  
  
## <a name="summary-of-accounts"></a>Resumo de contas  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013 dá suporte ao uso da conta de serviço de rede para a conta de serviço do Analysis Services. A conta de serviço de rede não é um cenário com suporte com o SharePoint 2010. Para obter mais informações sobre contas de serviço, veja [Configurar contas de serviço e permissões do Windows](http://msdn.microsoft.com/library/ms143504.aspx) (http://msdn.microsoft.com/library/ms143504.aspx).  
  
 A tabela a seguir resume as três contas usadas neste exemplo de uma configuração com privilégios mínimos.  
  
|Escopo|Nome|  
|-----------|----------|  
|Conta do administrador do SharePoint|**SPAdmin**|  
|Conta do farm do SharePoint|**SPFarm**|  
|Conta de serviço do Analysis Services|**SPsvc**|  
  
### <a name="the-sharepoint-administrator-account-spadmin"></a>A conta do administrador do SharePoint (SpAdmin)  
 **SPAdmin** é uma conta de domínio usada para instalar e configurar o farm. É a conta usada para executar o Assistente de Configuração do SharePoint e a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013. A conta **SPAdmin** é a única conta que exige direitos de administrador local. Antes de executar a ferramenta de Configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , conceda os privilégios de conta **SPAdmin** à instância do banco de dados do SQL Server em que o SharePoint cria bancos de dados de conteúdo e configuração. Para configurar a conta SPAdmin em um cenário de privilégios mínimos, ela deve ser um membro das funções **securityadmin** e **dbcreator**.  
  
### <a name="the-farm-account-spfarm"></a>A conta do farm (SPFarm)  
 **SPFarm** é uma conta de domínio que o serviço de timer do SharePoint e o aplicativo Web para a Administração Central usam para acessar o banco de dados de conteúdo do SharePoint. Esta conta não precisa ser um administrador local. O assistente de configuração do SharePoint concede o privilégio mínimo apropriado no banco de dados do SQL Server de back-end. A configuração de privilégios mínimos do SQL Server é a associação nas funções **securityadmin** e **dbcreator**.  
  
### <a name="the-service-account-for-power-pivot-service-spsvc"></a>A conta de serviço para o serviço Power Pivot (SPsvc)  
 Se um novo farm do SharePoint não estiver configurado antes de você executar a ferramenta de configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , por padrão a ferramenta configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] criará o seguinte:  
  
-   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
-   Aplicativo de Serviços do Excel.  
  
-   Aplicativo de Repositório Seguro.  
  
 A ferramenta de configuração do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] configura todos os três aplicativos de serviço no pool de aplicativos padrão. Esse pool de aplicativos normalmente é configurado para ser executado como a conta SPFarm, que tem acesso a vários recursos que uma conta de serviço não necessita. Para tornar o ambiente um ambiente de privilégios mínimos, configure uma nova conta de domínio para ser usada pelo pool de aplicativos e aplicativo Web apropriados.  
  
 **Para criar uma nova conta de domínio SPsvc para ser usada como uma conta de serviço do SharePoint:**  
  
1.  Na Administração Central do SharePoint, selecione **Segurança**.  
  
2.  Selecione **Configurar Contas de Serviço**  
  
3.  Selecione **Registrar nova conta gerenciada**.  
  
 A conta **SPSvc** não tem privilégios de administrador local e SPsvc não terá nenhum privilégio no banco de dados do SharePoint. Os únicos privilégios que o SPsvc exige são direitos administrativos à instância do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] do Analysis Services.  
  
 **Para configurar o pool de aplicativos apropriado para usar a conta SPsvc:**  
  
1.  Na Administração Central do SharePoint, selecione **Segurança**.  
  
2.  Selecione **Configurar Contas de Serviço**.  
  
3.  Selecione o pool de aplicativo de serviço usado pelo aplicativo de serviço do [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Selecione a conta SPSvc.  
  
 **Para conceder acesso ao aplicativo Web com o PowerShell:**  
  
1.  Execute o Shell de Gerenciamento do SharePoint 2013 com privilégios de administrador.  
  
2.  Execute o seguinte código do PowerShell:  
  
    ```  
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")  
  
    ```  
  
  

