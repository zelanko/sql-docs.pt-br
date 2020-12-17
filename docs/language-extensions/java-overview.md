---
title: O que é a Extensão da Linguagem Java?
titleSuffix: SQL Server Language Extensions
description: A Extensão de Linguagem Java é um recurso do SQL Server usado para executar código Java externo. Os dados relacionais podem ser empregados no código Java externo usando a estrutura de extensibilidade.
author: dphansen
ms.author: davidph
ms.date: 11/10/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: f68821900b2e304028bccfd79e96f988f02267e9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471717"
---
# <a name="what-is-java-language-extension"></a>O que é a Extensão da Linguagem Java?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

A Extensão de Linguagem Java é um recurso do SQL Server usado para executar código Java externo. Os dados relacionais podem ser usados no código Java externo usando a [estrutura de extensibilidade](concepts/extensibility-framework.md). A Extensão de Linguagem Java faz parte das [Extensões de Linguagem do SQL Server](language-extensions-overview.md).

O runtime do Java padrão é o Zulu Open JRE. Você também pode usar outro Java JRE ou SDK.

## <a name="what-you-can-do-with-the-java-language-extension"></a>O que você pode fazer com a Extensão de Linguagem Java

A Extensão de Linguagem Java usa a estrutura de extensibilidade para executar código Java externo. A execução de código é isolada dos principais processos de mecanismo, mas totalmente integrada à execução de consulta do SQL Server. Você pode executar o código Java na fonte dos dados, eliminando a necessidade de efetuar pull dos dados na rede.

A linguagem Java externa é definida com [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql). O procedimento armazenado do sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) é usado como a interface para executar o código Java.

## <a name="get-started-with-java-language-extension"></a>Introdução à Extensão de Linguagem Java

1. [Instale a Extensão de Linguagem Java do SQL Server no Windows](install/windows-java.md) ou [no Linux](../linux/sql-server-linux-setup-language-extensions-java.md).

1. Configure ferramentas de desenvolvimento.

    + Use o IDE de sua preferência para desenvolver código Java.
    + Instale o [SDK de Extensibilidade da Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md) a fim de executar código Java no SQL Server.
    + Use o [Azure Data Studio](../azure-data-studio/what-is.md) para executar código externo no SQL Server.
    + Use o procedimento armazenado do sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) para executar seu código Java no SQL Server.

1. Escreva seu primeiro código Java.

    + [Tutorial: Expressões regulares com Java](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>Limitações

O número de valores nos buffers de entrada e saída não pode exceder `MAX_INT (2^31-1)`, pois esse é o número máximo de elementos que pode ser alocado em uma matriz em Java.

## <a name="next-steps"></a>Próximas etapas

+ Instalar a [Extensão de Linguagem Java do SQL Server no Windows](install/windows-java.md) ou [no Linux](../linux/sql-server-linux-setup-language-extensions-java.md)
+ Instalar o [SDK de Extensibilidade da Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md)
