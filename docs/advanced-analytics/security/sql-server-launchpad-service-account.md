---
title: Configuração de conta do Launchpad
description: Como modificar a conta de serviço do SQL Server Launchpad usada para execução de scripts externos no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f05181e1a3069ec56f079751e43bd739424ce92
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727369"
---
# <a name="sql-server-launchpad-service-configuration"></a>Configuração de serviço do SQL Server Launchpad
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é um serviço que gerencia e executa scripts externos, semelhantes à forma com que o serviço de indexação e consulta de texto completo inicia um host separado para o processamento de consultas de texto completo.

Para obter mais informações, confira as seções sobre o Launchpad em [Arquitetura de extensibilidade no Serviços de Machine Learning do SQL Server](../../advanced-analytics/concepts/extensibility-framework.md#launchpad) e [Visão geral de segurança para a estrutura de extensibilidade nos Serviços de Machine Learning do SQL Server](../../advanced-analytics/concepts/security.md#launchpad).

## <a name="account-permissions"></a>Permissões de conta

Por padrão, o SQL Server Launchpad é configurado para ser executado em **NT Service\MSSQLLaunchpad**, que é provisionada com todas as permissões necessárias para executar scripts externos. A remoção de permissões dessa conta pode fazer com que o Launchpad não seja iniciado ou não acesse a instância de SQL Server em que os scripts externos devem ser executados.

Se você modificar a conta de serviço, use o [Console de Política de Segurança Local](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings).

As permissões necessárias para essa conta estão listadas na tabela a seguir.

| Configuração da política de grupo | Nome da constante |
|----------------------|---------------|
| [Ajustar cotas de memória para um processo](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [Ignorar verificação completa](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [Fazer logon como um serviço](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [Substituir um token de nível de processo](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

Para obter mais informações sobre as permissões necessárias para executar serviços SQL Server, consulte [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>Propriedades de configuração

Normalmente, não há motivo para modificar a configuração do serviço. As propriedades que poderiam ser alteradas incluem a conta de serviço, a contagem de processos externos (20 por padrão) ou a política de redefinição de senha para contas de trabalho.

1. Abra o [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

2. Em Serviços do SQL Server, clique com o botão direito do mouse no SQL Server Launchpad e selecione **Propriedades**.
  + Para alterar a conta de serviço, clique na guia **Fazer Logon**.
  + Para aumentar o número de usuários, clique na guia **Avançado** e altere a **Contagem de Contextos de Segurança**.

> [!Note]
> Em versões anteriores do SQL Server R Services 2016, você podia alterar algumas propriedades do serviço editando o arquivo de configuração [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Este arquivo não é mais usado para alterar as configurações. O SQL Server Configuration Manager é a abordagem certa para alterações na configuração de serviço, como a conta de serviço e o número de usuários.

## <a name="debug-settings"></a>Configurações de depuração

Algumas propriedades só podem ser alteradas usando o arquivo de configuração do Launchpad, que pode ser útil em casos limitados, como a depuração. O arquivo de configuração é criado durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, por padrão, é salvo como um arquivo de texto sem formatação em `<instance path>\binn\rlauncher.config`.

Você deve ser um administrador no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer alterações nesse arquivo. Se você editar o arquivo, é recomendável que você faça uma cópia de backup antes de salvar as alterações.

A tabela a seguir lista as configurações avançadas para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], com os valores permitidos.

|**Nome da configuração**|**Tipo**|**Descrição**|
|----|----|----|
|JOB\_CLEANUP\_ON\_EXIT|Integer |Esta é uma configuração interna apenas, não altere esse valor. </br></br>Especifica se a pasta de trabalho temporária criada para cada sessão de runtime externa deve ser limpa após a conclusão da sessão. Essa configuração é útil para depuração. </br></br>Os valores com suporte são **0** (desabilitado) ou **1** (habilitado). </br></br>O padrão é 1, o que significa que os arquivos de log são removidos ao sair.|
|TRACE\_LEVEL|Integer |Configura o nível de detalhamento do rastreamento MSSQLLAUNCHPAD para fins de depuração. Isso afeta os arquivos de rastreamento no caminho especificado pela configuração de LOG_DIRECTORY. </br></br>Os valores com suporte são: **1** (erro), **2** (desempenho), **3** (aviso), **4** (informações). </br></br>O padrão é 1, o que significa apenas erros de saída.|

Todas as configurações assumem a forma de um par chave-valor, com cada configuração em uma linha separada. Por exemplo, para alterar o nível de rastreamento, você adicionaria a linha `Default: TRACE_LEVEL=4`.

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>Imposição de política de senha

Se sua organização tiver uma política que exija a alteração de senhas regularmente, você precisará forçar o serviço Launchpad a regenerar novamente as senhas criptografadas que o Launchpad mantém para as contas de trabalho dele.

Para habilitar essa configuração e forçar a atualização da senha, abra o painel **Propriedades** para o serviço Launchpad no SQL Server Configuration Manager, clique em **Avançado** e altere **Redefinir a Senha de Usuários Externos** para **Sim**. Quando você aplicar essa alteração, as senhas serão regeneradas imediatamente para todas as contas de usuário. Para executar um script externo após essa alteração, você deve reiniciar o serviço Launchpad, momento em que ele fará a leitura das senhas recém-geradas.

Para redefinir senhas em intervalos regulares, você pode definir esse sinalizador manualmente ou usar um script.

## <a name="next-steps"></a>Próximas etapas

+ [Estrutura de extensibilidade](../concepts/extensibility-framework.md)
+ [Visão geral de segurança](../concepts/security.md)
