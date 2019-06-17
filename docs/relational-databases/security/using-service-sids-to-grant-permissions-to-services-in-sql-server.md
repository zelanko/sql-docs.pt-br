---
title: Usando SIDs de serviço para conceder permissões para serviços no SQL Server | Microsoft Docs
author: randomnote1
ms.author: dareist
ms.date: 05/02/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.openlocfilehash: 1a0bd129fc535b53d8d19ad76f99f3a86ba10c11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65135232"
---
# <a name="using-service-sids-to-grant-permissions-to-services-in-sql-server"></a>Usando SIDs de serviço para conceder permissões para serviços no SQL Server

O SQL Server usa [SID (identificadores de segurança) por serviço](https://support.microsoft.com/help/2620201/sql-server-uses-a-service-sid-to-provide-service-isolation) para possibilitar a concessão de permissões diretamente a um serviço específico. Esse método é usado pelo SQL Server para conceder permissões para os serviços de mecanismo e de agente (NT SERVICE\MSSQL$<InstanceName> e NT SERVICE\SQLAGENT$<InstanceName>, respectivamente). Usando esse método, esses serviços podem acessar o mecanismo de banco de dados somente quando os serviços estão em execução.

Esse mesmo método pode ser usado ao conceder permissões a outros serviços. Usar um SID de serviço elimina a sobrecarga de gerenciamento e manutenção de contas de serviço e dá um controle mais rigoroso e granular sobre as permissões concedidas aos recursos do sistema.

Exemplos de serviços em que um SID de serviço pode ser usado são:

- Serviço de Integridade do System Center Operations Manager (NT SERVICE\HealthService)
- Serviço de Clustering de Failover do Windows Server (WSFC) (SERVICE\ClusSvc NT)

Por padrão, alguns serviços não têm um SID de serviço. O SID de serviço deve ser criado usando [SC.exe](https://docs.microsoft.com/windows/desktop/services/configuring-a-service-using-sc). [Esse método](https://kevinholman.com/2016/08/25/sql-mp-run-as-accounts-no-longer-required/) foi adotado por administradores do Microsoft System Center Operations Manager para conceder permissão para o HealthService dentro do SQL Server.

Uma vez o serviço SID foi criado e confirmado, ele deve ter a permissão dentro do SQL Server. Conceder permissões é feito criando um logon do Windows usando um [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) ou uma consulta. Depois que o logon for criado, ele poderá receber permissões, ser adicionado a funções e ser mapeado para bancos de dados assim como qualquer outro logon.

> [!TIP]
> Se o erro `Login failed for user 'NT AUTHORITY\SYSTEM'` for recebido, verifique se o SID de serviço existe para o serviço desejado, se o logon do SID de serviço foi criado no SQL Server e se as permissões apropriadas foram concedidas para o SID de serviço no SQL Server.

## <a name="security"></a>Segurança

### <a name="eliminate-service-accounts"></a>Eliminar as contas de serviço

Tradicionalmente, contas de serviço eram usadas para permitir os serviços logon no SQL Server. Contas de serviço adicionam uma camada adicional de complexidade de gerenciamento devido à necessidade de manter e atualizar periodicamente a senha da conta de serviço. Além disso, as credenciais da conta de serviço poderiam ser usadas por uma pessoa tentando mascarar suas atividades ao realizar ações na instância.

### <a name="granular-permissions-to-system-accounts"></a>Permissões granulares para contas do sistema

Contas do sistema historicamente recebem permissões criando um logon para as contas [LocalSystem](https://msdn.microsoft.com/library/windows/desktop/ms684190) ([NT AUTHORITY\SYSTEM em en-us](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions#Localized_service_names)) ou [NetworkService](https://docs.microsoft.com/windows/desktop/Services/networkservice-account) ([NT AUTHORITY\NETWORK SERVICE em en-us](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?#Localized_service_names)) e concedendo a elas permissões de logon. Esse método concede qualquer permissão de processo ou serviço em SQL, que está em execução como uma conta do sistema.

Usar um SID de Serviço possibilita a concessão de permissões a um serviço específico. O serviço só tem acesso aos recursos para os quais recebeu permissões quando está em execução. Por exemplo, se o `HealthService` estiver em execução como `LocalSystem` e receber `View Server State`, a conta `LocalSystem` só terá permissão para `View Server State` quando estiver em execução no contexto do `HealthService`. Se qualquer outro processo tentar acessar o estado do servidor do SQL como `LocalSystem`, ele terá o acesso negado.

## <a name="examples"></a>Exemplos

### <a name="a-create-a-service-sid"></a>A. Criar uma ID de Serviço

O seguinte comando do PowerShell criará um SID de serviço no serviço de integridade do System Center Operations Manager.

```PowerShell
sc.exe --% sidtype "HealthService" unrestricted
```

> [!IMPORTANT]
> `--%` diz para o PowerShell deixar de analisar o restante do comando. Isso é útil ao usar comandos e aplicativos herdados.

### <a name="b-query-a-service-sid"></a>B. Consultar um SID de Serviço

Para verificar um SID de serviço ou verificar se um SID de serviço existe, execute o seguinte comando no PowerShell.

```PowerShell
sc.exe --% qsidtype "HealthService"
```

> [!IMPORTANT]
> `--%` diz para o PowerShell deixar de analisar o restante do comando. Isso é útil ao usar comandos e aplicativos herdados.

### <a name="c-add-a-newly-created-service-sid-as-a-login"></a>C. Adicionar um SID de serviço recém-criado como um logon

O exemplo a seguir cria um logon para o serviço de integridade do System Center Operations Manager usando o T-SQL.

```SQL
CREATE LOGIN [NT SERVICE\HealthService] FROM WINDOWS
GO
```

### <a name="d-add-an-existing-service-sid-as-a-login"></a>D. Adicionar um SID de serviço existente como um logon

O exemplo a seguir cria um logon para o Serviço de Cluster usando o T-SQL. Conceder permissões ao serviço de cluster elimina diretamente a necessidade de conceder permissões excessivas para a conta SYSTEM.

```SQL
CREATE LOGIN [NT SERVICE\ClusSvc] FROM WINDOWS
GO
```

### <a name="e-grant-permissions-to-a-service-sid"></a>E. Conceder permissões para um SID de Serviço

Conceda as permissões necessárias para gerenciar grupos de disponibilidade para o Serviço de Cluster.

```SQL
GRANT ALTER ANY AVAILABILITY GROUP TO 'NT SERVICE\ClusSvc'
GO

GRANT CONNECT SQL TO 'NT SERVICE\ClusSvc'
GO

GRANT VIEW SERVER STATE TO 'NT SERVICE\ClusSvc'
GO
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o serviço de estrutura de sid, leia [estrutura SERVICE_SID_INFO](https://docs.microsoft.com/windows/desktop/api/winsvc/ns-winsvc-_service_sid_info).

Leia sobre as opções adicionais disponíveis ao [criar um logon](https://docs.microsoft.com/sql/t-sql/statements/create-login-transact-sql).

Para usar segurança baseada em função com SIDs de serviço, leia sobre [criar funções](https://docs.microsoft.com/sql/t-sql/statements/create-role-transact-sql) no SQL Server.

Leia sobre diferentes maneiras de [conceder permissões](https://docs.microsoft.com/sql/t-sql/statements/grant-transact-sql) para SIDs de serviço no SQL Server.
