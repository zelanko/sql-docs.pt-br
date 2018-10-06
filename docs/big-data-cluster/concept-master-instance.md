---
title: O que é os clusters de grandes dados do SQL Server de mestre de instância? | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: f3b17330f38d30400564171ba09328dc4f8c8be7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795843"
---
# <a name="what-is-the-sql-server-big-data-cluster-master-instance"></a>O que é o big data do SQL Server de instância mestre do cluster?

Este artigo descreve a função dos *instância mestre do SQL Server* em um cluster do SQL Server 2019 ata big. A instância mestre é uma instância do SQL Server em execução em um cluster de big data do SQL Server [plano de controle](big-data-cluster-overview.md#controlplane).

A instância mestre do SQL Server fornece a seguinte funcionalidade:

## <a name="connectivity"></a>Conectividade

A instância mestre do SQL Server fornece um ponto de extremidade TDS acessível externamente para o cluster. Você pode se conectar a aplicativos ou ferramentas do SQL Server como o Studio de dados do Azure ou SQL Server Management Studio para esse ponto de extremidade, como você faria qualquer outra instância do SQL Server.

## <a name="scale-out-query-management"></a>Gerenciamento de consulta de expansão

A instância mestre do SQL Server contém o mecanismo de consulta de expansão que é usado para distribuir consultas entre instâncias do SQL Server em nós de [computação do pool de](concept-compute-pool.md). O mecanismo de consulta de expansão também fornece acesso por meio do Transact-SQL para todas as tabelas de Hive no cluster sem qualquer configuração adicional. (Suporte de tabelas do hive não está no CTP 2.0)

## <a name="metadata-and-user-databases"></a>Bancos de dados de usuário e metadados

Além do padrão do SQL Server system bancos de dados, a instância mestre do SQL também contém o seguinte:

- Um banco de dados de metadados que contém metadados de tabela do HDFS
- Um mapa de fragmentos do plano de dados
- Detalhes de tabelas externas que fornecem acesso ao plano de dados de cluster.
- Fontes de dados externas do PolyBase e tabelas externas definidas em bancos de dados do usuário.

Você também pode optar por adicionar seus próprios bancos de dados do usuário para a instância mestre do SQL Server.

## <a name="machine-learning-services"></a>Serviços de Machine learning

Serviços de aprendizado de máquina de SQL Server é um recurso de complemento para o mecanismo de banco de dados, usado para executar o código Java, R e Python no SQL Server. Esse recurso se baseia na estrutura de extensibilidade do SQL Server, que isola os processos externos do principais processos de mecanismo, mas integra-se totalmente com os dados relacionais, como procedimentos armazenados, script T-SQL que contém instruções de R ou Python ou Java, R ou Código do Python que contém o T-SQL.

Como parte de um cluster de big data do SQL Server, serviços de machine learning serão disponibilizado na instância SQL Serevr mestre por padrão. Isso significa que, depois que a execução do script externo estiver habilitada na instância mestre do SQL Server, ele vai ser possível executar o Java, scripts de R e Python usando sp_execute_external_script.

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

Para saber mais sobre o Clusters grandes de dados do SQL Server, consulte a visão geral a seguir:

- [O que é a Clusters de Big Data do SQL Server de 2019?](big-data-cluster-overview.md)
