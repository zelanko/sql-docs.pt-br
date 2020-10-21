---
title: O que são Extensões de Linguagem do SQL Server?
titleSuffix: ''
description: As Extensões de Linguagem é um recurso do SQL Server usado para executar código externo. No SQL Server 2019, há suporte para Java, Python e R. Os dados relacionais podem ser usados no código externo usando a estrutura de extensibilidade.
author: dphansen
ms.author: davidph
ms.date: 10/07/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 09d5643b3a39493843adc0ad2da716b7fda1b332
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934901"
---
# <a name="what-is-sql-server-language-extensions"></a>O que são Extensões de Linguagem do SQL Server?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

As Extensões de Linguagem é um recurso do SQL Server usado para executar código externo. Os dados relacionais podem ser usados no código externo usando a [estrutura de extensibilidade](concepts/extensibility-framework.md).

No SQL Server 2019, há suporte para Java, Python e R.

> [!NOTE]
> Para executar o Python ou o R no SQL Server, confira a documentação do [machine learning do SQL](../machine-learning/index.yml). Com o SQL Server 2019 e posterior, você pode usar um runtime personalizado do Python e do R com as extensões de linguagem. Para obter mais informações, confira o [runtime personalizado do Python](../machine-learning/install/custom-runtime-python.md) e o [runtime personalizado do R](../machine-learning/install/custom-runtime-r.md).

## <a name="what-you-can-do-with-language-extensions"></a>O que você pode fazer com as Extensões de Linguagem

As Extensões de Linguagem usam a estrutura de extensibilidade para executar código externo. A execução de código é isolada dos principais processos de mecanismo, mas totalmente integrada à execução de consulta do SQL Server. Você pode executar o código na fonte dos dados, eliminando a necessidade de efetuar pull dos dados na rede.

As linguagens externas são definidas com [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). O procedimento armazenado do sistema [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) é usado como a interface para executar o código.

As Extensões de Linguagem oferecem várias vantagens:

+ Segurança de dados. Aproximar a execução de linguagem externa da fonte de dados evita uma movimentação de dados desperdiçadora ou insegura.
+ Velocidade. Os bancos de dados são otimizados para operações baseadas em conjunto. Inovações recentes em bancos de dados, como tabelas na memória, agilizam resumos e agregações e são um complemento perfeito para a ciência de dados.
+ Facilidade de implantação e integração. [!INCLUDE [ssNoVersion](../includes/ssnoversion-md.md)] é o ponto central de operações para muitas outras tarefas e aplicativos de gerenciamento de dados. Usando os dados do banco de dados, você garante que os dados usados pela extensão de linguagem sejam consistentes e atualizados.

## <a name="next-steps"></a>Próximas etapas

+ Instalar um [runtime personalizado do Python para o SQL Server](../machine-learning/install/custom-runtime-python.md)
+ Instalar um [runtime personalizado do R para o SQL Server](../machine-learning/install/custom-runtime-r.md)
+ Instalar as [Extensões de Linguagem do SQL Server no Windows](install/install-sql-server-language-extensions-on-windows.md) ou [no Linux](../linux/sql-server-linux-setup-language-extensions.md)
+ Instalar o [SDK de Extensibilidade da Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md)
