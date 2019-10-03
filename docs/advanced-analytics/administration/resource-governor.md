---
title: Gerenciar cargas de trabalho do Python e do R com o Resource Governor
description: Saiba como usar Resource Governor para gerenciar a alocação de CPU, e/s física e recursos de memória para cargas de trabalho de Python e R em SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/02/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9000ab8bb15e8f9910b8b780aa38d134fa984032
ms.sourcegitcommit: af5e1f74a8c1171afe759a4a8ff2fccb5295270a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71823541"
---
# <a name="manage-python-and-r-workloads-with-resource-governor-in-sql-server-machine-learning-services"></a>Gerenciar cargas de trabalho do Python e do R com o Resource Governor no SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Saiba como usar [resource governor](../../relational-databases/resource-governor/resource-governor.md) para gerenciar a alocação de CPU, e/s física e recursos de memória para cargas de trabalho de Python e R em SQL Server serviços de Machine Learning.

Os algoritmos de aprendizado de máquina em Python e R normalmente são de computação intensiva. Dependendo de suas prioridades de carga de trabalho, talvez seja necessário aumentar ou diminuir os recursos disponíveis para Serviços de Machine Learning.

Para obter mais informações gerais, consulte [resource governor](../../relational-databases/resource-governor/resource-governor.md).

> [!NOTE] 
> O Resource Governor é um recurso de edição Enterprise.

## <a name="default-allocations"></a>Alocações padrão

Por padrão, os tempos de execução de script externo para Machine Learning são limitados a não mais do que 20% da memória total do computador. Depende do seu sistema, mas, em geral, você pode achar esse limite inadequado para tarefas de aprendizado de máquina sérias, como treinar um modelo ou prever muitas linhas de dados. 

## <a name="manage-resources-with-resource-governor"></a>Gerenciar recursos com Resource Governor
 
Por padrão, os processos externos usam até 20% da memória total do host no servidor local. Você pode modificar o pool de recursos padrão para fazer alterações em todo o servidor, com processos de R e Python utilizando qualquer capacidade que você disponibilizar para processos externos.

Como alternativa, você pode criar **pools de recursos externos**personalizados, com classificadores e grupos de carga de trabalho associados, para determinar a alocação de recursos para solicitações provenientes de programas, hosts ou outros critérios específicos que você fornecer. Um pool de recursos externos é um tipo de pool de recursos [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] introduzido no para ajudar a gerenciar os processos de R e Python externos ao mecanismo de banco de dados.

1. [Habilitar governança de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) (está desativado por padrão).

2. Execute [criar pool de recursos externos](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) para criar e configurar o pool de recursos, seguido por [ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) para implementá-lo.

3. Crie um grupo de cargas de trabalho para alocações granulares, por exemplo, entre treinamento e pontuação.

4. Crie um classificador para interceptar chamadas para processamento externo.

5. Execute consultas e procedimentos usando os objetos que você criou.

Para obter instruções, consulte [como criar um pool de recursos para scripts R e Python externos](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md) para obter informações passo a passo.

Para obter uma introdução à terminologia e conceitos gerais, consulte [resource governor pool de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="processes-under-resource-governance"></a>Processos sob governança de recursos
  
 Você pode usar um *pool de recursos externos* para gerenciar os recursos usados pelos seguintes executáveis em uma instância do mecanismo de banco de dados:

+ Rterm. exe quando chamado localmente de SQL Server ou chamado remotamente com SQL Server como o contexto de computação remota
+ Python. exe quando chamado localmente de SQL Server ou chamado remotamente com SQL Server como o contexto de computação remota
+ BxlServer.exe e processos satélite
+ Processos de satélite iniciados pelo Launchpad, como PythonLauncher. dll
  
> [!NOTE]
> Não há suporte para o gerenciamento direto do serviço Launchpad usando Resource Governor. O Launchpad é um serviço confiável que só pode hospedar iniciadores fornecidos pela Microsoft. Os iniciadores confiáveis são configurados explicitamente para evitar o consumo excessivo de recursos.
  
## <a name="next-steps"></a>Próximas etapas

+ [Criar um pool de recursos para o aprendizado de máquina](create-external-resource-pool.md)
+ [Resource Governor pools de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
