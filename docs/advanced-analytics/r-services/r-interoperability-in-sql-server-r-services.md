---
title: "Interoperabilidade de R no SQL Server R Services | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0506b950-34b3-4f11-8e2f-d067a58015bd
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Interoperabilidade de R no SQL Server R Services

Este tópico enfoca o mecanismo de execução para R em [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], e descreve as diferenças entre o Microsoft R e código-fonte aberto R. Para obter informações sobre os componentes adicionais, consulte [novos componentes do SQL Server](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md).

### Componentes de software livre R

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] inclui uma distribuição completa dos pacotes de R base e ferramentas. Para obter mais informações sobre o que está incluído com a distribuição de base, consulte a documentação instalada durante a instalação no seguinte local padrão:
`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`

Como parte da instalação do [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], você deve concordar com os termos da licença pública GNU. Depois disso, você pode executar pacotes R padrão sem modificações adicionais como faria em qualquer outra distribuição do código-fonte aberto de R.

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Não modifique o tempo de execução de R de qualquer forma. O tempo de execução de R é executado fora do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] processar e pode ser executado independentemente da [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. No entanto, é altamente recomendável que você não executar essas ferramentas enquanto [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] está usando R, para evitar contenção de recursos.

A distribuição de pacote básico de R que está associada um determinado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instância pode ser encontrada na pasta associada à instância. Por exemplo, se você instalou os serviços de R na instância padrão, as bibliotecas de R estão localizadas em `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`.

Da mesma forma, as ferramentas de R associadas com a instância padrão deve estar localizadas no `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`,

Para obter mais informações sobre a distribuição de base, consulte [pacotes instalados com o Microsoft R Open](https://mran.revolutionanalytics.com/rro/installed/)

### Pacotes R adicionais

Além da distribuição de R base, [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] inclui alguns pacotes de R proprietárias, bem como uma estrutura para execução paralela de R e bibliotecas que oferece suporte à execução de R em contextos de computação remota. 

Esse conjunto combinado de recursos de R - a distribuição de base de R mais os recursos aprimorados de R e pacotes - é referido como **Microsoft R**. Se você instalar o Microsoft R Server (autônomo), você obterá exatamente o mesmo conjunto de pacotes que são instalados com o SQL Server R Services (no banco de dados), mas em uma pasta diferente. 

Microsoft R inclui uma distribuição da biblioteca de Kernel de matemática Intel, que é usado sempre que possível para processamento mais rápido na matemático. Por exemplo, a biblioteca de álgebra linear básicos (BLAS) é usada para muitos pacotes complementares, bem como para R em si. Para obter mais informações, consulte estes artigos:

+ [Como o Kernel de matemática Intel acelera R](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html)
+ [Benefícios de desempenho da vinculação R para bibliotecas matemáticas multithread](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html)

Entre as adições mais importantes Microsoft r estão o **RevoScaleR** e **RevoPemaR** pacotes. Esses são os pacotes de R que foram gravados amplamente em C ou C++ para melhorar o desempenho.

+ **RevoScaleR.** Inclui uma variedade de APIs para análise e manipulação de dados. As APIs foram otimizadas para analisar conjuntos de dados que são muito grandes para caber na memória e executar cálculos distribuídos em vários processadores ou núcleos.

   As APIs RevoScaleR também oferecem suporte ao trabalho com subconjuntos de dados para maior escalabilidade. Em outras palavras, a maioria das funções de RevoScaleR pode operar em blocos de dados e use a atualização de algoritmos para agregar resultados. Portanto soluções R baseadas nas funções de RevoScaleR podem trabalhar com grandes conjuntos de dados e não são associadas por memória local.

  O pacote de RevoScaleR também oferece suporte a. Formato de arquivo XDF para movimentação e armazenamento de dados usados para análise mais rápida. O formato XDF usa armazenamento Colunar, é portátil e pode ser usado para carregar e manipular dados de várias fontes, incluindo texto, SPSS ou uma conexão ODBC. Um exemplo de como usar o formato XDF é fornecido neste tutorial: [aprofundamento de ciência de dados](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)


+ **RevoPemaR.** PEMA representa o algoritmo paralelo de memória externa. O **RevoPemaR** pacote fornece APIs que você pode usar para desenvolver seus próprios algoritmos paralelos. Para obter mais informações, consulte [RevoPemaR Getting Started Guide](https://msdn.microsoft.com/microsoft-r/rserver/rserver-pemar-getting-started).

## Consulte também
[Visão geral sobre arquitetura](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)

[Novos componentes do SQL Server para oferecer suporte a serviços de R](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)

[Visão geral de segurança](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)
