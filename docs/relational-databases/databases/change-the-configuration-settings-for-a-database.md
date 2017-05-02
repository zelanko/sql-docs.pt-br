---
title: "Alterar as definições de configuração de um banco de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database configuration [SQL Server]
- configuration options [SQL Server], databases
- modifying database configuration settings
ms.assetid: c29c3385-5043-400f-bb4e-044a4c9a9a4b
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 858cf7833f497051bbe494308036f3ab76f8befb
ms.lasthandoff: 04/11/2017

---
# <a name="change-the-configuration-settings-for-a-database"></a>Alterar as definições de configuração de um banco de dados
  Este tópico descreve como alterar opções em nível de banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Essas opções são exclusivas de cada banco de dados e não afetam outros bancos de dados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para alterar as configurações de opção para um banco de dados, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Apenas o administrador do sistema, proprietário do banco de dados, membros das funções de servidor fixas **sysadmin** e **dbcreator** e da função de banco de dados fixa **db_owner** podem modificar essas opções.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>Para alterar as configurações de opção para um banco de dados  
  
1.  No Pesquisador de Objetos conecte-se a uma instância [!INCLUDE[ssDE](../../includes/ssde-md.md)] , expanda o servidor, expanda **Bancos de Dados**, clique com o botão direito do mouse em um banco de dados e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades de Banco de Dados** , clique em **Opções** para acessar a maioria das definições de configuração. As configurações de arquivo e grupo de arquivos, espelhamento e envio de logs estão em suas páginas respectivas.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>Para alterar as configurações de opção para um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo define o modelo de recuperação e as opções de verificação de página de dados para o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
 [!code-sql[DatabaseDDL#AlterDatabase7](../../relational-databases/databases/codesnippet/tsql/change-the-configuration_1.sql)]  
  
 Para obter mais exemplos, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="see-also"></a>Consulte também  
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [Renomear um banco de dados](../../relational-databases/databases/rename-a-database.md)   
 [Reduzir um banco de dados](../../relational-databases/databases/shrink-a-database.md)  
  
  
