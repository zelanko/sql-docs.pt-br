---
title: O que são Extensões de Linguagem do SQL Server?
titleSuffix: ''
description: As Extensões de Linguagem é um recurso do SQL Server usado para executar código externo. No SQL Server, há suporte para Java, Python e R. Os dados relacionais podem ser empregados no código externo usando a estrutura de extensibilidade.
author: dphansen
ms.author: davidph
ms.date: 11/06/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e62b61e2b90f3a2f3ec837115d99a65070571c57
ms.sourcegitcommit: 06cb1751b1bc7420dbe4ad4555ab1afc5fc5bd71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361747"
---
# <a name="what-is-sql-server-language-extensions"></a>O que são Extensões de Linguagem do SQL Server?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

As Extensões de Linguagem é um recurso do SQL Server usado para executar código externo. Os dados relacionais podem ser usados no código externo usando a [estrutura de extensibilidade](concepts/extensibility-framework.md). No SQL Server 2019, há suporte os runtimes de Java, Python e R.

> [!NOTE]
> Para executar o Python ou o R no SQL Server, confira a documentação do [Serviços de Machine Learning](../machine-learning/sql-server-machine-learning-services.md). Com o SQL Server 2019 e posterior, você pode usar um runtime personalizado do Python e do R com as extensões de linguagem. Para obter mais informações, confira como instalar o [runtime personalizado do Python](../machine-learning/install/custom-runtime-python.md) e o [runtime personalizado do R](../machine-learning/install/custom-runtime-r.md).

## <a name="what-you-can-do-with-language-extensions"></a>O que você pode fazer com as Extensões de Linguagem

As Extensões de Linguagem usam a [estrutura de extensibilidade](concepts/extensibility-framework.md) para executar código externo. A execução de código é isolada dos principais processos de mecanismo, mas totalmente integrada à execução de consulta do SQL Server. Você pode executar o código na fonte dos dados, eliminando a necessidade de efetuar pull dos dados na rede.

As linguagens externas são definidas com [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). O procedimento armazenado do sistema [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) é usado como a interface para executar o código.

As Extensões de Linguagem oferecem várias vantagens:

+ Segurança de dados. Aproximar a execução de linguagem externa da fonte de dados evita uma movimentação de dados não segura.
+ Velocidade. Os bancos de dados são otimizados para operações baseadas em conjunto. 
+ Facilidade de implantação e integração. [!INCLUDE [ssNoVersion](../includes/ssnoversion-md.md)] é o ponto central de operações para muitas outras tarefas e aplicativos de gerenciamento de dados. Usando os dados do banco de dados, você garante que os dados usados pela extensão de linguagem sejam consistentes e atualizados.

## <a name="next-steps"></a>Próximas etapas

+ Instalar as [Extensões de Linguagem do SQL Server no Windows](install/windows-java.md) ou [no Linux](../linux/sql-server-linux-setup-language-extensions-java.md)
+ Instalar um [runtime personalizado do Python para o SQL Server](../machine-learning/install/custom-runtime-python.md)
+ Instalar um [runtime personalizado do R para o SQL Server](../machine-learning/install/custom-runtime-r.md)
+ Instalar o [SDK de Extensibilidade da Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md)
