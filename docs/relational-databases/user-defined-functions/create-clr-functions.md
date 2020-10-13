---
description: Criar funções CLR
title: Criar funções CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CLR functions [SQL Server]
- user-defined functions [SQL Server], CLR
ms.assetid: a82df075-2243-4e19-bfe1-ae6d65dabd0f
author: rothja
ms.author: jroth
ms.openlocfilehash: 4e7e7ba7e0e3f526c69026b9f759937d7329d50c
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91811070"
---
# <a name="create-clr-functions"></a>Criar funções CLR
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Crie um objeto de banco de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seja programado em um assembly criado no CLR (Common Language Runtime) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Os objetos do banco de dados que podem aproveitar o modelo de programação avançado fornecido pelo CLR inclui funções de agregação, funções, procedimentos armazenados, gatilhos e tipos.  
  
 Criar uma função CLR em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envolve as seguintes etapas:  
  
-   Defina a função como um método estático de uma classe em um idioma com suporte do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para obter mais informações sobre como programar funções no Common Language Runtime, veja [Funções CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md). Em seguida, compilar a classe para criar um assembly no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , usando o compilador de idioma apropriado.  
  
-   Registre o assembly no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução CREATE ASSEMBLY. Para obter mais informações sobre assemblies no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md).  
  
-   Crie a função que faz referência ao assembly registrado, usando a instrução [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) .  
  
> [!NOTE]
>  A implantação de um projeto SQL Server no [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra um assembly no banco de dados especificado para o projeto. Ao implantar o projeto, cria-se também as funções CLR no banco de dados para todos os métodos anotados com o atributo **SqlFunction** . Para obter mais informações, consulte [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
> 
> [!NOTE]
>  A capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de executar o código CLR, por padrão, está desativada. É possível criar, alterar e remover objetos do banco de dados que fazem referência aos módulos de código gerenciados, mas essas referências não serão executadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que a opção [clr enabled Option](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) seja habilitada, usando [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
## <a name="accessing-external-resources"></a>Acessando recursos externos  
 As funções CLR podem ser usadas para acessar recursos externos como arquivos, recursos de rede, serviços da Web, outros bancos de dados (incluindo as instâncias remotas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Isto pode ser alcançado usando diversas classes no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], como `System.IO`, `System.WebServices`, `System.Sql`e assim por diante. O assembly que contém essas funções deve ser configurado pelo menos com o conjunto de permissões EXTERNAL_ACCESS para este propósito. Para obter mais informações, consulte [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md). O provedor gerenciado do cliente SQL pode ser usado para acessar instâncias remotas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, as conexões de loopback para o servidor de origem não são suportadas nas funções CLR.  
  
 **Para criar, modificar ou descartar assemblies no SQL Server**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Para criar uma função CLR**  
  
-   [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
  
## <a name="accessing-native-code"></a>Acessando código nativo  
 Podem ser usadas funções CLR para acessar código nativo (não gerenciado), como código escrito em C ou C++, pelo uso de PInvoke de código gerenciado (veja [Chamando funções nativas com base no código gerenciado](/cpp/dotnet/calling-native-functions-from-managed-code) para obter detalhes). Isto pode permitir reutilizar o código herdado como CLR UDFs ou escrever UDFs de desempenho crítico em código nativo. Isto requer o uso de um assembly UNSAFE. Veja [Segurança de acesso a código da integração CLR](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md) para obter advertências sobre o uso de assemblies UNSAFE.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar funções definidas pelo usuário &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)   
 [Criar agregações definidas pelo usuário](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)   
 [Executar funções definidas pelo usuário](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)   
 [Exibir funções definidas pelo usuário](../../relational-databases/user-defined-functions/view-user-defined-functions.md)   
 [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
