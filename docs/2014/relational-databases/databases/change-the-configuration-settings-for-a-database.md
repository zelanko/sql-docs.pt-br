---
title: Alterar as definições de configuração de um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database configuration [SQL Server]
- configuration options [SQL Server], databases
- modifying database configuration settings
ms.assetid: c29c3385-5043-400f-bb4e-044a4c9a9a4b
caps.latest.revision: 28
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c766596bd49664773d0345b292079843fef52a46
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130770"
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
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>Para alterar as configurações de opção para um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo define o modelo de recuperação e as opções de verificação de página de dados para o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
 [!code-sql[DatabaseDDL#AlterDatabase7](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase7)]  
  
 Para obter mais exemplos, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
## <a name="see-also"></a>Consulte também  
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)   
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)   
 [Renomear um banco de dados](rename-a-database.md)   
 [Reduzir um banco de dados](shrink-a-database.md)  
  
  
