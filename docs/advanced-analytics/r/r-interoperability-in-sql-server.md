---
title: Interoperabilidade de R no SQL Server R Services | Microsoft Docs
ms.custom: 
ms.date: 07/11/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0506b950-34b3-4f11-8e2f-d067a58015bd
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e393db396c7d41f7eca7851fa10544d697eac5c8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="r-interoperability-in-sql-server"></a>Interoperabilidade de R no SQL Server

Este tópico enfoca o mecanismo de execução de R no SQL Server e descreve as diferenças entre o Microsoft R e software livre R.

Aplica-se a: SQL Server 2016 R Services, SQL Server 2017 serviços de aprendizado de máquina

Para obter informações sobre os componentes adicionais, consulte [novos componentes do SQL Server](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md).

### <a name="open-source-r-components"></a>Componentes de software livre R

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] inclui uma distribuição completa dos pacotes R de base e ferramentas. Para obter mais informações sobre o que está incluído na distribuição de base, consulte a documentação instalada durante a instalação no seguinte local padrão: `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`

Como parte da instalação do [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], você deve concordar com os termos da Licença Pública de GNU. Depois disso, você poderá executar pacotes R padrão sem modificações adicionais como faria em qualquer outra distribuição de software livre de R.

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] não modifica o tempo de execução de R de nenhuma maneira. O tempo de execução de R é executado fora do processo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e pode ser executado independentemente de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. No entanto, é altamente recomendável que você não execute essas ferramentas enquanto [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] está usando R, para evitar contenção de recursos.

A distribuição de pacote base de R que está associada a uma determinada instância [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] pode ser encontrada na pasta associada à instância. Por exemplo, se você instalou o R Services na instância padrão, as bibliotecas de R estão localizadas na pasta por padrão:

    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library

Da mesma forma, as ferramentas de R associadas com a instância padrão deve estar localizadas na pasta de est por padrão:

    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin

Para obter mais informações sobre como o Microsoft R é diferente de uma distribuição de base de R que você pode obter de CRAN, consulte [interoperabilidade com produtos Microsoft R e recursos e linguagem R](https://docs.microsoft.com/en-us/r-server/what-is-r-server-interoperability)

### <a name="additional-r-packages-from-microsoft-r"></a>Pacotes R adicionais da Microsoft R

Além da distribuição de R base, [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] inclui alguns pacotes de R proprietárias, bem como uma estrutura para execução paralela de R que também dá suporte à execução de R em contextos de computação remota.

Esse conjunto combinado de recursos de R – a distribuição de base de R mais os recursos aprimorados e pacotes de R – é chamado de **Microsoft R**. Se você instalar o Microsoft R Server (autônomo), obterá exatamente o mesmo conjunto de pacotes que é instalado com o SQL Server R Services (no banco de dados), mas em uma pasta diferente.

O Microsoft R inclui uma distribuição da biblioteca Intel Math Kernel, que é usada sempre que possível para processamento matemático mais rápido. Por exemplo, a biblioteca de álgebra linear básica (BLAS) é usada para muitos pacotes complementares, bem como para o R em si. Para obter mais informações, consulte estes tópicos:

+ [Como o Intel Math Kernel acelera o R](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html)
+ [Benefícios de desempenho da vinculação de R a bibliotecas matemáticas multithread](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html)

Entre as adições mais importantes do Microsoft R, estão os pacotes **RevoScaleR** e **RevoPemaR**. Esses são os pacotes de R que foram escritos primariamente em C ou C++ para melhorar o desempenho.

+ **RevoScaleR.** Inclui uma variedade de APIs para análise e manipulação de dados. As APIs foram otimizadas para analisar conjuntos de dados que são grandes demais para caber na memória e executar cálculos distribuídos em vários processadores ou núcleos.

   As APIs de RevoScaleR também dão suporte ao trabalho com subconjuntos de dados para maior escalabilidade. Em outras palavras, a maioria das funções do RevoScaleR pode operar em blocos de dados e usar algoritmos de atualização para agregar os resultados. Portanto, soluções de R baseadas nas funções de RevoScaleR podem trabalhar com conjuntos de dados muito grandes e não são limitados pela memória local.

  O pacote de RevoScaleR também dá suporte ao formato de arquivo XDF para movimentação e armazenamento de dados usados para análise mais rápidos. O formato XDF usa armazenamento colunar, é portátil e pode ser usado para carregar e manipular dados de várias fontes, incluindo texto, SPSS ou uma conexão ODBC. 

+ **RevoPemaR.** PEMA significa Algoritmo Paralelo de Memória Externa (Parallel External Memory Algorithm). O pacote **RevoPemaR** fornece APIs que podem ser usadas para desenvolver seus próprios algoritmos paralelos. Para obter mais informações, consulte [Guia de introdução ao RevoPemaR](https://docs.microsoft.com/r-server/r/how-to-developer-pemar).

Também é recomendável que você tente [MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package), um novo pacote de R da Microsoft que oferece suporte à execução remota de código R e escalonável, processamento, distribuído usar algoritmos de aprendizado de máquina aprimorada desenvolvida pela Microsoft Research.

## <a name="next-steps"></a>Próximas etapas

[Visão geral da arquitetura](../../advanced-analytics/r/architecture-overview-sql-server-r.md)

[Componentes do SQL Server para dar suporte a R](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md)

[Visão geral de segurança](../../advanced-analytics/r/security-overview-sql-server-r.md)

