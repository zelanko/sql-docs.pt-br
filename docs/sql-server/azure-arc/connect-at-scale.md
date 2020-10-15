---
title: Conectar as instâncias do SQL Server com o Azure Arc em escala
titleSuffix: ''
description: Neste artigo, você aprenderá a conectar instâncias do SQL Server como SQL Servers habilitados para o Azure Arc (versão prévia) usando uma entidade de serviço.
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 36d4581756cd89e016658f8e415aaec6fbe9a35b
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988002"
---
# <a name="connect-sql-server-instances-to-azure-arc-at-scale"></a>Conectar as instâncias do SQL Server com o Azure Arc em escala

Você pode conectar várias instâncias do SQL Server instaladas em vários computadores Windows ou Linux ao Azure Arc usando o mesmo [script gerado para um único computador](connect.md). O script se conectará a cada computador e registrará o computador e as instâncias do SQL Server instaladas nele no Azure Arc. Para obter a melhor experiência possível, é recomendado usar uma [entidade de serviço](/azure/active-directory/develop/app-objects-and-service-principals) do Azure Active Directory. Uma entidade de serviço é uma identidade de gerenciamento limitada especial que recebe apenas a permissão mínima necessária para conectar computadores ao Azure e criar os recursos do Azure para o servidor habilitado para o Azure Arc e o SQL Server habilitado para o Azure Arc. Isso é mais seguro do que usar uma conta com privilégios maiores como um Administrador de Locatários e segue nossas melhores práticas de segurança de controle de acesso.  

Os métodos de instalação e configuração do agente do Connected Machine requerem que o método automatizado usado tenha permissões de administrador nos computadores. No Linux, usando a conta raiz, e no Windows, como membro do grupo de Administradores Locais.

