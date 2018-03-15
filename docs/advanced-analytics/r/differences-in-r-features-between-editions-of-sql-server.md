---
title: "SQL Server Machine Learning Services - disponibilidade de recursos entre edições | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 16ca6c44b15c9fb7c1983d5a04175ebbade57895
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>Disponibilidade de recursos em edições de serviços de aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 Recursos de aprendizagem de máquina estão disponíveis no SQL Server 2016 e 2017 do SQL Server. Este artigo lista as edições fornecendo o recurso, descreve as limitações que se aplicam em edições específicas e lista os recursos disponíveis apenas em algumas edições.

 > [!NOTE]
 > Em geral, o aprendizado de máquina do SQL Server (no banco de dados) não inclui o [operacionalização](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) recursos que estão incluídos em uma instalação de servidor de R ou servidor de aprendizado de máquina autônoma. Operacionalização inclui a implantação do serviço web e hospedagem e, portanto, compete para os mesmos recursos que outras operações do SQL Server.
 > 
 > Por esse motivo, é recomendável instalar o servidor do SQL Server 2016 R (autônomo) ou o servidor do aprendizado de máquina 2017 SQL Server (autônomo) em um servidor físico diferente para dar suporte à implantação de modelos de previsão como um serviço web. 

## <a name="sql-server-2017-machine-learning-services-in-database-and-standalone"></a>SQL (autônomo) e serviços de aprendizado de máquina do servidor de 2017 (no banco de dados)

A edição de desenvolvedor fornece desempenho equivalente do Enterprise Edition. Não há suporte para o uso da edição de desenvolvedor para ambientes de produção.

|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------|----------|--------|---|------------------------------|-------|
| O interpretador de R & proprietários pacotes | Sim | Sim | Não | Não | não | 
| Bibliotecas de cliente & interpretador do Python | Sim | Sim | Não | Não | não | 
| Agrupamento de dados <br/>(processar grandes quantidades de dados, excedendo o que couber na memória) | Sim | Não | Não | Não | não |
| Processamento de expansão <br/>(mais de 2 processadores) | Sim | Não | Não | Não | não |
| Operacionalização | Sim | Não | Não | Não | não |
| [PREVER](../../t-sql/queries/predict-transact-sql.md) função <br/>(executa [pontuação nativo](../sql-native-scoring.md) em um modelo previamente treinado, salvo anteriormente no formato binário necessário) | Sim | Sim | Sim | Sim | Sim |
| Compatibilidade de cliente de R | Sim | Sim | Não | Não | não | 
| Microsoft R Open | Sim | Sim | Não | Não | não | 
| Anaconda Python 3.5 | Sim | Sim | Não | Não | não | 

## <a name="sql-server-2016-r-services-in-database-and-r-server-standalone"></a>SQL Server 2016 R Services (no banco de dados) e R Server (autônomo)

Disponibilidade de recursos é igual a de 2017, menos suporte do Python que não fazia parte da versão 2016 primeiro.

## <a name="r-feature-availability-in-azure-sql-database"></a>Disponibilidade de recursos de R no banco de dados do SQL Azure
  
Depois de uma versão de teste inicial, os serviços de R está **não** disponíveis no banco de dados SQL Azure, pendente desenvolvimento adicional. 

## <a name="performance-expectations-for-enterprise-edition"></a>Expectativas de desempenho para o Enterprise Edition

Desempenho das soluções de aprendizado de máquina em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera geralmente superam implementações usando R convencional, dado o mesmo hardware. Que é porque, no SQL Server, as soluções de R podem ser executadas usando recursos do servidor e, às vezes, são distribuídas para vários processos usando o **RevoScaleR** funções. 

Desempenho não foi avaliado para soluções de Python, como o recurso ainda está em desenvolvimento, mas alguns dos mesmos benefícios podem ser aplicados.

Os usuários também podem esperar ver diferenças consideráveis no desempenho e escalabilidade para o mesmo computador, solução de aprendizado se executar no vs Enterprise Edition. Standard Edition. Motivos incluem suporte para paralela maiores threads disponíveis para aprendizado de máquina, processamento e streaming (ou agrupamento), que permite que as funções de RevoScaleR lidar com mais dados do que pode caber na memória. 

No entanto, o desempenho mesmo em hardware idêntico pode ser afetado por vários fatores fora do código R ou Python. Esses fatores incluem concorrentes demandas de recursos do servidor, o tipo de plano de consulta que é criado, as alterações de esquema, a necessidade de atualizar estatísticas ou criar um novo plano de consulta, fragmentação e muito mais. É possível que um procedimento armazenado contendo código R ou Python pode ser executado em segundos em uma carga de trabalho, mas levar minutos, se houver outros serviços em execução.  Portanto, é recomendável que você monitore vários aspectos de desempenho do servidor, incluindo a rede para contextos de computação remota, ao avaliar o desempenho de aprendizado de máquina.

Também é recomendável que você configure [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) (disponível na edição Enterprise) para personalizar a maneira que os trabalhos de script externo são priorizados ou tratados sob cargas de trabalho excessiva no servidor. Você pode definir funções de classificação para especificar a origem do trabalho de script externo e priorizar determinadas cargas de trabalho, para limitar a quantidade de memória usada pelas consultas SQL e controlar o número de processos paralelos usados em uma base de carga de trabalho.

## <a name="see-also"></a>Consulte também

+ [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [Edições e componentes do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [Dicas sobre computação com grandes dados em R (servidor de aprendizado de máquina)](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
