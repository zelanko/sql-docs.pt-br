---
title: Propriedade de banco de dados TRUSTWORTHY | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TRUSTWORTHY database property
ms.assetid: 64b2a53d-4416-4a19-acc0-664a61b45348
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 9ac99b46c31d67b0175fffa882dcf5411194930c
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025546"
---
# <a name="trustworthy-database-property"></a>Propriedade de banco de dados TRUSTWORTHY
  A propriedade de banco de dados TRUSTWORTHY é usada para indicar se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] confia no banco de dados e em seu conteúdo. Por padrão, esta configuração é OFF, mas pode ser definida como ON usando a instrução ALTER DATABASE. Por exemplo, `ALTER DATABASE AdventureWorks2012 SET TRUSTWORTHY ON;`.  
  
> [!NOTE]  
>  Para definir esta opção, é preciso ser um membro da função de servidor fixa **sysadmin** .  
  
 Essa propriedade pode ser usada para reduzir ameaças que podem ocorrer ao anexar um banco de dados que contenha um dos seguintes objetos:  
  
-   Assemblies maliciosos com um definição de permissão EXTERNAL_ACCESS ou UNSAFE. Para obter mais informações, consulte [CLR Integration Security](../clr-integration/security/clr-integration-security.md).  
  
-   Módulos maliciosos que são definidos para serem executados como usuários com altos privilégios. Para obter mais informações, veja [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-clause-transact-sql).  
  
 Essas duas situações exigem um grau específico de privilégios e estão protegidas pelos mecanismos adequados, quando usados no contexto de um banco de dados já anexado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, se o banco de dados estiver off-line, um usuário que tem acesso ao arquivo de banco de dados provavelmente poderá anexá-lo a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de sua preferência e adicionar conteúdo malicioso ao banco de dados. Quando bancos de dados são desanexados e anexados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], determinadas permissões são definidas nos dados e nos arquivos de log restringindo o acesso aos arquivos de banco de dados.  
  
 Como um banco de dados que é anexado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é confiável imediatamente, ele não tem permissão para acessar recursos além do escopo do banco de dados, até que seja explicitamente marcado como confiável. Além disso, os módulos que são criados para acessar recursos fora do banco de dados, e assemblies com as definições de permissão EXTERNAL_ACCESS e UNSAFE, têm requisitos adicionais para uma execução bem-sucedida.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
