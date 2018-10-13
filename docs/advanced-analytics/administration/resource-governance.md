---
title: Governança de recursos para o aprendizado de máquina no SQL Server | Microsoft Docs
description: Alocar memória RAM, CPU e e/s para cargas de trabalho de R e Python na instância de mecanismo de banco de dados do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 76b6af9ccf6fc3c5a54f4cb8be3fe7068eb578b5
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100547"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>Governança de recursos para o aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Algoritmos de aprendizado de máquina e ciência de dados são computacionalmente intensivas. Dependendo das prioridades de carga de trabalho, talvez seja necessário aumentar os recursos disponíveis para ciência de dados ou diminuição de recursos se a execução do script R e Python prejudica o desempenho de outros serviços em execução simultaneamente. 

Quando você precisa balancear novamente a distribuição de recursos do sistema em várias cargas de trabalho, você pode usar [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) para alocar a CPU, e/s física e os recursos de memória consumidos pelos tempos de execução externos para R e Python. Se você mudar as alocações de recursos, lembre-se de que você talvez precise também reduzir a quantidade de memória reservada para outras cargas de trabalho e serviços. 

> [!NOTE] 
> Administrador de recursos é um recurso do Enterprise Edition.

## <a name="default-allocations"></a>Alocações padrão

Por padrão, os tempos de execução do script externo para o machine learning são limitados a não mais de 20% da memória total do computador. Ele depende do seu sistema, mas em geral, você pode encontrar esse limite inadequado para tarefas de aprendizado de máquina graves, como um modelo de treinamento ou para prever em várias linhas de dados. 

## <a name="use-resource-governor-to-control-resourcing"></a>Usar o Resource Governor para controlar a alocação de recursos
 
Por padrão, os processos externos usam até 20% da memória total do host no servidor local. Você pode modificar o pool de recursos padrão para fazer alterações em todo o servidor, com o R e processos de Python utilizando qualquer capacidade que você disponibilizar para processos externos.

Como alternativa, você pode construir personalizado *pools de recursos externos*, com grupos de carga de trabalho associada e classificadores, para determinar a alocação de recurso para solicitações provenientes de programas específicos, hosts ou outros critérios que Você pode fornecer. Um pool de recursos externo é um tipo de pool de recursos introduzido no [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] para ajudar a gerenciar os processos de R e Python externos ao mecanismo de banco de dados.

1. [Habilitar a governança de recursos](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) (ele está desativado por padrão).

2. Execute [CREATE EXTERNAL RESOURCE POOL](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) para criar e configurar o pool de recursos, seguido por [ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) implementá-lo.

3. Crie um grupo de carga de trabalho para alocações granulares, por exemplo, entre treinamento e pontuação.

4. Crie um classificador para interceptar chamadas para processamento externo.

5. Executar consultas e procedimentos usando os objetos que você criou.

Para obter instruções, consulte [como criar um pool de recursos para os scripts de R e Python externos](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md) para obter instruções passo a passo.

Para obter uma introdução à terminologia e conceitos gerais, consulte [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="processes-under-resource-governance"></a>Processos de governança de recursos
  
 Você pode usar um *pool de recursos externos* para gerenciar os recursos usados pelos executáveis em uma instância do mecanismo de banco de dados a seguir:

+ Rterm.exe quando chamado localmente do SQL Server ou chamado remotamente com o SQL Server como o contexto de computação remota
+ Python.exe quando chamado localmente do SQL Server ou chamado remotamente com o SQL Server como o contexto de computação remota
+ BxlServer.exe e processos satélite
+ Processos satélite iniciados pelo Launchpad, como PythonLauncher.dll
  
> [!NOTE]
> Não há suporte para o gerenciamento direto de serviço Launchpad pelo administrador de recursos. Barra inicial é um serviço confiável que pode somente os iniciadores de host fornecidos pela Microsoft. Inicializadores confiáveis são configurados explicitamente para evitar o consumo excessivo de recursos.
  
## <a name="see-also"></a>Confira também

+ [Gerenciar integração de aprendizado de máquina](../r/managing-and-monitoring-r-solutions.md)
+ [Criar um pool de recursos para o aprendizado de máquina](../r/how-to-create-a-resource-pool-for-r.md)
+ [Pools de recursos do administrador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
