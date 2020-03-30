---
title: Dimensionar scripts simultâneos
description: Configure a execução de script R e Python paralela ou simultânea em um pool de contas de usuário para dimensionar os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: c10f92bcb0f8b64441ad4b088c4b8b3e2f62236b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727696"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>Escalonar a execução simultânea de scripts externos nos Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Saiba mais sobre contas de trabalho para os Serviços de Machine Learning do SQL Server e sobre como alterar a configuração padrão para dimensionar o número de execuções simultâneas de scripts externos.

Como parte do processo de instalação para os Serviços de Machine Learning, um novo *pool de contas de usuário* do Windows é criado para dar suporte à execução de tarefas pelo serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. A finalidade dessas contas de trabalho é isolar a execução simultânea de scripts externos por diferentes usuários do SQL Server.

> [!Note]
> No SQL Server 2019, **SQLRUserGroup** tem apenas um membro que agora é a única conta de serviço do SQL Server Launchpad, em vez de várias contas de trabalho. Este artigo descreve as contas de trabalho para SQL Server 2016 e 2017.

## <a name="worker-account-group"></a>Grupo de contas de trabalho

Um grupo de conta do Windows é criado pela instalação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada instância em que o aprendizado de máquina está instalado e habilitado.

- Em uma instância padrão, o nome do grupo é **SQLRUserGroup**. O nome é o mesmo, independentemente de você usar o Python, o R ou os dois.
- Em uma instância nomeada, o nome do grupo padrão é sufixado com o nome da instância, por exemplo, **SQLRUserGroupMyInstanceName**.

Por padrão, o pool de contas de usuário contém 20 contas de usuário. Na maioria dos casos, 20 é mais do que adequado para oferecer suporte a tarefas de aprendizado de máquina, mas é possível alterar o número de contas. O número máximo de contas de usuário é 100.

- Em uma instância padrão, as contas individuais são nomeadas de **MSSQLSERVER01** a **MSSQLSERVER20**.
- Para uma instância nomeada, as contas individuais são nomeadas após o nome da instância: por exemplo, de **MyInstanceName01** a **MyInstanceName20**.

Se mais de uma instância usar aprendizado de máquina, o computador terá vários grupos de usuários. Um grupo não pode ser compartilhado entre diferentes instâncias.

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>Número de contas de trabalho

Para modificar o número de usuários no pool de contas, você deverá editar as propriedades do serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] conforme descrito abaixo.

As senhas associadas a cada conta de usuário são geradas aleatoriamente, mas você pode alterá-las posteriormente, depois que as contas forem criadas.

1. Abra o SQL Server Configuration Manager e selecione **Serviços do SQL Server**.
2. Clique duas vezes o serviço Launchpad do SQL Server e interrompa o serviço se ele estiver em execução.
3.  Na guia **Serviço**, certifique-se de que o Modo de Inicialização está definido como Automático. Os scripts externos não podem ser iniciados quando o Launchpad não está em execução.
4.  Clique na guia **Avançado** e edite o valor de **Contagem de Usuários Externos**, se necessário. Essa configuração controla quantos usuários diferentes do SQL podem executar sessões de script simultaneamente. O padrão é 20 contas. O número máximo de usuários é 100.
5. Opcionalmente, você poderá definir a opção **Redefinir a Senha de Usuários Externos** para _Sim_ se sua organização tiver uma política que exija a alteração de senhas regularmente. Isso regenerará as senhas criptografadas que o Launchpad mantém para as contas de usuário. Para obter mais informações, consulte [Imposição de Política de Senha](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy).
6.  Reinicie o serviço Launchpad.

## <a name="managing-workloads"></a>Gerenciar cargas de trabalho

O número de contas nesse pool determina quantas sessões de script externo podem estar ativas simultaneamente.  Por padrão, são criadas 20 contas, o que significa que 20 usuários diferentes podem ter sessões de Python ou R ativas simultaneamente. Caso tenha expectativa de executar mais de 20 scripts simultâneos, você pode aumentar o número de contas de trabalho.

Quando o mesmo usuário executa vários scripts externos simultaneamente, todas as sessões executadas pelo usuário usarão a mesma conta de trabalho. Por exemplo, um único usuário poderá ter 100 scripts Python ou R diferentes em execução simultaneamente, desde que os recursos permitam, mas todos os scripts seriam executados usando uma única conta de trabalho.

O número de contas de trabalho às quais você pode dar suporte e o número de sessões simultâneas que qualquer usuário pode executar são limitados apenas pelos recursos de servidor. Normalmente, a memória é o primeiro gargalo que você encontrará ao usar o runtime de Python ou R.

Os recursos que podem ser usados por scripts Python ou R são regidos pelo SQL Server. É recomendável monitorar o uso de recursos usando DMVs do SQL Server ou examinar os contadores de desempenho no objeto de trabalho associado do Windows, para então ajustar o uso de memória do servidor de acordo com isso. Se você tiver o Edição Enterprise do SQL Server, poderá alocar recursos usados para executar scripts externos configurando um [pool de recursos externo](how-to-create-a-resource-pool.md).

## <a name="next-steps"></a>Próximas etapas

- [Monitorar a execução de script do Python e do R usando relatórios personalizados no SQL Server Management Studio](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [Monitorar os Serviços de Machine Learning do SQL Server usando DMVs (exibições de gerenciamento dinâmico)](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)