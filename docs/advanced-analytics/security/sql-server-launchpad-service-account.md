---
title: SQL Server Launchpad configuração da conta de serviço
description: Como modificar a conta de serviço SQL Server Launchpad usada para a execução de script externo no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9146020fb35d729575c8441e71b711e287399a75
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345532"
---
# <a name="sql-server-launchpad-service-configuration"></a>Configuração do serviço de SQL Server Launchpad
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é um serviço que gerencia e executa scripts externos, semelhante ao modo como o serviço de indexação e consulta de texto completo inicia um host separado para o processamento de consultas de texto completo.

Para obter mais informações, consulte as seções Launchpad em [arquitetura de extensibilidade em SQL Server serviços de Machine Learning](../../advanced-analytics/concepts/extensibility-framework.md#launchpad) e [visão geral de segurança para a estrutura de extensibilidade no SQL Server serviços de Machine Learning](../../advanced-analytics/concepts/security.md#launchpad).

## <a name="account-permissions"></a>Permissões de conta

Por padrão, SQL Server Launchpad é configurado para ser executado em **NT Service\MSSQLLaunchpad**, que é provisionado com todas as permissões necessárias para executar scripts externos. A remoção de permissões dessa conta pode fazer com que o Launchpad não seja iniciado ou acesse a instância de SQL Server em que os scripts externos devem ser executados.

Se você modificar a conta de serviço, certifique-se de usar o [console de política de segurança local](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings).

As permissões necessárias para essa conta estão listadas na tabela a seguir.

| Configuração de política de grupo | Nome da constante |
|----------------------|---------------|
| [Ajustar cotas de memória para um processo](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [Ignorar verificação completa](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [Fazer logon como um serviço](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [Substituir um token de nível de processo](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

Para obter mais informações sobre as permissões necessárias para executar serviços SQL Server, consulte [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>Propriedades de configuração

Normalmente, não há motivo para modificar a configuração do serviço. As propriedades que poderiam ser alteradas incluem a conta de serviço, a contagem de processos externos (20 por padrão) ou a política de redefinição de senha para contas de trabalho.

1. Abra [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

2. Em serviços de SQL Server, clique com o botão direito do mouse em SQL Server Launchpad e selecione **Propriedades**.
  + Para alterar a conta de serviço, clique na guia **fazer logon** .
  + Para aumentar o número de usuários, clique na guia **avançado** e altere a **contagem**de contextos de segurança.

> [!Note]
> Nas versões anteriores do SQL Server R Services 2016, você pode alterar algumas propriedades do serviço editando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] arquivo de configuração. Este arquivo não é mais usado para alterar as configurações. SQL Server Configuration Manager é a abordagem certa para alterações na configuração de serviço, como a conta de serviço e o número de usuários.

## <a name="debug-settings"></a>Configurações de depuração

Algumas propriedades só podem ser alteradas usando o arquivo de configuração do Launchpad, que pode ser útil em casos limitados, como a depuração. O arquivo de configuração é criado durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a instalação e, por padrão, é salvo como um arquivo `<instance path>\binn\rlauncher.config`de texto sem formatação no.

Você deve ser um administrador no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer alterações nesse arquivo. Se você editar o arquivo, é recomendável que você faça uma cópia de backup antes de salvar as alterações.

A tabela a seguir lista as configurações avançadas [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]para, com os valores permitidos.

|**Nome da configuração**|**Tipo**|**Descrição**|
|----|----|----|
|LIMPEZA\_\_DOTRABALHOAOSAIR\_|Inteiro |Esta é apenas uma configuração interna – não altere esse valor. </br></br>Especifica se a pasta de trabalho temporária criada para cada sessão de tempo de execução externa deve ser limpa após a conclusão da sessão. Essa configuração é útil para depuração. </br></br>Os valores com suporte são **0** (desabilitado) ou **1** (habilitado). </br></br>O padrão é 1, o que significa que os arquivos de log são removidos ao sair.|
|NÍVEL\_DE RASTREAMENTO|Inteiro |Configura o nível de detalhamento de rastreamento de MSSQLLAUNCHPAD para fins de depuração. Isso afeta os arquivos de rastreamento no caminho especificado pela configuração LOG_DIRECTORY. </br></br>Os valores com suporte são: **1** (erro), **2** (desempenho), **3** (aviso), **4** (informações). </br></br>O padrão é 1, o que significa apenas erros de saída.|

Todas as configurações assumem a forma de um par chave-valor, com cada configuração em uma linha separada. Por exemplo, para alterar o nível de rastreamento, você adicionaria a `Default: TRACE_LEVEL=4`linha.

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>Impondo política de senha

Se sua organização tiver uma política que exija a alteração de senhas regularmente, você precisará forçar o serviço Launchpad a regenerar novamente as senhas criptografadas que o Launchpad mantém para as contas de trabalho dele.

Para habilitar essa configuração e forçar a atualização da senha, abra o painel **Propriedades** para o serviço Launchpad no SQL Server Configuration Manager, clique em **Avançado** e altere **Redefinir a Senha de Usuários Externos** para **Sim**. Quando você aplicar essa alteração, as senhas serão regeneradas imediatamente para todas as contas de usuário. Para executar um script externo após essa alteração, você deve reiniciar o serviço Launchpad e, nesse momento, ele lerá as senhas recém-gerado.

Para redefinir senhas em intervalos regulares, você pode definir esse sinalizador manualmente ou usar um script.

## <a name="next-steps"></a>Próximas etapas

+ [Estrutura de extensibilidade](../concepts/extensibility-framework.md)
+ [Visão geral de segurança](../concepts/security.md)
