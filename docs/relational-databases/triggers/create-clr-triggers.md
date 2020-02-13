---
title: Criar gatilhos CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
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
ms.openlocfilehash: 096a915f8a86e7dcf8acd5e029fa6e277b8a56c0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68075549"
---
# <a name="create-clr-triggers"></a>Criar gatilhos CLR
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  É possível criar um objeto de banco de dados dentro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seja programado em um assembly criado no CLR (Common Language Runtime) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Os objetos do banco de dados que podem alavancar o modelo de programação avançado fornecido pelo CLR incluem gatilhos DML, gatilhos DDL, procedimentos armazenados, funções, funções de agregação e tipos.  
  
 A criação de um gatilho CLR (DML ou DDL) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] engloba as seguintes etapas:  
  
-   Defina o gatilho como uma classe em uma linguagem com suporte para .NET Framework. Para mais informações sobre como programar gatilhos CLR, consulte [Gatilhos CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c). Em seguida, compile a classe para criar um assembly no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , usando o compilador de idioma apropriado.  
  
-   Registrar o assembly no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução CREATE ASSEMBLY. Para obter mais informações sobre assemblies no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md).  
  
-   Crie o gatilho que referencia o assembly registrado.  
  
> [!NOTE]
>  A implantação de um projeto SQL Server no [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra um assembly no banco de dados especificado para o projeto. Ao implantar o projeto, cria-se também os gatilhos CLR no banco de dados para todos os métodos anotados com o atributo **SqlTrigger** . Para obter mais informações, consulte [Deploying CLR Database Objects](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
> 
> [!NOTE]
>  A capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de executar o código CLR, por padrão, está desativada. É possível criar, alterar e remover objetos do banco de dados que fazem referência aos módulos de código gerenciados, mas essas referências não serão executadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que a [opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) tenha sido habilitada usando [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 **Para criar, modificar ou descartar um assembly**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Para criar um gatilho CLR**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Gatilhos DML](../../relational-databases/triggers/dml-triggers.md)   
 [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [Acesso aos dados dos objetos de banco de dados CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
