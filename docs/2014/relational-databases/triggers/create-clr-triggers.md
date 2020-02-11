---
title: Criar gatilhos CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CRL triggers
- DML triggers, CLR triggers
- DDL triggers, CLR triggers
ms.assetid: 31f41703-134d-49fc-9850-76c297351c2c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b68531b962b10785927c6212b2483f2d9c1d7d3a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62698826"
---
# <a name="create-clr-triggers"></a>Criar gatilhos CLR
  Você pode criar um objeto de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados dentro do que é programado em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] assembly criado no Common Language Runtime (CLR). Os objetos do banco de dados que podem alavancar o modelo de programação avançado fornecido pelo CLR incluem gatilhos DML, gatilhos DDL, procedimentos armazenados, funções, funções de agregação e tipos.  
  
 A criação de um gatilho CLR (DML ou DDL) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] engloba as seguintes etapas:  
  
-   Defina o gatilho como uma classe em uma linguagem com suporte para .NET Framework. Para mais informações sobre como programar gatilhos CLR, consulte [Gatilhos CLR](../../database-engine/dev-guide/clr-triggers.md). Em seguida, compile a classe para criar um assembly no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , usando o compilador de idioma apropriado.  
  
-   Registrar o assembly no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução CREATE ASSEMBLY. Para obter mais informações sobre assemblies no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../clr-integration/assemblies-database-engine.md).  
  
-   Crie o gatilho que referencia o assembly registrado.  
  
> [!NOTE]  
>  A implantação de um projeto SQL Server no [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra um assembly no banco de dados especificado para o projeto. Ao implantar o projeto, cria-se também os gatilhos CLR no banco de dados para todos os métodos anotados com o atributo `SqlTrigger`. Para obter mais informações, consulte [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  A capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de executar o código CLR, por padrão, está desativada. Você pode criar, alterar e remover objetos de banco de dados que referenciam módulos de código gerenciado, mas essas referências [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não serão executadas no, a menos que a [opção CLR Enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) esteja habilitada usando [sp_configure (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql).  
  
 **Para criar, modificar ou descartar um assembly**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **Para criar um gatilho CLR**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)  
  
## <a name="see-also"></a>Consulte Também  
 [Gatilhos DML](dml-triggers.md)   
 [Conceitos de programação de integração do CLR&#41; &#40;Common Language Runtime](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [Acesso aos dados dos objetos de banco de dados CLR](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
