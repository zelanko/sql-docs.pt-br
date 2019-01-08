---
title: Opção de configuração de servidor cross db ownership chaining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cross-database ownership chaining
- cross db ownership chaining option
- chaining ownership
ms.assetid: 7b2d49f2-b91c-4aee-a52b-6cc49bed03af
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5630579e787a3bfcb5d64ee3bcf0ec5bee368611
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52639211"
---
# <a name="cross-db-ownership-chaining-server-configuration-option"></a>Opção cross db ownership chaining de configuração de servidor
  Use a opção **cross db ownership chaining** para configurar o encadeamento de propriedades de bancos de dados em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Essa opção de servidor permite que você controle o encadeamento de propriedade no nível do banco de dados ou em todos os bancos de dados:  
  
-   Quando **cross db ownership chaining** estiver desativado (0) para a instância, o encadeamento de propriedades de bancos de dados estará desabilitado para todos os bancos de dados.  
  
-   Quando **cross db ownership chaining** estiver ativado (1) para a instância, estará ativado para todos os bancos de dados.  
  
-   Você pode definir o encadeamento de propriedades de banco de dados para bancos de dados individuais com a cláusula SET da instrução ALTER DATABASE. Se você estiver criando um novo banco de dados, poderá definir a opção cross db ownership chaining para o novo banco de dados com a instrução CREATE DATABASE.  
  
     A definição da opção **cross db ownership chaining** como 1 não é recomendada, a menos que todos os bancos de dados hospedados pela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisem participar do encadeamento de propriedades de bancos de dados e que você esteja ciente das implicações de segurança dessa configuração.  
  
## <a name="controlling-cross-database-ownership-chaining"></a>Controlando o encadeamento de propriedades de banco de dados  
 Antes de ativar ou desativar o encadeamento de propriedades de banco de dados, considere o seguinte:  
  
-   É necessário ser um membro da função de servidor fixa **sysadmin** para ativar ou desativar o encadeamento de propriedades de bancos de dados.  
  
-   Antes de desativar o encadeamento de propriedades de banco de dados em um servidor de produção, teste completamente todos os aplicativos, inclusive aplicativos de terceiros, para assegurar que as alterações não afetem a funcionalidade do aplicativo.  
  
-   Você poderá alterar a opção **cross db ownership chaining** enquanto o servidor estiver em execução, se especificar RECONFIGURE com **sp_configure**.  
  
-   Se houver bancos de dados que exijam o encadeamento de propriedades de bancos de dados, a prática recomendada é desativar a opção **cross db ownership chaining** para a instância usando **sp_configure**e depois ativar o encadeamento de propriedades de bancos de dados para bancos de dados individuais que o exijam usando a instrução ALTER DATABASE.  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
