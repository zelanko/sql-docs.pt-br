---
title: Exemplo de uma configuração de privilégio mínimo para o PowerPivot para SharePoint 2013 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c1e09e6c-52d3-48ab-8c70-818d5d775087
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 147664030dd6e52c4bfaf17efd6fa7aea35d53ae
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782777"
---
# <a name="example-of-a-minimum-privilege-configuration-for-powerpivot-for-sharepoint-2013"></a>Exemplo de uma configuração de privilégios mínimos para o PowerPivot para SharePoint 2013
  Este tópico descreve um exemplo da configuração do PowerPivot para SharePoint 2013 com privilégios mínimos. A configuração utiliza uma conta diferente para cada um dos três componentes e cada conta tem o nível mínimo de privilégios.  
  
## <a name="summary-of-accounts"></a>Resumo de contas  
 O PowerPivot para SharePoint 2013 dá suporte ao uso da conta de serviço de rede para a conta de serviço do Analysis Services. A conta de serviço de rede não é um cenário com suporte com o SharePoint 2010. Para obter mais informações sobre contas de serviço, consulte [Configurar contas de serviço e permissões do Windows](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) (https://msdn.microsoft.com/library/ms143504.aspx).  
  
 A tabela a seguir resume as três contas usadas neste exemplo de uma configuração com privilégios mínimos.  
  
|Escopo|Nome|  
|-----------|----------|  
|Conta do administrador do SharePoint|**SPAdmin**|  
|Conta do farm do SharePoint|**SPFarm**|  
|Conta de serviço do Analysis Services|**SPsvc**|  
  
### <a name="the-sharepoint-administrator-account-spadmin"></a>A conta do administrador do SharePoint (SpAdmin)  
 **SPAdmin** é uma conta de domínio usada para instalar e configurar o farm. É a conta usada para executar o assistente de configuração do SharePoint e a ferramenta de configuração do PowerPivot para SharePoint 2013. a conta de **administrador** é a única conta que exige direitos de administrador local. Antes de executar a ferramenta de configuração do PowerPivot, conceda os privilégios da conta de **administrador** para a instância de banco de dados SQL Server, em que o SharePoint cria o conteúdo e banco de dados de configuração. Para configurar a conta SPAdmin em um cenário de privilégios mínimos, ela deve ser um membro das funções **securityadmin** e **dbcreator**.  
  
### <a name="the-farm-account-spfarm"></a>A conta do farm (SPFarm)  
 **SPFarm** é uma conta de domínio que o serviço de timer do SharePoint e o aplicativo Web para a Administração Central usam para acessar o banco de dados de conteúdo do SharePoint. Esta conta não precisa ser um administrador local. O assistente de configuração do SharePoint concede o privilégio mínimo apropriado no banco de dados do SQL Server de back-end. A configuração de privilégios mínimos do SQL Server é a associação nas funções **securityadmin** e **dbcreator**.  
  
### <a name="the-service-account-for-powerpivot-service-spsvc"></a>A conta de serviço para o serviço PowerPivot (SPsvc)  
 Se um novo farm do SharePoint não estiver configurado antes de você executar a ferramenta de configuração do PowerPivot, por padrão a ferramenta configuração do PowerPivot criará o seguinte:  
  
-   Aplicativo de serviço PowerPivot.  
  
-   Aplicativo de Serviços do Excel.  
  
-   Aplicativo de Repositório Seguro.  
  
 A ferramenta de configuração do PowerPivot configura todos os três aplicativos de serviço no pool de aplicativos padrão. Esse pool de aplicativos normalmente é configurado para ser executado como a conta SPFarm, que tem acesso a vários recursos que uma conta de serviço não necessita. Para tornar o ambiente um ambiente de privilégios mínimos, configure uma nova conta de domínio para ser usada pelo pool de aplicativos e aplicativo Web apropriados.  
  
 **Para criar uma nova conta de domínio SPsvc para ser usada como uma conta de serviço do SharePoint:**  
  
1.  Na administração central do SharePoint, clique em **segurança**.  
  
2.  Clique em **Configurar contas de serviço**  
  
3.  Clique em **registrar nova conta gerenciada**.  
  
 A conta **SPSvc** não tem privilégios de administrador local e SPsvc não terá nenhum privilégio no banco de dados do SharePoint. Os únicos privilégios que o SPsvc exige são direitos administrativos à instância do PowerPivot do Analysis Services.  
  
 **Para configurar o pool de aplicativos apropriado para usar a conta SPsvc:**  
  
1.  Na administração central do SharePoint, clique em **segurança**.  
  
2.  Clique em **Configurar contas de serviço**.  
  
3.  Selecione o pool de aplicativo de serviço usado pelo aplicativo de serviço PowerPivot. Selecione a conta SPSvc.  
  
 **Para conceder acesso ao aplicativo Web com o PowerShell:**  
  
1.  Execute o Shell de Gerenciamento do SharePoint 2013 com privilégios de administrador.  
  
2.  Execute o seguinte código do PowerShell:  
  
    ```powershell
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")
    ```  
