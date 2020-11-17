---
title: Quais são as novidades nas Extensões de Linguagem do SQL Server?
titleSuffix: ''
description: Saiba mais sobre as novidades nas Extensões de Linguagem do SQL Server que expandem, estendem e aprofundam a integração entre linguagens externas e a plataforma de dados.
author: dphansen
ms.author: davidph
ms.date: 11/09/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0b1f7aec4b3581a8604fad68518a36ac8ecc14dd
ms.sourcegitcommit: 863420525a1f5d5b56b311b84a6fb14e79404860
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94417993"
---
# <a name="whats-new-in-sql-server-language-extensions"></a>Quais são as novidades nas Extensões de Linguagem do SQL Server?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

As funcionalidades da [Extensão de Linguagem](language-extensions-overview.md) são adicionadas ao SQL Server em cada versão conforme continuamos expandindo, estendendo e aprofundando a integração entre linguagens externas e a plataforma de dados.

## <a name="sql-server-2019"></a>SQL Server 2019

Os novos recursos para [Extensão de Linguagem](language-extensions-overview.md) no SQL Server 2019 podem ser encontrados abaixo. Para obter mais informações sobre todos os recursos desta versão, confira [Novidades do SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) e [Notas sobre a versão do SQL Server 2019](../sql-server/sql-server-version-15-release-notes.md).

### <a name="new-python-and-r-language-extensions"></a>Novas extensões de linguagem Python e R

- Um [runtime personalizado do Python](../machine-learning/install/custom-runtime-python.md) está disponível com as Extensões de Linguagem. Para obter mais informações, confira como [Instalar um runtime personalizado do Python no Windows](../machine-learning/install/custom-runtime-python.md?view=sql-server-ver15&preserve-view=true) ou [Instalar um runtime personalizado do Python no Linux](../machine-learning/install/custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true).

- Um [runtime personalizado do R](../machine-learning/install/custom-runtime-r.md) está disponível com as Extensões de Linguagem. Para obter mais informações, confira como [Instalar um runtime personalizado do R no Windows](../machine-learning/install/custom-runtime-r.md?view=sql-server-ver15&preserve-view=true) ou [Instalar um runtime personalizado do R no Linux](../machine-learning/install/custom-runtime-r.md?view=sql-server-linux-ver15&preserve-view=true).

### <a name="new-java-language-extension"></a>Nova extensão da linguagem Java

- O Runtime do Java padrão no Windows e Linux é o Open Zulu JRE e é incluído com a [instalação das Extensões de Linguagem do SQL Server no Windows](install/windows-java.md) e a [instalação das Extensões de Linguagem do SQL Server no Linux](../linux/sql-server-linux-setup-language-extensions-java.md).
- [Tipos de dados Java](how-to/java-to-sql-data-types.md) com suporte.
- [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) para registrar a linguagem externa (por exemplo, Java) no SQL Server.
- [SDK de Extensibilidade da Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md).
- No Windows e no Linux, o código Java pode ser acessado em uma biblioteca externa usando a instrução [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md). Saiba mais: [Como chamar Java do SQL Server](how-to/call-java-from-sql.md).
- [Extensão da linguagem Java](language-extensions-overview.md) no Windows e Linux. Você pode disponibilizar o código Java compilado para o SQL Server atribuindo permissões e definindo o caminho. Os aplicativos cliente com acesso ao SQL Server podem usar dados e executar seu código chamando [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), o mesmo procedimento usado para a integração do R e Python nos Serviços de Machine Learning do SQL Server.

## <a name="next-steps"></a>Próximas etapas

+ Instalar [Extensões de Linguagem do SQL Server no Windows](install/windows-java.md) ou [no Linux](../linux/sql-server-linux-setup-language-extensions-java.md).
