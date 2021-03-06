---
title: Grupos de escala horizontal do PolyBase | Microsoft Docs
description: Use o recurso de Grupo do PolyBase para criar um cluster de instâncias do SQL Server. Isso aprimora o desempenho de consulta para grandes conjuntos de dados de fontes externas.
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sql13.swb.polybasescaleoutcluster.page.f1
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016'
ms.openlocfilehash: 3928d00a2b72c4d1484fa8b30ca579a5af0ef34c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97416337"
---
# <a name="polybase-scale-out-groups"></a>Grupos de escala horizontal do PolyBase

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Uma instância do SQL Server autônoma com PolyBase pode se tornar um gargalo de desempenho ao lidar com grandes conjuntos de dados no Hadoop ou no Armazenamento de Blobs do Azure. O recurso Grupo do PolyBase permite a você criar um cluster de instâncias do SQL Server para processar grandes conjuntos de dados de fontes de dados externas, como Hadoop e Armazenamento de Blobs do Azure, de maneira escalar horizontal para melhor desempenho de consulta. Agora, você pode dimensionar sua computação no SQL Server para atender às demandas de desempenho de sua carga de trabalho. Grupos de expansão do PolyBase, um grupo de instâncias do SQL Server, permitem processar grandes conjuntos de dados externos em uma arquitetura de processamento paralelo. O desempenho de consulta e carregamento de dados pode aumentar de modo linear conforme você adiciona mais instâncias do SQL Server ao grupo. 
  
Veja [Introdução ao PolyBase](./polybase-guide.md) e [Guia do PolyBase](../../relational-databases/polybase/polybase-guide.md).
  
![Diagrama que mostra grupos de expansão do PolyBase.](../../relational-databases/polybase/media/polybase-scale-out-groups.png "Grupos de escala horizontal do PolyBase")  
  
## <a name="head-node"></a>Nó de cabeçalho  

O nó de cabeçalho contém a instância do SQL Server para a qual as consultas do PolyBase são enviadas. Cada grupo do PolyBase pode ter apenas um nó de cabeçalho. Um nó de cabeçalho é um grupo lógico do Mecanismo de Banco de Dados do SQL Server, do Mecanismo de PolyBase e do Serviço de Movimentação de Dados PolyBase na instância do SQL Server. Com o SQL Server 2017 e 2016, o nó principal deve ser da Edição Enterprise. A partir do SQL Server 2019, o nó principal do PolyBase pode ser de uma edição Enterprise ou Standard.
  
## <a name="compute-node"></a>Nó de computação

Um nó de computação contém a instância do SQL Server que auxilia no processamento de consulta de escala horizontal de dados externos. Um nó de cabeçalho é um grupo lógico do SQL Server e do serviço de movimentação de dados de PolyBase na instância do SQL Server. Um grupo do PolyBase pode ter vários nós de computação. O nó principal e os nós de computação devem executar a mesma versão do SQL Server. A versão inicial do SQL Server 2016 permitia que os nós de computação fossem de uma edição Enterprise ou Standard. A partir do SQL Server 2016 SP1, todas as edições do SQL Server podem ser um nó de computação.

## <a name="scale-out-reads"></a>Leituras de expansão

Ao consultar instâncias externas do SQL Server, do Oracle ou do Teradata, as tabelas de partição serão beneficiadas por leituras de expansão. Cada nó em um grupo de expansão do PolyBase pode criar até 8 leitores para ler dados externos. E a cada leitor é atribuída uma partição para ler na tabela externa. 

Por exemplo, digamos que você tenha uma tabela externa do SQL Server com 12 partições mensais e um grupo expansão do PolyBase com 3 nós; cada nó usará 4 leitores do PolyBase para processar cada uma das 12 partições. Isso é ilustrado na imagem a seguir. 

> [!NOTE]
>  isso é diferente das leituras de expansão no Hadoop. 

![Leituras de expansão do PolyBase](../../relational-databases/polybase/media/polybase-scale-out-groups2.png "Grupos de escala horizontal do PolyBase")
  
## <a name="distributed-query-processing"></a>Processamento de consulta distribuída  

As consultas do PolyBase são enviadas ao SQL Server no nó de cabeçalho. A parte da consulta que se refere a tabelas externas é entregue ao mecanismo de PolyBase.
  
O mecanismo de PolyBase é o componente principal por trás das consultas do PolyBase. Ele analisa a consulta em dados externos, gera o plano de consulta e distribui o trabalho para o serviço de movimentação de dados em nós de computação para execução. Após a conclusão do trabalho, ele recebe os resultados dos nós de computação e os envia para o SQL Server para processamento e retorno ao cliente.
  
O serviço de movimentação de dados do PolyBase recebe instruções do mecanismo do PolyBase e transfere dados entre o HDFS e o SQL Server, e entre instâncias do SQL Server nos nós de cabeçalho e computação.
  
## <a name="next-steps"></a>Próximas etapas

Para configurar um grupo expansão do PolyBase, consulte o guia a seguir:

[Aprimorar grupos expansão do PolyBase no Windows](configure-scale-out-groups-windows.md)

## <a name="see-also"></a>Consulte Também

 [sys-dm-exec-compute-nodes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)   
 [sys-dm-exec-compute-node-status](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)   
 [sys.dm_exec_compute_node_errors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)
