---
title: O que é a instância mestre?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve a instância mestre do SQL Server em um cluster de big data do SQL Server 2019 (visualização).
author: rothja
ms.author: jroth
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 6c3a9a425d5de55e7018c9e33b37a8e3d1a8e1c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66783079"
---
# <a name="what-is-the-master-instance-in-a-sql-server-big-data-cluster"></a>O que é a instância mestre em um cluster de big data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve a função dos *instância mestre do SQL Server* em um cluster de big data do SQL Server de 2019. A instância mestre é uma instância do SQL Server em execução em um cluster de big data do SQL Server [plano de controle](big-data-cluster-overview.md#controlplane).

A instância mestre do SQL Server fornece a seguinte funcionalidade:

## <a name="connectivity"></a>Conectividade

A instância mestre do SQL Server fornece um ponto de extremidade TDS acessível externamente para o cluster. Você pode se conectar a aplicativos ou ferramentas do SQL Server como o Studio de dados do Azure ou SQL Server Management Studio para esse ponto de extremidade, como você faria qualquer outra instância do SQL Server.

## <a name="scale-out-query-management"></a>Gerenciamento de consulta de expansão

A instância mestre do SQL Server contém o mecanismo de consulta de expansão que é usado para distribuir consultas entre instâncias do SQL Server em nós de [computação do pool de](concept-compute-pool.md). O mecanismo de consulta de expansão também fornece acesso por meio do Transact-SQL para todas as tabelas de Hive no cluster sem qualquer configuração adicional.

## <a name="metadata-and-user-databases"></a>Bancos de dados de usuário e metadados

Além do padrão do SQL Server system bancos de dados, a instância mestre do SQL também contém o seguinte:

- Um banco de dados de metadados que contém metadados de tabela do HDFS
- Um mapa de fragmentos do plano de dados
- Detalhes de tabelas externas que fornecem acesso ao plano de dados de cluster.
- Fontes de dados externas do PolyBase e tabelas externas definidas em bancos de dados do usuário.

Você também pode optar por adicionar seus próprios bancos de dados do usuário para a instância mestre do SQL Server.

## <a name="machine-learning-services"></a>Serviços de Machine learning

Serviços de aprendizado de máquina de SQL Server é um recurso de complemento para o mecanismo de banco de dados, usado para executar o código Java, R e Python no SQL Server. Esse recurso se baseia na estrutura de extensibilidade do SQL Server, que isola os processos externos do principais processos de mecanismo, mas integra-se totalmente com os dados relacionais, como procedimentos armazenados, script T-SQL que contém instruções de R ou Python ou Java, R ou Código do Python que contém o T-SQL.

Como parte de um cluster de big data do SQL Server, serviços de machine learning serão disponibilizado na instância mestre do SQL Server por padrão. Isso significa que, depois que a execução do script externo estiver habilitada na instância mestre do SQL Server, ele vai ser possível executar o Java, scripts de R e Python usando sp_execute_external_script.

### <a name="advantages-of-machine-learning-services-in-a-big-data-cluster"></a>Vantagens de serviços do machine learning em um cluster de big data

SQL Server 2019 torna fácil para big data a ser unida aos dados dimensionais normalmente são armazenados no banco de dados empresariais. O valor de big data aumenta muito quando ele não é apenas nas mãos de partes de uma organização, mas também está incluído em relatórios, painéis e aplicativos. Ao mesmo tempo, os cientistas de dados podem continuar a usar as ferramentas do ecossistema HDFS/Spark e fácil, ter acesso aos dados na instância mestre do SQL Server e em fontes de dados externos acessíveis em tempo real _por meio de_ o mestre do SQL Server instância.

Com clusters do SQL Server 2019 big data, você pode fazer mais com seu Lagos de dados empresariais. Os analistas e desenvolvedores do SQL Server podem:

* Crie aplicativos que consomem dados Lagos de dados da empresa.
* Razão em todos os dados com consultas Transact-SQL.
* Use o ecossistema existente de aplicativos e ferramentas do SQL Server para acessar e analisar os dados da empresa.
* Reduza a necessidade de movimentação de dados por meio da virtualização de dados e data marts.
* Continue a usar o Spark para cenários de big data.
* Crie aplicativos empresariais inteligentes usando o Spark ou do SQL Server para treinar modelos por Lagos de dados.
* Operacionalize modelos em bancos de dados de produção para melhor desempenho.
* Dados de Stream diretamente para o enterprise data marts para análise em tempo real.
* Explore dados visualmente usando ferramentas de BI e análise interativa.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte os seguintes recursos:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
- [Workshop: Arquitetura de clusters de grandes dados do Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
