---
title: Governança de recursos para execução de script R e Python
description: Aloque memória RAM, CPU e e/s para cargas de trabalho R e Python em SQL Server instância do mecanismo de banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 55a83e7e63a4e43afe1168aab3307f2806a55fca
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715258"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>Governança de recursos para aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Os algoritmos de ciência de dados e de aprendizado de máquina são computacionalmente intensivos. Dependendo das prioridades de carga de trabalho, talvez seja necessário aumentar os recursos disponíveis para a ciência de dados ou diminuir a origem se a execução do script R e Python subminar o desempenho de outros serviços em execução simultaneamente. 

Quando você precisa reequilibrar a distribuição de recursos do sistema em várias cargas de trabalho, você pode usar [resource governor](../../relational-databases/resource-governor/resource-governor.md) para alocar CPU, e/s física e recursos de memória consumidos pelos tempos de execução externos para R e Python. Se você mudar as alocações de recursos, lembre-se de que talvez seja necessário reduzir também a quantidade de memória reservada para outras cargas de trabalho e serviços. 

> [!NOTE] 
> O Resource Governor é um recurso de edição Enterprise.

## <a name="default-allocations"></a>Alocações padrão

Por padrão, os tempos de execução de script externo para Machine Learning são limitados a não mais do que 20% da memória total do computador. Depende do seu sistema, mas, em geral, você pode achar esse limite inadequado para tarefas de aprendizado de máquina sérias, como treinar um modelo ou prever muitas linhas de dados. 

## <a name="use-resource-governor-to-control-resourcing"></a>Usar Resource Governor para controlar a insourcing
 
Por padrão, os processos externos usam até 20% da memória total do host no servidor local. Você pode modificar o pool de recursos padrão para fazer alterações em todo o servidor, com processos de R e Python utilizando qualquer capacidade que você disponibilizar para processos externos.

Como alternativa, você pode construir pools de *recursos externos*personalizados, com classificadores e grupos de carga de trabalho associados, para determinar a alocação de recursos para solicitações provenientes de programas, hosts ou outros critérios específicos que você fornecer. Um pool de recursos externos é um tipo de pool de recursos [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] introduzido no para ajudar a gerenciar os processos de R e Python externos ao mecanismo de banco de dados.

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
  
## <a name="see-also"></a>Confira também

+ [Gerenciar a integração do Machine Learning](../r/managing-and-monitoring-r-solutions.md)
+ [Criar um pool de recursos para o aprendizado de máquina](../r/how-to-create-a-resource-pool-for-r.md)
+ [Resource Governor pools de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
