---
title: Criar gatilhos CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CRL triggers
- DML triggers, CLR triggers
- DDL triggers, CLR triggers
ms.assetid: 31f41703-134d-49fc-9850-76c297351c2c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c91d1322b60fccc0c3eae16e88db828f153f9f01
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428195"
---
# <a name="create-clr-triggers"></a>Criar gatilhos CLR
  É possível criar um objeto de banco de dados dentro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programada em um assembly criado no CLR (Common Language Runtime) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Os objetos do banco de dados que podem alavancar o modelo de programação avançado fornecido pelo CLR incluem gatilhos DML, gatilhos DDL, procedimentos armazenados, funções, funções de agregação e tipos.  
  
 A criação de um gatilho CLR (DML ou DDL) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] engloba as seguintes etapas:  
  
-   Defina o gatilho como uma classe em uma linguagem com suporte para .NET Framework. Para mais informações sobre como programar gatilhos CLR, consulte [Gatilhos CLR](../../database-engine/dev-guide/clr-triggers.md). Em seguida, compile a classe para criar um assembly no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , usando o compilador de idioma apropriado.  
  
-   Registrar o assembly no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a instrução CREATE ASSEMBLY. Para obter mais informações sobre assemblies no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Assemblies &#40;Mecanismo de Banco de Dados&#41;](../clr-integration/assemblies-database-engine.md).  
  
-   Crie o gatilho que referencia o assembly registrado.  
  
> [!NOTE]  
>  A implantação de um projeto SQL Server no [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra um assembly no banco de dados especificado para o projeto. Ao implantar o projeto, cria-se também os gatilhos CLR no banco de dados para todos os métodos anotados com o atributo `SqlTrigger`. Para obter mais informações, consulte [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  A capacidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de executar o código CLR, por padrão, está desativada. É possível criar, alterar e remover objetos do banco de dados que fazem referência aos módulos de código gerenciados, mas essas referências não serão executadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que a [opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) tenha sido habilitada usando [sp_configure (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql).  
  
 **Para criar, modificar ou descartar um assembly**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **Para criar um gatilho CLR**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)  
  
## <a name="see-also"></a>Consulte também  
 [Gatilhos DML](dml-triggers.md)   
 [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [Acesso aos dados dos objetos de banco de dados CLR](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
