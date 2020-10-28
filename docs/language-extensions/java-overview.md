---
title: O que é a Extensão da Linguagem Java?
description: No SQL Server 2019, há suporte para as extensões de linguagem Java, Python e R. As Extensões de Linguagem são recursos do SQL Server usados para executar códigos externos.  Os dados relacionais podem ser empregados no código externo usando a estrutura de extensibilidade.
author: cawrites
ms.author: chadam
ms.date: 10/06/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f6b7f2c21aa79ee5c0c9657cf817d9801b5d2891
ms.sourcegitcommit: 2b6760408de3b99193edeccce4b92a2f9ed5bcc6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92175900"
---
# <a name="what-is-java-language-extension"></a>O que é a Extensão da Linguagem Java?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

As Extensões de Linguagem é um recurso do SQL Server usado para executar código externo. Os dados relacionais podem ser usados no código externo usando a [estrutura de extensibilidade](concepts/extensibility-framework.md).

No SQL Server 2019, há suporte para Java. O runtime do Java padrão é o Zulu Open JRE. Você também pode usar outro Java JRE ou SDK.

> [!NOTE]
> Para executar o Python ou o R no SQL Server, confira a documentação do [machine learning do SQL](../machine-learning/index.yml). Com o SQL Server 2019 e posterior, você pode usar um runtime personalizado do Python e do R com as extensões de linguagem. Para obter mais informações, confira o [runtime personalizado do Python](../machine-learning/install/custom-runtime-python.md) e o [runtime personalizado do R](../machine-learning/install/custom-runtime-r.md).

## <a name="what-you-can-do-with-language-extensions"></a>O que você pode fazer com as Extensões de Linguagem

As Extensões de Linguagem usam a estrutura de extensibilidade para executar código externo. A execução de código é isolada dos principais processos de mecanismo, mas totalmente integrada à execução de consulta do SQL Server. Você pode executar o código na fonte dos dados, eliminando a necessidade de efetuar pull dos dados na rede.

As linguagens externas são definidas com [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql). O procedimento armazenado do sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) é usado como a interface para executar o código.

As Extensões de Linguagem oferecem várias vantagens:

+ Segurança de dados. Aproximar a execução de linguagem externa da fonte de dados evita uma movimentação de dados desperdiçadora ou insegura.
+ Velocidade. Os bancos de dados são otimizados para operações baseadas em conjunto. Inovações recentes em bancos de dados, como tabelas na memória, agilizam resumos e agregações e são um complemento perfeito para a ciência de dados.
+ Facilidade de implantação e integração. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é o ponto central de operações para muitas outras tarefas e aplicativos de gerenciamento de dados. Ao usar dados no banco de dados, você garante que os dados usados pelo Java sejam consistentes e atualizados.

## <a name="how-to-get-started"></a>Como começar

### <a name="step-1-install-the-software"></a>Etapa 1: Instalar o software

+ [Extensões de Linguagem do SQL Server no Windows](install/windows-java.md)
+ [Extensões de Linguagem do SQL Server no Linux](../linux/sql-server-linux-setup-language-extensions-java.md)

### <a name="step-2-configure-a-development-tool"></a>Etapa 2: Configurar uma ferramenta de desenvolvimento

Normalmente, os desenvolvedores escrevem código em seu próprio laptop ou estação de trabalho de desenvolvimento. Com extensões de linguagem no SQL Server, não há necessidade de alterar esse processo. Após a conclusão da instalação, você poderá executar código Java no SQL Server.

+ **Use o IDE de sua preferência** para desenvolver código Java.

+ **Instale o [SDK de Extensibilidade da Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md)** para executar código Java no SQL Server

+ **Use o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) ou o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)** para executar código externo no SQL Server

+ **Use o procedimento armazenado do sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)** para executar seu código Java no SQL Server.

### <a name="step-3-write-your-first-code"></a>Etapa 3: Escrever seu primeiro código

Executar código Java de dentro do script T-SQL:

+ [Tutorial: Expressões regulares com Java](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>Limitações

+ O número de valores nos buffers de entrada e saída não pode exceder `MAX_INT (2^31-1)`, pois esse é o número máximo de elementos que pode ser alocado em uma matriz em Java.

## <a name="next-steps"></a>Próximas etapas

+ Instalar um [runtime personalizado do Python para o SQL Server](../machine-learning/install/custom-runtime-python.md)
+ Instalar um [runtime personalizado do R para o SQL Server](../machine-learning/install/custom-runtime-r.md)
+ Instalar as [Extensões de Linguagem do SQL Server no Windows](../language-extensions/install/windows-java.md) ou [no Linux](../linux/sql-server-linux-setup-language-extensions-java.md)
+ Instalar o [SDK de Extensibilidade da Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md)
