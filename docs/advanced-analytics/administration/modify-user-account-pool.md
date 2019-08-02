---
title: Dimensionar a execução simultânea de scripts externos
description: Configure a execução de script de R e Python paralela ou simultânea em um pool de contas de usuário para dimensionar SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a5a0cd5ab05f7675ce011fe5205cbba3432725f4
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715860"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>Dimensionar a execução simultânea de scripts externos no SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Como parte do processo de instalação para os [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)], um novo *pool de contas de usuário* do Windows é criado para dar suporte à execução de tarefas pelo serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. A finalidade dessas contas de trabalho é isolar a execução simultânea de scripts externos por diferentes usuários do SQL.

Este artigo descreve a configuração e a capacidade padrão para as contas de trabalho e como alterar a configuração padrão para dimensionar o número de execuções simultâneas de scripts externos no SQL Server Serviços de Machine Learning.

## <a name="worker-account-group"></a>Grupo de contas de trabalho

Um grupo de contas do Windows é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado pela instalação para cada instância em que o Machine Learning está instalado e habilitado.

- Em uma instância padrão, o nome do grupo é **SQLRUserGroup**. O nome é o mesmo se você usar R ou Python ou ambos.
- Em uma instância nomeada, o nome do grupo padrão é sufixado com o nome da instância, por exemplo, **SQLRUserGroupMyInstanceName**.

Por padrão, o pool de contas de usuário contém 20 contas de usuário. Na maioria dos casos, 20 é mais do que adequado para dar suporte a tarefas de aprendizado de máquina, mas você pode alterar o número de contas. O número máximo de contas é 100.

- Em uma instância padrão, as contas individuais são nomeadas de **MSSQLSERVER01** a **MSSQLSERVER20**.
- Para uma instância nomeada, as contas individuais são nomeadas após o nome da instância: por exemplo, de **MyInstanceName01** a **MyInstanceName20**.

Se mais de uma instância usar o Machine Learning, o computador terá vários grupos de usuários. Um grupo não pode ser compartilhado entre instâncias.

> [!Note]
> No SQL Server 2019, **SQLRUserGroup** tem apenas um membro que agora é a única conta de serviço de SQL Server Launchpad em vez de várias contas de trabalho.

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>Número de contas de trabalho

Para modificar o número de usuários no pool de contas, você deverá editar as propriedades do serviço [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] conforme descrito abaixo.

As senhas associadas a cada conta de usuário são geradas aleatoriamente, mas você pode alterá-las posteriormente, depois que as contas forem criadas.

1. Abra o SQL Server Configuration Manager e selecione **Serviços do SQL Server**.
2. Clique duas vezes o serviço Launchpad do SQL Server e interrompa o serviço se ele estiver em execução.
3.  Na guia **Serviço**, certifique-se de que o Modo de Inicialização está definido como Automático. Os scripts externos não podem ser iniciados quando o Launchpad não está em execução.
4.  Clique na guia **Avançado** e edite o valor de **Contagem de Usuários Externos**, se necessário. Essa configuração controla quantos usuários diferentes do SQL podem executar sessões de script externas simultaneamente. O padrão é 20 contas. O número máximo de usuários é 100.
5. Opcionalmente, você poderá definir a opção **Redefinir a Senha de Usuários Externos** para _Sim_ se sua organização tiver uma política que exija a alteração de senhas regularmente. Isso regenerará as senhas criptografadas que o Launchpad mantém para as contas de usuário. Para obter mais informações, consulte [Imposição de Política de Senha](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy).
6.  Reinicie o serviço Launchpad.

## <a name="managing-workloads"></a>Gerenciando cargas de trabalho

O número de contas nesse pool determina quantas sessões de script externo podem estar ativas simultaneamente.  Por padrão, 20 contas são criadas, o que significa que 20 usuários diferentes podem ter sessões de R ou Python ativas ao mesmo tempo. Você pode aumentar o número de contas de trabalho, se espera executar mais de 20 scripts simultâneos.

Quando o mesmo usuário executa vários scripts externos simultaneamente, todas as sessões executadas por esse usuário usam a mesma conta de trabalho. Por exemplo, um único usuário pode ter 100 diferentes scripts de R em execução simultaneamente, desde que os recursos permitam, mas todos os scripts seriam executados usando uma única conta de trabalho.

O número de contas de trabalho às quais você pode dar suporte e o número de sessões simultâneas que qualquer usuário pode executar é limitado apenas por recursos do servidor. Normalmente, a memória é o primeiro gargalo que você encontrará ao usar o tempo de execução de R.

Os recursos que podem ser usados por scripts Python ou R são governados pelo SQL Server. É recomendável monitorar o uso de recursos usando DMVs do SQL Server ou examinar os contadores de desempenho no objeto de trabalho associado do Windows, para então ajustar o uso de memória do servidor de acordo com isso. Se você tiver SQL Server Enterprise Edition, poderá alocar recursos usados para executar scripts externos Configurando um [pool de recursos externos](how-to-create-a-resource-pool.md).

## <a name="see-also"></a>Confira também

Para obter informações adicionais sobre como configurar a capacidade, consulte estes artigos:

- [Configuração de SQL Server para o R Services](../../advanced-analytics/r/sql-server-configuration-r-services.md)
- [Estudo de caso de desempenho para R Services](../../advanced-analytics/r/performance-case-study-r-services.md)