Antes de começar, examine os [pré-requisitos](overview.md#prerequisites) e crie uma função personalizada que atenda às permissões necessárias.

## <a name="connecting-multiple-sql-server-instances-on-windows-using-azure-powershell"></a>Como conectar várias instâncias do SQL Server no Windows usando o Azure PowerShell

Cada computador precisa ter o [Azure PowerShell](/powershell/azure/install-az-ps) instalado.

1. Crie a entidade de serviço usando o PowerShell com o cmdlet [`New-AzADServicePrincipal`](/powershell/module/az.resources/new-azadserviceprincipal). Armazene a saída em uma variável. Caso contrário, você não poderá recuperar a senha necessária mais tarde.

    ```azurepowershell-interactive
    $sp = New-AzADServicePrincipal -DisplayName "Arc-for-servers" -Role <your custom role>
    $sp
    ```

    ```output
    Secret                : System.Security.SecureString
    ServicePrincipalNames : {ad9bcd79-be9c-45ab-abd8-80ca1654a7d1, https://Arc-for-servers}
    ApplicationId         : ad9bcd79-be9c-45ab-abd8-80ca1654a7d1
    ObjectType            : ServicePrincipal
    DisplayName           : Hybrid-RP
    Id                    : 5be92c87-01c4-42f5-bade-c1c10af87758
    Type                  :
    ```

   > [!NOTE]
   > Quando você cria uma entidade de serviço, sua conta deve ser um Proprietário ou Administrador de Acesso de Usuário na assinatura que deseja usar para integração. Se você não tiver permissões suficientes para criar atribuições de função, a entidade de serviço poderá ser criada, mas não poderá integrar computadores. As instruções de como criar uma função personalizada são fornecidas em [Permissões necessárias](overview.md#required-permissions).

2. Recupere a senha armazenada na variável `$sp`:

   ```azurepowershell-interactive
   $credential = New-Object pscredential -ArgumentList "temp", $sp.Secret
   $credential.GetNetworkCredential().password
   ```
3. Recupere o valor da ID do locatário da entidade de serviço:
 
   ```azurepowershell-interactive
   $tenantId= (Get-AzContext).Tenant.Id
   ```
4. Copie e salve os valores da senha, da ID do aplicativo e da ID do locatário usando as práticas de segurança apropriadas. Se você esquecer ou perder a senha da entidade de serviço, poderá redefini-la usando o cmdlet [`New-AzADSpCredential`](/powershell/module/azurerm.resources/new-azurermadspcredential).

   > [!NOTE]
   > Observe que, no momento, o Azure Arc para servidores não dá suporte à entrada com um certificado, portanto, a entidade de serviço precisa usar um segredo para autenticar-se.

5. Baixe o script do PowerShell no portal seguindo as instruções em [Conectar o SQL Server com o Azure Arc](connect.md).

6. Abra o script em uma instância de administrador do ISE do PowerShell e substitua as variáveis de ambiente a seguir usando os valores gerados durante o provisionamento da entidade de serviço já descrito. Essas variáveis estão vazias inicialmente.

   ```azurepowershell-interactive
   $servicePrincipalAppId="{serviceprincipalAppID}"
   $servicePrincipalSecret="{serviceprincipalPassword}"
   $servicePrincipalTenantId="{serviceprincipalTenantId}"
   ```

7. Executar o script em cada computador de destino

## <a name="connecting-multiple-sql-server-instances-on-linux-using-azure-cli"></a>Como conectar várias instâncias do SQL Server no Linux usando a CLI do Azure

Cada computador de destino precisa ter a [CLI do Azure instalada](/cli/azure/install-azure-cli). O script de registro entrará automaticamente no Azure com as credenciais da entidade de serviço se elas tiverem sido fornecidas e se não houver nenhum outro usuário já conectado. Siga as etapas a seguir para conectar as instâncias do SQL Server em vários computadores Linux.

1. Crie a entidade de serviço usando o comando ['az ad sp create-for-rbac'](/cli/azure/ad/sp.md#az_ad_sp_create_for_rbac). 

   ```azurecli-interactive
   az ad sp create-for-rbac --name <your service principal name> --role <your custom role name>    
   ```

   ```output
   { "appId": "d2ff754a-e10a-4eb6-9cdc-ce6e7a4687db",
     "displayName": "Arc-for-servers",
     "name": "http://Arc-for-servers",
     "password": {SomeRandomlyGeneratedPassword}",
     "tenant": "2530e75f-673b-4841-8270-47ca6a34ef4f"
   }
   ```

   > [!NOTE]
   > Quando você cria uma entidade de serviço, sua conta deve ser um Proprietário ou Administrador de Acesso de Usuário na assinatura que deseja usar para integração. Se você não tiver permissões suficientes para criar atribuições de função, a entidade de serviço poderá ser criada, mas não poderá integrar computadores. As instruções de como criar uma função personalizada são fornecidas em [Permissões necessárias](overview.md#required-permissions).

2. Baixe o script de shell do Linux no portal seguindo as instruções em [Conectar o SQL Server com o Azure Arc](connect.md).

3. Substitua as variáveis a seguir no script usando os valores retornados pelo comando 'az ad sp create-for-rbac'. Essas variáveis estão vazias inicialmente.

   ```bash
   servicePrincipalAppId="{serviceprincipalAppID}"
   servicePrincipalSecret="{serviceprincipalPassword}"
   servicePrincipalTenant="{serviceprincipalTenant}"
   ```

3. Executar o script em cada computador de destino
 
   ```bash
   sudo chmod +x ./RegisterSqlServerArc.sh
   ./RegisterSqlServerArc.sh
   ```

## <a name="validate-successful-onboarding"></a>Validar a integração bem-sucedida

Depois de registrar as instâncias do SQL Server no SQL Server habilitado para o Azure Arc (versão prévia), acesse o [portal do Azure](https://aka.ms/azureportal) e veja os recursos do Azure Arc recém-criados. Você verá um novo recurso __Computador – Azure Arc__ para cada computador conectado e um novo recurso __SQL Server – Azure Arc__ para cada instância do SQL Server registrada. 

![Uma integração bem-sucedida](./media/join-at-scale/successful-onboard.png)

## <a name="next-steps"></a>Próximas etapas

- Saiba como gerenciar seu computador usando o [Azure Policy](/azure/governance/policy/overview) para itens como [configurar convidados](/azure/governance/policy/concepts/guest-configuration) de VM, verificar se o computador está relatando ao workspace do Log Analytics esperado, habilitar o monitoramento com o [Azure Monitor em VMs](/azure/azure-monitor/insights/vminsights-enable-policy) e muito mais.

- Saiba mais sobre o [Agente do Log Analytics](/azure/azure-monitor/platform/log-analytics-agent). O agente do Log Analytics para Windows e Linux é necessário quando você deseja monitorar proativamente o sistema operacional e as cargas de trabalho em execução no computador, o gerencia usando os runbooks de automação ou soluções como o Gerenciamento de Atualizações ou usa outros serviços do Azure como a [Central de Segurança do Azure](/azure/security-center/security-center-intro).

- Saiba como [Configurar a instância do SQL Server para verificação periódica de integridade do ambiente usando a avaliação do SQL sob demanda](assess.md)

- Saiba como [Configurar a segurança de dados avançada da instância do SQL Server](configure-advanced-data-security.md)