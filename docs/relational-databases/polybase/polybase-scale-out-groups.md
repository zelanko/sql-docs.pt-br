---
title: Grupos de escala horizontal do PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 53802a8a327c2e66810cd8f084d0ba297eb95426
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47629934"
---
# <a name="polybase-scale-out-groups"></a>Grupos de escala horizontal do PolyBase

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Uma instância do SQL Server autônoma com PolyBase pode se tornar um gargalo de desempenho ao lidar com grandes conjuntos de dados no Hadoop ou no Armazenamento de Blobs do Azure. O recurso Grupo do PolyBase permite a você criar um cluster de instâncias do SQL Server para processar grandes conjuntos de dados de fontes de dados externas, como Hadoop e Armazenamento de Blobs do Azure, de maneira escalar horizontal para melhor desempenho de consulta. Agora, você pode dimensionar sua computação no SQL Server para atender às demandas de desempenho de sua carga de trabalho. Grupos de expansão do PolyBase, um grupo de instâncias do SQL Server, permitem processar grandes conjuntos de dados externos em uma arquitetura de processamento paralelo. O desempenho de consulta e carregamento de dados pode aumentar de modo linear conforme você adiciona mais instâncias do SQL Server ao grupo. 
  
Veja [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md) e [Guia do PolyBase](../../relational-databases/polybase/polybase-guide.md).
  
![Grupos de escala horizontal do PolyBase](../../relational-databases/polybase/media/polybase-scale-out-groups.png "Grupos de escala horizontal do PolyBase")  
  
## <a name="head-node"></a>Nó de cabeçalho  

O nó de cabeçalho contém a instância do SQL Server para a qual as consultas do PolyBase são enviadas. Cada grupo do PolyBase pode ter apenas um nó de cabeçalho. Um nó de cabeçalho é um grupo lógico do Mecanismo de Banco de Dados do SQL, do Mecanismo de PolyBase e do Serviço de Movimentação de Dados de PolyBase na instância do SQL Server.
  
## <a name="compute-node"></a>Nó de computação  

Um nó de computação contém a instância do SQL Server que auxilia no processamento de consulta de escala horizontal de dados externos. Um nó de cabeçalho é um grupo lógico do SQL Server e do serviço de movimentação de dados de PolyBase na instância do SQL Server. Um grupo do PolyBase pode ter vários nós de computação. O nó principal e os nós de computação devem executar a mesma versão do SQL Server.

## <a name="scale-out-reads"></a>Leituras de expansão

Ao consultar instâncias externas do SQL Server, do Oracle ou do Teradata, as tabelas de partição serão beneficiadas por leituras de expansão. Cada nó em um grupo de expansão do PolyBase pode criar até 8 leitores para ler dados externos. E a cada leitor é atribuída uma partição para ler na tabela externa. 

Por exemplo, digamos que você tenha uma tabela externa do SQL Server com 12 partições mensais e um grupo expansão do PolyBase com 3 nós; cada nó usará 4 leitores do PolyBase para processar cada uma das 12 partições. Isso é ilustrado na imagem a seguir. 

> [!NOTE]
 isso é diferente das leituras de expansão no Hadoop. 

![Grupos de escala horizontal do PolyBase](../../relational-databases/polybase/media/polybase-scale-out-groups2.png "Grupos de escala horizontal do PolyBase")
  
## <a name="distributed-query-processing"></a>Processamento de consulta distribuída  

As consultas do PolyBase são enviadas ao SQL Server no nó de cabeçalho. A parte da consulta que se refere a tabelas externas é entregue ao mecanismo de PolyBase.
  
O mecanismo de PolyBase é o componente principal por trás das consultas do PolyBase. Ele analisa a consulta em dados externos, gera o plano de consulta e distribui o trabalho para o serviço de movimentação de dados em nós de computação para execução. Após a conclusão do trabalho, ele recebe os resultados dos nós de computação e os envia para o SQL Server para processamento e retorno ao cliente.
  
O serviço de movimentação de dados do PolyBase recebe instruções do mecanismo do PolyBase e transfere dados entre o HDFS e o SQL Server, e entre instâncias do SQL Server nos nós de cabeçalho e computação.
  
## <a name="editions-availability"></a>Disponibilidade de edições  

Após a instalação do SQL Server, a instância poderá ser designada como um nó de cabeçalho ou um nó de computação. A escolha depende da versão em que o PolyBase do SQL Server está em execução. Em uma instalação da edição Enterprise, a instância pode ser designada como nó de cabeçalho ou nó de computação. Em uma edição Standard, a instância pode ser designada apenas como um nó de computação.

## <a name="next-steps"></a>Próximas etapas

Para configurar um grupo expansão do PolyBase, consulte o guia a seguir:

[Aprimorar grupos expansão do PolyBase no Windows](configure-scale-out-groups-windows.md)
