---
title: Criar agregações definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: c278b746-6323-4b32-b460-239915acc067
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 23d5180928f4f3335aa17dff61b50e6fdd19549f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68196475"
---
# <a name="create-user-defined-aggregates"></a>Criar agregações definidas pelo usuário
  Você pode criar um objeto de banco de dados dentro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é programado em um assembly CLR. Os objetos do banco de dados que podem alavancar o modelo de programação avançado fornecido pelo CLR incluem gatilhos, procedimentos armazenados, funções, funções de agregação e tipos.  
  
 Assim como as funções de agregação internas fornecidas em [!INCLUDE[tsql](../../includes/tsql-md.md)], as funções de agregação definidas pelo usuário executam o cálculo de um conjunto de valores e retornam um único valor.  
  
 Criar uma função de agregação definida pelo usuário em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envolve as seguintes etapas:  
  
-   Definir a função de agregação definida pelo usuário como uma classe em uma linguagem [!INCLUDE[msCoName](../../includes/msconame-md.md)] suportada por .NET Framework. Para obter mais informações sobre como programar agregações definidas pelo usuário em CLR, veja [Agregações CLR definidas pelo usuário](../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md). Compile essa classe para criar um assembly CLR que usa o compilador de linguagem apropriado.  
  
-   Registrar o assembly no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução CREATE ASSEMBLY. Para obter mais informações sobre assemblies no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../clr-integration/assemblies-database-engine.md).  
  
-   Criar a agregação definida pelo usuário que referencia o assembly registrado que usa a instrução CREATE AGGREGATE.  
  
> [!NOTE]  
>  A implantação de um projeto SQL Server no [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra um assembly no banco de dados especificado para o projeto. Implantar um projeto também cria uma agregação definida pelo usuário no banco de dados para todas as definições de classe anotadas pelo atributo `SqlUserDefinedAggregate`. Para obter mais informações, consulte [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  A capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de executar o código CLR, por padrão, está desativada. É possível criar, alterar e remover objetos do banco de dados que fazem referência aos módulos de código gerenciados, mas essas referências não serão executadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que a [Opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) tenha sido habilitada com [sp_configure (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql).  
  
 **Para criar, modificar ou descartar um assembly**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **Para criar uma agregação definida pelo usuário**  
  
-   [CREATE AGGREGATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-aggregate-transact-sql)  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
