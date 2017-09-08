---
title: "Modificar o pool de contas de usuário para o SQL Server R Services | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 33e22f7edec807d046798d89a9cd5daa642e8d3b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="modify-the-user-account-pool-for-sql-server-r-services"></a>Modificar o pool de contas de usuário para o SQL Server R Services
  Como parte do processo de instalação para os [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], um novo *pool de contas de usuário* do Windows é criado para dar suporte à execução de tarefas pelo serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. A finalidade dessas contas de trabalho é isolar a execução simultânea de scripts R por diferentes usuários do SQL. 

Este tópico descreve a configuração padrão, a segurança e a capacidade das contas de trabalho e como alterar a configuração padrão.

## <a name="worker-accounts-used-by-r-services"></a>Contas de trabalho usadas pelo R Services   

O grupo de conta do Windows é criado pela instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada instância em que R Services está instalado. Portanto, se você tiver instalado várias instâncias com suporte a R, haverá vários grupos de usuários.

-   Em uma instância padrão, o nome do grupo é **SQLRUserGroup**. 
-   Em uma instância nomeada, o nome do grupo padrão é sufixado com o nome da instância, por exemplo, **SQLRUserGroupMyInstanceName**. 

Por padrão, o pool de contas de usuário contém 20 contas de usuário. Na maioria dos casos, 20 é mais do que adequado para dar suporte a sessões de R, mas você pode alterar o número de contas.
-  Em uma instância padrão, as contas individuais são nomeadas de **MSSQLSERVER01** a **MSSQLSERVER20**.  
-   Para uma instância nomeada, as contas individuais são nomeadas após o nome da instância: por exemplo, de **MyInstanceName01** a **MyInstanceName20**.  

### <a name = "HowToChangeGroup"> </a>Como alterar o número de contas de trabalho do R

Para modificar o número de usuários no pool de contas, você deverá editar as propriedades do serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] conforme descrito abaixo.  
  
As senhas associadas a cada conta de usuário são geradas aleatoriamente, mas você pode alterá-las posteriormente, depois que as contas forem criadas.  
  
1. Abra o SQL Server Configuration Manager e selecione **Serviços do SQL Server**.
2. Clique duas vezes o serviço Launchpad do SQL Server e interrompa o serviço se ele estiver em execução. 
3.  Na guia **Serviço**, certifique-se de que o Modo de Inicialização está definido como Automático. Os scripts R falharão se o Launchpad não estiver em execução.
4.  Clique na guia **Avançado** e edite o valor de **Contagem de Usuários Externos**, se necessário. Essa configuração controla quantos usuários diferentes do SQL podem realizar consultas simultaneamente em R. O padrão é 20 contas.
5. Opcionalmente, você poderá definir a opção **Redefinir a Senha de Usuários Externos** para _Sim_ se sua organização tiver uma política que exija a alteração de senhas regularmente. Isso regenerará as senhas criptografadas que o Launchpad mantém para as contas de usuário. Para obter mais informações, consulte [Imposição de Política de Senha](#bkmk_EnforcePolicy).    
6.  Reinicie o serviço.  

## <a name="managing-r-workload"></a>Gerenciamento de carga de trabalho de R

O número de contas nesse pool determina quantas sessões de R podem estar ativas simultaneamente.  Por padrão, são criadas 20 contas, o que significa que 20 usuários diferentes podem ter sessões de R ativas simultaneamente. Se você prever a necessidade de mais usuários simultâneos executando scripts R, você poderá aumentar o número de contas de trabalho. 

Quando o mesmo usuário executa vários scripts de R simultaneamente, todas as sessões executadas pelo usuário usarão a mesma conta de trabalho. Por exemplo, um único usuário poderá ter 100 scripts R diferentes em execução simultaneamente, desde que os recursos permitam, usando uma única conta de trabalho.

O número de contas de trabalho às quais você pode dar suporte e o número de sessões simultâneas do R que qualquer usuário pode executar são limitados apenas pelos recursos de servidor.  Normalmente, a memória é o primeiro afunilamento que você encontrará ao usar o tempo de execução de R.

No R Services, os recursos que podem ser usados pelos scripts R são regidos pelo SQL Server. É recomendável monitorar o uso de recursos usando DMVs do SQL Server ou examinar os contadores de desempenho no objeto de trabalho associado do Windows, para então ajustar o uso de memória do servidor de acordo com isso. 
 
Se você tiver o SQL Server Enterprise Edition, você poderá alocar recursos usados para executar scripts R configurando um [pool de recursos externo](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md). 

Para obter informações adicionais sobre o gerenciamento de capacidade de script R, consulte estes artigos:

- [Configuração do SQL Server para R Services](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
-  [Estudo de caso de desempenho (para R Services)](../../advanced-analytics/r-services/performance-case-study-r-services.md)

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

Para garantir que haja suporte para esses cenários, o administrador de banco de dados deverá fornecer o grupo de contas de trabalho do R com permissão para fazer logon na instância do SQL Server em que os scripts R serão executados (permissões **Conectar-se a**). Isso é conhecido como *autenticação implícita* e permite que o SQL Server execute os scripts R usando as credenciais do usuário remoto.

> [!NOTE]
> Essa limitação não se aplicará se você usar logons SQL para executar scripts R em uma estação de trabalho remota, pois as credenciais de logon SQL são passadas explicitamente do cliente R para a instância do SQL Server e, em seguida, para o ODBC.


### <a name="how-to-enable-implied-authentication"></a>Como habilitar a autenticação implícita

1. Abra o SQL Server Management Studio como administrador na instância em que você executará o código R.

2. Execute o script a seguir. Edite o nome do grupo de usuários, caso tenha alterado o padrão e o nome do computador e da instância.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ````


  
## <a name="see-also"></a>Consulte também  
 [Configuração (SQL Server R Services)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  

