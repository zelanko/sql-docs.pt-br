---
title: O que é a instância mestre?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve a função de instância mestre do SQL Server em um cluster de Big Data do SQL Server 2019 (versão prévia).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cafc62e12bcecad1ac6bcf389b87c864576c83a3
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958709"
---
# <a name="what-is-the-master-instance-in-a-sql-server-big-data-cluster"></a>O que é a instância mestre em um cluster de Big Data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve a função da *instância mestre do SQL Server* em um cluster de Big Data do SQL Server 2019. A instância mestre é uma instância do SQL Server em execução em um [plano de controle](big-data-cluster-overview.md#controlplane) do cluster de Big Data do SQL Server.

A instância mestra do SQL Server fornece a seguinte funcionalidade:

## <a name="connectivity"></a>Conectividade

A instância mestre do SQL Server fornece um ponto de extremidade do TDS acessível externamente para o cluster. Você pode conectar aplicativos ou ferramentas do SQL Server, como o Azure Data Studio ou o SQL Server Management Studio, a esse ponto de extremidade, assim como faria com qualquer outra instância do SQL Server.

## <a name="scale-out-query-management"></a>Gerenciamento de consulta de expansão

A instância mestre do SQL Server contém o mecanismo de consulta de expansão usado para distribuir consultas entre instâncias do SQL Server em nós no [pool de computação](concept-compute-pool.md). O mecanismo de consulta de expansão também fornece acesso por meio do Transact-SQL a todas as tabelas de Hive no cluster sem nenhuma configuração adicional.

## <a name="metadata-and-user-databases"></a>Bancos de dados de metadados e do usuário

Além dos bancos de dados do sistema do SQL Server padrão, a instância mestre do SQL também contém o seguinte:

- Um banco de dados de metadados que contém metadados da tabela do HDFS
- Um mapa de fragmentos do plano de dados
- Detalhes de tabelas externas que fornecem acesso ao plano de dados do cluster.
- Fontes de dados externas do PolyBase e tabelas externas definidas em bancos de dado do usuário.

Você também pode optar por adicionar seus próprios bancos de dados do usuário à instância mestra do SQL Server.

## <a name="machine-learning-services"></a>Serviços de aprendizado de máquina

Os serviços de aprendizado de máquina do SQL Server são um recurso complementar ao mecanismo de banco de dados, usados para executar código Java, R e Python no SQL Server. Esse recurso se baseia na estrutura de extensibilidade do SQL Server, que isola processos externos dos processos principais do mecanismo, mas se integra totalmente com os dados relacionais como procedimentos armazenados, como um script de T-SQL contendo instruções em R ou em Python ou como código Java, R ou Python que contém T-SQL.

Como parte de um cluster de Big Data do SQL Server, os serviços de aprendizado de máquina estarão disponíveis na instância mestre do SQL Server por padrão. Isso significa que, uma vez que a execução de script externo esteja habilitada na instância mestre do SQL Server, será possível executar scripts de Java, R e Python usando sp_execute_external_script.

### <a name="advantages-of-machine-learning-services-in-a-big-data-cluster"></a>Vantagens dos serviços de aprendizado de máquina em um cluster de Big Data

O SQL Server 2019 facilita o ingresso de Big Data nos dados dimensionais normalmente armazenados no banco de dados empresarial. O valor dos Big Data aumenta muito quando eles não estão apenas nas mãos de partes de uma organização, mas também estão incluídos em relatórios, painéis e aplicativos. Ao mesmo tempo, os cientistas de dados podem continuar usando as ferramentas do ecossistema do Spark/HDFS e ter acesso fácil e em tempo real aos dados na instância mestre do SQL Server e em fontes de dados externas acessíveis _por meio_ da instância mestre do SQL Server.

Com os clusters de Big Data do SQL Server 2019, você pode fazer mais com seus data lakes corporativos. Desenvolvedores e analistas do SQL Server podem:

* Criar aplicativos que consomem dados de data lakes corporativos.
* Explorar todos os dados com consultas Transact-SQL.
* Usar o ecossistema existente de ferramentas e aplicativos do SQL Server para acessar e analisar dados corporativos.
* Reduzir a necessidade de movimentação de dados por meio da virtualização de dados e de data marts.
* Continuar usando o Spark para cenários de Big Data.
* Criar aplicativos empresariais inteligentes usando o Spark ou o SQL Server para treinar modelos em data lakes.
* Operacionalizar modelos em bancos de dados de produção para obter o melhor desempenho.
* Transmitir dados diretamente para data marts corporativos para análise em tempo real.
* Explorar os dados visualmente usando ferramentas interativas de análise e BI.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de Big Data do SQL Server, confira os seguintes recursos:

- [O que são os clusters de Big Data do SQL Server 2019?](big-data-cluster-overview.md)
- [Workshop: Arquitetura de clusters de Big Data do Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
