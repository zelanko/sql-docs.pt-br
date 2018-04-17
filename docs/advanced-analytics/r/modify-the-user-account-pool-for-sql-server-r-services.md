---
title: Modificar o pool de conta de usuário para o aprendizado de máquina do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 77b84e3117b0a1366f3d0b5f9d74802d938bc86b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="modify-the-user-account-pool-for-sql-server-machine-learning"></a>Modificar o pool de conta de usuário para o aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Como parte do processo de instalação para os [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)], um novo *pool de contas de usuário* do Windows é criado para dar suporte à execução de tarefas pelo serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. O objetivo dessas contas de trabalho é isolar a execução simultânea de scripts externos por diferentes usuários do SQL.

Este artigo descreve a configuração padrão, a segurança e a capacidade para as contas de trabalho e como alterar a configuração padrão.

**Aplica-se a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)], [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="worker-accounts-used-for-external-script-execution"></a>Contas de trabalho usadas para a execução do script externo

O grupo de contas do Windows é criado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação para cada instância na qual o machine learning está instalado e habilitado.

-   Em uma instância padrão, o nome do grupo é **SQLRUserGroup**. O nome é o mesmo se você usar R, Python ou ambos.
-   Em uma instância nomeada, o nome do grupo padrão é sufixado com o nome da instância, por exemplo, **SQLRUserGroupMyInstanceName**.

Por padrão, o pool de contas de usuário contém 20 contas de usuário. Na maioria dos casos, 20 é mais do que adequado para dar suporte a tarefas de aprendizado de máquina, mas você pode alterar o número de contas. O número máximo de contas é 100.
-  Em uma instância padrão, as contas individuais são nomeadas de **MSSQLSERVER01** a **MSSQLSERVER20**.
-   Para uma instância nomeada, as contas individuais são nomeadas após o nome da instância: por exemplo, de **MyInstanceName01** a **MyInstanceName20**.

Se mais de uma instância usa o aprendizado de máquina, o computador tenha vários grupos de usuários. Um grupo não pode ser compartilhado entre instâncias.

### <a name = "HowToChangeGroup"> </a>Como alterar o número de contas de trabalho

Para modificar o número de usuários no pool de contas, você deverá editar as propriedades do serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] conforme descrito abaixo.

As senhas associadas a cada conta de usuário são geradas aleatoriamente, mas você pode alterá-las posteriormente, depois que as contas forem criadas.

1. Abra o SQL Server Configuration Manager e selecione **Serviços do SQL Server**.
2. Clique duas vezes o serviço Launchpad do SQL Server e interrompa o serviço se ele estiver em execução.
3.  Na guia **Serviço**, certifique-se de que o Modo de Inicialização está definido como Automático. Scripts externos não podem iniciar quando a barra inicial não está em execução.
4.  Clique na guia **Avançado** e edite o valor de **Contagem de Usuários Externos**, se necessário. Essa configuração controla quantos usuários diferentes do SQL pode executar script externo sessões simultaneamente. O padrão é 20 contas. O número máximo de usuários é 100.
5. Opcionalmente, você poderá definir a opção **Redefinir a Senha de Usuários Externos** para _Sim_ se sua organização tiver uma política que exija a alteração de senhas regularmente. Isso regenerará as senhas criptografadas que o Launchpad mantém para as contas de usuário. Para obter mais informações, consulte [Imposição de Política de Senha](#bkmk_EnforcePolicy).
6.  Reinicie o serviço barra inicial.

## <a name="managing-machine-learning-workloads"></a>Gerenciar cargas de trabalho de aprendizado de máquina

O número de contas nesse pool determina quantas sessões de script externo podem estar ativas simultaneamente.  Por padrão, 20 contas são criadas, o que significa que 20 usuários diferentes podem ter R ou Python sessões ativas ao mesmo tempo. Você pode aumentar o número de contas de trabalho, se você pretende executar mais de 20 scripts simultâneas.

Quando o mesmo usuário executa vários scripts externos ao mesmo tempo, todas as sessões de execução que o usuário usam a mesma conta de trabalho. Por exemplo, um único usuário pode ter diferentes 100 scripts de R em execução simultaneamente, contanto que permitem que recursos, mas todos os scripts seriam executados usando uma conta de trabalho único.

O número de contas de trabalho que você pode dar suporte e o número de sessões simultâneas que qualquer usuário pode executar, é limitado apenas pelos recursos de servidor. Normalmente, a memória é o primeiro gargalo que você encontrará ao usar o tempo de execução de R.

Os recursos que podem ser usados pelos scripts Python ou R são administrados pelo SQL Server. É recomendável monitorar o uso de recursos usando DMVs do SQL Server ou examinar os contadores de desempenho no objeto de trabalho associado do Windows, para então ajustar o uso de memória do servidor de acordo com isso. Se você tiver o SQL Server Enterprise Edition, você pode alocar recursos usados para a execução de scripts externos, configurando uma [pool de recursos externos](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md).

Para obter informações adicionais sobre o gerenciamento de máquina aprendizado capacidade de tarefas, consulte estes artigos:

- [Configuração do SQL Server para R Services](../../advanced-analytics/r/sql-server-configuration-r-services.md)
-  [Estudo de caso de desempenho para R Services](../../advanced-analytics/r/performance-case-study-r-services.md)

## <a name="security"></a>Segurança

Cada grupo de usuário é associado com o serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] em uma instância específica e não dá suporte a trabalhos do R executados em outras instâncias.

