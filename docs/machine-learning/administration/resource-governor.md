---
title: Gerenciar com o Resource Governor
description: Saiba como usar o Resource Governor para gerenciar a alocação de CPU, E/S física e recursos de memória para cargas de trabalho de Python e R nos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 55fd9d7c699523856ad2623298c62d6f986904a5
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283547"
---
# <a name="manage-python-and-r-workloads-with-resource-governor-in-sql-server-machine-learning-services"></a>Gerenciar cargas de trabalho do Python e do R com o Resource Governor nos Serviços de Machine Learning do SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Saiba como usar o [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) para gerenciar a alocação de CPU, E/S física e recursos de memória para cargas de trabalho de Python e R nos Serviços de Machine Learning do SQL Server.

Os algoritmos de aprendizado de máquina em Python e R têm uso intensivo de computação. Dependendo de suas prioridades de carga de trabalho, talvez seja necessário aumentar ou diminuir os recursos disponíveis para os Serviços de Machine Learning.

Para ver informações mais gerais, confira [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).

> [!NOTE] 
> O Resource Governor é um recurso da Edição Enterprise.

## <a name="default-allocations"></a>Alocações padrão

Por padrão, os runtimes de script externo para aprendizado de máquina são limitados a não mais do que 20% da memória total do computador. Isso depende do seu sistema, mas, em geral, você pode achar esse limite inadequado para tarefas de aprendizado de máquina sérias, como treinar um modelo ou prever muitas linhas de dados. 

## <a name="manage-resources-with-resource-governor"></a>Gerenciar recursos com o Resource Governor
 
Por padrão, os processos externos usam até 20% da memória total do host no servidor local. É possível modificar o pool de recursos padrão para fazer alterações em todo o servidor com processos de R e Python e usando qualquer capacidade que você disponibilizar para processos externos.

Como opção, você pode criar **pools de recursos externos** personalizados, com grupos de carga de trabalho e classificadores associados, a fim de determinar a alocação de recurso para solicitações provenientes de programas, hosts ou outros critérios específicos que você definir. Um pool de recursos externos é um tipo de pool de recursos introduzido no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] para ajudar a gerenciar os processos de R e Python externos ao mecanismo de banco de dados.

1. [Habilite a governança de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) (ela está desativada por padrão).

2. Execute [CREATE EXTERNAL RESOURCE POOL](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) para criar e configurar o pool de recursos, seguido por [ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) para implementá-lo.

3. Crie um grupo de carga de trabalho para alocações granulares, por exemplo, entre treinamento e pontuação.

4. Crie um classificador para interceptar chamadas para processamento externo.

5. Execute consultas e procedimentos usando os objetos que você criou.

Para ver as instruções do passo a passo, confira [Criar um pool de recursos para os Serviços de Machine Learning do SQL Server](create-external-resource-pool.md).

Para ver uma introdução à terminologia e conceitos gerais, confira [Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="processes-under-resource-governance"></a>Processos sob governança de recursos
  
 Você pode usar um *pool de recursos externos* para gerenciar os recursos usados pelos seguintes executáveis em uma instância do mecanismo de banco de dados:

+ Rterm.exe quando chamado localmente do SQL Server ou chamado remotamente com o SQL Server como o contexto de computação remota
+ Python.exe quando chamado localmente do SQL Server ou chamado remotamente com o SQL Server como o contexto de computação remota
+ BxlServer.exe e processos satélite
+ Processos de satélite iniciados pelo Launchpad, como PythonLauncher.dll
  
> [!NOTE]
> Não há suporte para o gerenciamento direto do serviço Launchpad por meio do Resource Governor. O Launchpad é um serviço confiável que só pode hospedar iniciadores desenvolvidos pela Microsoft. Inicializadores confiáveis também são configurados explicitamente para evitar o consumo excessivo de recursos.
  
## <a name="next-steps"></a>Próximas etapas

+ [Criar um pool de recursos para o aprendizado de máquina](create-external-resource-pool.md)
+ [Pools de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
