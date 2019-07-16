---
title: Criando objetos de banco de dados com integração Common Language Runtime (CLR) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- database objects [CLR integration], building
- common language runtime [SQL Server], building database objects
- managed code [SQL Server], database objects
- building database objects [CLR integration]
- .NET Framework routines [SQL Server]
ms.assetid: ce34132c-bfa3-447b-9131-b6e17c672efe
author: rothja
ms.author: jroth
ms.openlocfilehash: 7037105391425632dba0af3646635305e510f207
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138673"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>Criando objetos de banco de dados com integração CLR (Common Language Runtime)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode compilar objetos de banco de dados que usam a integração do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o CLR do .NET Framework. Código gerenciado executado dentro de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é conhecido como "rotina CLR". Essas rotinas incluem:  
  
-   Funções definidas pelo usuário com valor escalar (UDFs escalares)  
  
-   Funções definidas pelo usuário com valor de tabela (TVFs)  
  
-   Procedimentos definidos pelo usuário (UDPs)  
  
-   Gatilhos definidos pelo usuário  
  
 As rotinas CLR têm a mesma estrutura no código gerenciado. Elas são mapeadas para métodos públicos e estáticos (compartilhados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET) de uma classe. Além das rotinas, também podem ser definidos UDTs (tipos definidos pelo usuário) e funções de agregação definida pelo usuário usando o .NET Framework. Os UDTs e as agregações definidas pelo usuário são mapeados para classes inteiras do .NET Framework.  
  
 Cada tipo de rotina do .NET Framework tem uma declaração [!INCLUDE[tsql](../../../includes/tsql-md.md)] e pode ser usada em qualquer lugar no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que o equivalente de [!INCLUDE[tsql](../../../includes/tsql-md.md)] possa ser usado. Por exemplo, UDFs escalares podem ser usados em qualquer expressão escalar. Uma TVF pode ser usada em qualquer cláusula FROM. Um procedimento pode ser invocado em uma instrução EXEC ou de um aplicativo cliente.  
  
> [!NOTE]  
>  A execução de um objeto CLR (função definida pelo usuário, tipo definido pelo usuário ou gatilho) no Common Language Runtime poderá acontecer em vários threads (plano paralelo), se o otimizador de consulta achar que isso é benéfico. No entanto, se uma função definida pelo usuário acessar dados, a execução estará em um plano serial. Quando executado em uma versão de servidor antes do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], se uma função definida pelo usuário contiver parâmetros LOB ou valores de retorno, execução também deverá estar em um plano serial.  
  
 A tabela a seguir lista os tópicos abordados nesta seção.  
  
 [Introdução à integração CLR](../../../relational-databases/clr-integration/database-objects/getting-started-with-clr-integration.md)  
 Fornece uma visão geral breve das bibliotecas e namespaces necessários para compilar um objeto usando a integração CLR com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Inclui o exemplo de procedimento armazenado CLR "Hello World".  
  
 [Bibliotecas do .NET Framework compatíveis](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)  
 Fornece informações sobre as bibliotecas do .NET Framework suportadas pela integração CLR.  
  
 [Restrições do modelo de programação da integração CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
 Fornece informações sobre restrições de modelo de programação de integração CLR.  
  
 [Tipos de dados do SQL Server no .NET Framework](../../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 Uma visão geral dos tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e seus equivalentes do .NET Framework.  
  
 [Visão geral dos atributos personalizados da integração CLR](https://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)  
 Fornece informações sobre atributos personalizados de integração CLR.  
  
 [Funções do CLR definidas pelo usuário](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 Descreve como implementar e usar os vários tipos de funções CLR: com valor de tabela, escalares e funções de agregação definida pelo usuário.  
  
 [Tipos definidos pelo usuário do CLR](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 Descreve como implementar e usar tipos definidos pelo usuário CLR.  
  
 [Procedimentos armazenados CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)  
 Descreve como implementar e usar procedimentos armazenados CLR.  
  
 [Gatilhos CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
 Descreve como implementar e usar gatilhos CLR.  
  
## <a name="see-also"></a>Consulte também  
 [Common Language Runtime &#40;CLR&#41; visão geral da integração](../../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
  
  