Para cada conta de trabalho, enquanto a sessão está ativa, uma pasta temporária é criada para armazenar os objetos de script, resultados intermediários e outras informações usadas pelo R e pelo SQL Server durante a execução do script R. Esses arquivos de trabalho, localizados na pasta ExtensibilityData, têm o acesso restrito aos administradores e são limpos pelo SQL Server após a conclusão do script. 

Para obter mais informações, consulte [Visão geral de segurança](../../advanced-analytics/r-services/security-overview-sql-server-r.md).

### <a name="bkmk_EnforcePolicy"></a>Imposição de política de senha

Se sua organização tiver uma política que exija a alteração de senhas regularmente, você precisará forçar o serviço Launchpad a regenerar novamente as senhas criptografadas que o Launchpad mantém para as contas de trabalho dele.  

Para habilitar essa configuração e forçar a atualização da senha, abra o painel **Propriedades** para o serviço Launchpad no SQL Server Configuration Manager, clique em **Avançado** e altere **Redefinir a Senha de Usuários Externos** para **Sim**. Quando você aplicar essa alteração, as senhas serão regeneradas imediatamente para todas as contas de usuário. Para usar o script R após essa alteração, você deve reiniciar o serviço Launchpad, momento em que ele fará a leitura das senhas recém-geradas. 

Para redefinir senhas em intervalos regulares, você pode definir esse sinalizador manualmente ou usar um script.

### <a name="additional-permission-required-to-support-remote-compute-contexts"></a>Permissão adicional necessária para dar suporte a contextos de computação remota

Por padrão, o grupo de contas de trabalho do R **não** tem permissões de logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à qual ele está associado. Isso pode ser um problema se os usuários do R se conectarem ao SQL Server de um cliente remoto para executar scripts R ou então se um script usar ODBC para obter dados adicionais. 

Para garantir que haja suporte para esses cenários, o administrador de banco de dados deverá fornecer o grupo de contas de trabalho do R com permissão para fazer logon na instância do SQL Server em que os scripts R serão executados (permissões **Conectar-se a**). Isso é conhecido como *autenticação implícita*e permite que o SQL Server executar os scripts de R usando as credenciais do usuário remoto.

> [!NOTE]
> Essa limitação não se aplicará se você usar logons SQL para executar scripts R em uma estação de trabalho remota, pois as credenciais de logon SQL são passadas explicitamente do cliente R para a instância do SQL Server e, em seguida, para o ODBC.


### <a name="how-to-enable-implied-authentication"></a>Como habilitar a autenticação implícita

1. Abra o SQL Server Management Studio como administrador na instância onde você executa o código de R ou Python.

2. Execute o script a seguir. Edite o nome do grupo de usuários, caso tenha alterado o padrão e o nome do computador e da instância.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ````

