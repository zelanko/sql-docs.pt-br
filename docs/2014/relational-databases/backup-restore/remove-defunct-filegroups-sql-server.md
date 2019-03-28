---
title: Remover grupos de arquivos extintos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], defunct filegroups
- defunct filegroups
- restoring filegroups [SQL Server]
- deferred transactions
- filegroups [SQL Server], defunct
- unrestored filegroups
ms.assetid: 055f9c6a-5c18-4942-98e7-ec918f0ff975
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2a59277110d91ffd40a2db7d62fd3a01aa109dfc
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536628"
---
# <a name="remove-defunct-filegroups-sql-server"></a>Remover grupos de arquivos expirados (SQL Server)
  Este tópico descreve como remover grupos de arquivos expirados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para remover grupos de arquivos expirados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Este tópico é relevante para bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contêm vários arquivos ou grupos de arquivos; no modelo simples, ele é relevante somente para grupos de arquivos somente leitura.  
  
-   Todos os arquivos em um grupo de arquivos tornam-se extintos quando um grupo de arquivos off-line é removido.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Se um grupo de arquivos não recuperado não precisar mais ser restaurado, você poderá criar o grupo de arquivos *expirado* , removendo-o do banco de dados. O grupo de arquivos expirado não pode mais ser restaurado nesse banco de dados, mas seus metadados permanecem. Depois que o grupo de arquivos expirar, o banco de dados poderá ser reinicializado e a recuperação tornará o banco de dados consistente nos grupos de arquivos restaurados.  
  
     Por exemplo, a criação de um grupo de arquivos expirado é uma opção para resolver transações adiadas causadas por um grupo de arquivos offline que você já não quer mais no banco de dados. Transações que foram adiadas porque o grupo de arquivos estava offline são removidas desse estado depois que o grupo de arquivos é considerado extinto. Para obter mais informações, veja [Transações adiadas &#40;SQL Server&#41;](deferred-transactions-sql-server.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-remove-defunct-filegroups"></a>Para remover grupos de arquivos expirados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados do qual deseja excluir o arquivo e depois clique em **Propriedades**.  
  
3.  Selecione a página **Arquivos** .  
  
4.  Na grade **Arquivos de bancos de dados** , selecione os arquivos a serem excluídos, clique em **Remover**e em **OK**.  
  
5.  Selecione a página **Grupos de Arquivos** .  
  
6.  Na grade **Linhas** , selecione o grupo de arquivos a ser excluído, clique em **Remover**e em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-remove-defunct-filegroups"></a>Para remover grupos de arquivos expirados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. (**Observação:** Este exemplo supõe que os arquivos e o grupo de arquivos já existem. Para criar esses objetos, veja o exemplo B no tópico [Opções de arquivos e grupos de arquivos ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).) O primeiro exemplo remove os arquivos `test1dat3` e `test1dat4` do grupo de arquivos expirados usando a instrução `ALTER DATABASE` com a cláusula `REMOVE FILE`. O segundo exemplo remove o grupo de arquivos expirados `Test1FG1` usando a cláusula `REMOVE FILEGROUP`.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat3 ;  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4 ;  
GO  
  
```  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILEGROUP Test1FG1 ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [Transações adiadas &#40;SQL Server&#41;](deferred-transactions-sql-server.md)   
 [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](file-restores-full-recovery-model.md)   
 [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](file-restores-simple-recovery-model.md)   
 [Restauração online &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [Restaurar páginas &#40;SQL Server&#41;](restore-pages-sql-server.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
