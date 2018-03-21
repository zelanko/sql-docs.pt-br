---
title: "SQL Server Machine Learning Services - disponibilidade de recursos entre edições | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2018
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
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 4322211bcc3a5466976368b9562ed3e95ad7e331
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/21/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>Disponibilidade de recursos em edições de serviços de aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 Recursos de aprendizagem de máquina estão disponíveis no SQL Server 2016 e 2017 do SQL Server. Este artigo lista as edições fornecendo o recurso, descreve as limitações que se aplicam em edições específicas e lista os recursos disponíveis apenas em algumas edições.


## <a name="sql-server-2017-machine-learning-features"></a>Recursos de aprendizagem de máquina do SQL Server de 2017

Edições Enterprise e Developer têm a mesma cobertura de recurso para que você possa criar soluções para uma instalação corporativa sem incorrer no custo mesmo. Embora as edições são funcionalmente equivlanet, o uso da edição de desenvolvedor não há suporte para ambientes de produção.

A diferença entre a integração básica e avançada é a escala. Integração avançada pode usar todos os núcleos disponíveis para o processamento paralelo de conjuntos de dados de qualquer tamanho de que seu computador pode acomodar. A integração básica é limitada a 2 núcleos e conjuntos de dados ajuste na memória. 

Integração básica e avançada se aplica às instâncias (no banco de dados). Um servidor autônomo não é um recurso de instância do mecanismo de banco de dados e é oferecido como uma opção de instalação somente nas edições Developer e Enterprise.

|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Integração básica do R|Sim|Sim|Sim|Sim|não|   
|Integração avançada do R|Sim|Não|Não|Não|não| 
|Integração Básica do Python|Sim|Sim|Sim|Sim|não|
|Integração Avançada do Python|Sim|Não|Não|Não|não| 
|Servidor do Machine Learning (Autônomo)|Sim|Não|Não|Não|não|   

 > [!NOTE]
 > Somente um servidor (autônomo) oferece o [operacionalização](https://docs.microsoft.com/machine-learning-server/what-is-operationalization) recursos que estão incluídos em uma instalação Microsoft (sem SQL-marca) R Server ou servidor de aprendizado de máquina. Operacionalização inclui a implantação do serviço web e recursos de hospedagem.
>
> Para uma instalação (no banco de dados), a abordagem equivalente para operacionalização de soluções é aproveitando os recursos do mecanismo de banco de dados, quando você converte o código para uma função que pode ser executados em um procedimento armazenado.


## <a name="sql-server-2016-r-features"></a>Recursos do SQL Server 2016 R

SQL Server 2016 inclui apenas a integração de R. No SQL Server 2016, a integração do R básica e avançada são equivalentes a 2017 do SQL Server.

## <a name="r-feature-availability-in-azure-sql-database"></a>Disponibilidade de recursos de R no banco de dados do SQL Azure
  
Depois de uma versão de teste inicial, R Services foi removido do banco de dados SQL Azure, pendente desenvolvimento adicional. 

## <a name="performance-expectations-for-enterprise-edition"></a>Expectativas de desempenho para o Enterprise Edition

Desempenho das soluções de aprendizado de máquina em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera geralmente superam implementações usando R convencional, dado o mesmo hardware. Que é porque, no SQL Server, as soluções de R podem ser executadas usando recursos do servidor e, às vezes, são distribuídas para vários processos usando o **RevoScaleR** funções. 

Os usuários também podem esperar ver diferenças consideráveis no desempenho e escalabilidade para o mesmo computador, solução de aprendizado se executar no vs Enterprise Edition. Standard Edition. Motivos incluem suporte para paralela maiores threads disponíveis para aprendizado de máquina, processamento e streaming (ou agrupamento), que permite que as funções de RevoScaleR lidar com mais dados do que pode caber na memória. 

No entanto, o desempenho mesmo em hardware idêntico pode ser afetado por vários fatores fora do código R ou Python. Esses fatores incluem concorrentes demandas de recursos do servidor, o tipo de plano de consulta que é criado, as alterações de esquema, a necessidade de atualizar estatísticas ou criar um novo plano de consulta, fragmentação e muito mais. É possível que um procedimento armazenado contendo código R ou Python pode ser executado em segundos em uma carga de trabalho, mas levar minutos, se houver outros serviços em execução.  Portanto, é recomendável que você monitore vários aspectos de desempenho do servidor, incluindo a rede para contextos de computação remota, ao avaliar o desempenho de aprendizado de máquina.

Também é recomendável que você configure [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) (disponível na edição Enterprise) para personalizar a maneira que os trabalhos de script externo são priorizados ou tratados sob cargas de trabalho excessiva no servidor. Você pode definir funções de classificação para especificar a origem do trabalho de script externo e priorizar determinadas cargas de trabalho, para limitar a quantidade de memória usada pelas consultas SQL e controlar o número de processos paralelos usados em uma base de carga de trabalho.

## <a name="see-also"></a>Consulte também

+ [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [Edições e componentes do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [Dicas sobre computação com grandes dados em R (servidor de aprendizado de máquina)](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
