---
title: Criando objetos de banco de dados com integração CLR (Common Language Runtime) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 8dc507d455636bf6256fd7ba4649dba53d32884e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62919250"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>Criando objetos de banco de dados com integração CLR (Common Language Runtime)
  Você pode criar objetos de banco de [!INCLUDE[ssNoVersion](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dados usando o é chamado de "rotina CLR". Essas rotinas incluem:  
  
-   Funções definidas pelo usuário com valor escalar (UDFs escalares)  
  
-   Funções definidas pelo usuário com valor de tabela (TVFs)  
  
-   Procedimentos definidos pelo usuário (UDPs)  
  
-   Gatilhos definidos pelo usuário  
  
 As rotinas CLR têm a mesma estrutura no código gerenciado. Elas são mapeadas para métodos públicos e estáticos (compartilhados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET) de uma classe. Além das rotinas, também podem ser definidos UDTs (tipos definidos pelo usuário) e funções de agregação definida pelo usuário usando o .NET Framework. Os UDTs e as agregações definidas pelo usuário são mapeados para classes inteiras do .NET Framework.  
  
 Cada tipo de rotina de .NET Framework tem [!INCLUDE[tsql](../../../includes/ssnoversion-md.md)] um que [!INCLUDE[tsql](../../../includes/tsql-md.md)] o equivalente pode ser usado. Por exemplo, UDFs escalares podem ser usados em qualquer expressão escalar. Uma TVF pode ser usada em qualquer cláusula FROM. Um procedimento pode ser invocado em uma instrução EXEC ou de um aplicativo cliente.  
  
> [!NOTE]  
>  A execução de um objeto CLR (função definida pelo usuário, tipo definido pelo usuário ou gatilho) no Common Language Runtime poderá acontecer em vários threads (plano paralelo), se o otimizador de consulta achar que isso é benéfico. No entanto, se uma função definida pelo usuário acessar dados, a execução estará em um plano serial. Quando executado em uma versão de servidor antes do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], se uma função definida pelo usuário contiver parâmetros LOB ou valores de retorno, execução também deverá estar em um plano serial.  
  
 A tabela a seguir lista os tópicos abordados nesta seção.  
  
 [Introdução à integração CLR](getting-started-with-clr-integration.md)  
 Fornece uma visão geral breve das bibliotecas e namespaces necessários para compilar um objeto usando a integração CLR com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Inclui o exemplo de procedimento armazenado CLR "Hello World".  
  
 [Bibliotecas do .NET Framework compatíveis](supported-net-framework-libraries.md)  
 Fornece informações sobre as bibliotecas do .NET Framework suportadas pela integração CLR.  
  
 [Restrições do modelo de programação da Integração CLR](clr-integration-programming-model-restrictions.md)  
 Fornece informações sobre restrições de modelo de programação de integração CLR.  
  
 [Tipos de dados do SQL Server no .NET Framework](../../clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 Uma visão geral dos tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e seus equivalentes do .NET Framework.  
  
 [Visão geral dos atributos personalizados da integração CLR](../../../database-engine/dev-guide/overview-of-clr-integration-custom-attributes.md)  
 Fornece informações sobre atributos personalizados de integração CLR.  
  
 [Funções CLR definidas pelo usuário](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 Descreve como implementar e usar os vários tipos de funções CLR: com valor de tabela, escalares e funções de agregação definida pelo usuário.  
  
 [Tipos CLR definidos pelo usuário](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 Descreve como implementar e usar tipos definidos pelo usuário CLR.  
  
 [Procedimentos armazenados CLR](../../../database-engine/dev-guide/clr-stored-procedures.md)  
 Descreve como implementar e usar procedimentos armazenados CLR.  
  
 [Gatilhos CLR](../../../database-engine/dev-guide/clr-triggers.md)  
 Descreve como implementar e usar gatilhos CLR.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral da integração do CLR&#41; &#40;Common Language Runtime](../common-language-runtime-integration-overview.md)  
  
  
