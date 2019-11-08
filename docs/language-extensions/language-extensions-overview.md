---
title: O que são Extensões de Linguagem?
titleSuffix: SQL Server Language Extensions
description: Saiba mais sobre as extensões de linguagem do SQL Server 2019 (versão prévia) que executam scripts externos no SQL Server.
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 15ff0339a487ecebdca23057bfce9053b5efca2e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73589020"
---
# <a name="what-is-sql-server-language-extensions-preview"></a>O que são Extensões de Linguagem do SQL Server (versão prévia)?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

As Extensões de Linguagem é um recurso do SQL Server usado para executar código externo. Os dados relacionais podem ser usados no código externo usando a [estrutura de extensibilidade](concepts/extensibility-framework.md).

No SQL Server 2019, há suporte para Java. O runtime do Java padrão é o Zulu Open JRE. Você também pode usar outro Java JRE ou SDK.

## <a name="what-you-can-do-with-language-extensions"></a>O que você pode fazer com as Extensões de Linguagem

As Extensões de Linguagem usam a estrutura de extensibilidade para executar código externo. A execução de código é isolada dos principais processos de mecanismo, mas totalmente integrada à execução de consulta do SQL Server. Eles permitem que você execute código onde os dados residem, acabando com a necessidade de extrair dados pela rede.

As linguagens externas são definidas com [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql). O procedimento armazenado do sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) é usado como a interface para executar o código.

As Extensões de Linguagem oferecem várias vantagens:

+ Segurança de dados. Aproximar a execução de linguagem externa da fonte de dados evita uma movimentação de dados desperdiçadora ou insegura.
+ Velocidade. Os bancos de dados são otimizados para operações baseadas em conjunto. Inovações recentes em bancos de dados, como tabelas na memória, agilizam resumos e agregações e são um complemento perfeito para a ciência de dados.
+ Facilidade de implantação e integração. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é o ponto central de operações para muitas outras tarefas e aplicativos de gerenciamento de dados. Usando dados que residem no banco de dados, você garante que os dados usados pelo Java sejam consistentes e atualizados.

## <a name="how-to-get-started"></a>Como começar a usar

### <a name="step-1-install-the-software"></a>Etapa 1: Instalar o software

+ [Extensões de Linguagem do SQL Server no Windows](install/install-sql-server-language-extensions-on-windows.md)
+ [Extensões de Linguagem do SQL Server no Linux](../linux/sql-server-linux-setup-language-extensions.md)

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

+ Instalar [Extensões de Linguagem do SQL Server no Windows](install/install-sql-server-language-extensions-on-windows.md) ou [no Linux](../linux/sql-server-linux-setup-language-extensions.md)
+ Instalar o [SDK de Extensibilidade da Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md)
