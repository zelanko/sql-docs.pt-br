---
title: Criar funções CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CLR functions [SQL Server]
- user-defined functions [SQL Server], CLR
ms.assetid: a82df075-2243-4e19-bfe1-ae6d65dabd0f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1a15690eb5aff48ec0f72df16e8342ed5c0522c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62524056"
---
# <a name="create-clr-functions"></a>Criar funções CLR
  É possível criar um objeto de banco de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programada em um assembly criado no CLR (Common Language Runtime) [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Os objetos do banco de dados que podem aproveitar o modelo de programação avançado fornecido pelo CLR inclui funções de agregação, funções, procedimentos armazenados, gatilhos e tipos.  
  
 Criar uma função CLR em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envolve as seguintes etapas:  
  
-   Defina a função como um método estático de uma classe em um idioma com suporte do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para obter mais informações sobre como programar funções no Common Language Runtime, veja [Funções CLR definidas pelo usuário](../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md). Em seguida, compilar a classe para criar um assembly no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , usando o compilador de idioma apropriado.  
  
-   Registre o assembly no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução CREATE ASSEMBLY. Para obter mais informações sobre assemblies no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../clr-integration/assemblies-database-engine.md).  
  
-   Crie a função que faz referência ao assembly registrado, usando a instrução [CREATE FUNCTION](/sql/t-sql/statements/create-function-transact-sql) .  
  
> [!NOTE]  
>  A implantação de um projeto SQL Server no [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra um assembly no banco de dados especificado para o projeto. Ao implantar o projeto, cria-se também as funções CLR no banco de dados para todos os métodos anotados com o atributo `SqlFunction`. Para obter mais informações, consulte [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  A capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de executar o código CLR, por padrão, está desativada. É possível criar, alterar e remover objetos do banco de dados que fazem referência aos módulos de código gerenciados, mas essas referências não serão executadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que a opção [clr enabled Option](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) seja habilitada, usando [sp_configure (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql).  
  
## <a name="accessing-external-resources"></a>Acessando recursos externos  
 As funções CLR podem ser usadas para acessar recursos externos como arquivos, recursos de rede, serviços da Web, outros bancos de dados (incluindo as instâncias remotas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Isto pode ser alcançado usando diversas classes no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], como `System.IO`, `System.WebServices`, `System.Sql`e assim por diante. O assembly que contém essas funções deve ser configurado pelo menos com o conjunto de permissões EXTERNAL_ACCESS para este propósito. Para obter mais informações, consulte [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql). O provedor gerenciado do cliente SQL pode ser usado para acessar instâncias remotas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, as conexões de loopback para o servidor de origem não são suportadas nas funções CLR.  
  
 **Para criar, modificar ou descartar assemblies no SQL Server**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **Para criar uma função CLR**  
  
-   [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)  
  
## <a name="accessing-native-code"></a>Acessando código nativo  
 Podem ser usadas funções CLR para acessar código nativo (não gerenciado), como código escrito em C ou C++, pelo uso de PInvoke de código gerenciado (veja [Chamando funções nativas com base no código gerenciado](https://go.microsoft.com/fwlink/?LinkID=181929) para obter detalhes). Isto pode permitir reutilizar o código herdado como CLR UDFs ou escrever UDFs de desempenho crítico em código nativo. Isto requer o uso de um assembly UNSAFE. Veja [Segurança de acesso a código da integração CLR](../clr-integration/security/clr-integration-code-access-security.md) para obter advertências sobre o uso de assemblies UNSAFE.  
  
## <a name="see-also"></a>Consulte também  
 [Criar funções definidas pelo usuário &#40;Mecanismo de Banco de Dados&#41;](create-user-defined-functions-database-engine.md)   
 [Criar agregações definidas pelo usuário](create-user-defined-aggregates.md)   
 [Executar funções definidas pelo usuário](execute-user-defined-functions.md)   
 [Exibir funções definidas pelo usuário](view-user-defined-functions.md)   
 [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
