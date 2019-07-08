---
title: Aumentar o tamanho de um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], size
- increasing database size
- database size [SQL Server], increasing
- size [SQL Server], databases
ms.assetid: 14f4206d-3afa-4ba9-9849-23e81d63306d
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 31080369230401094587cb392a89d0262a6f1bfa
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67585303"
---
# <a name="increase-the-size-of-a-database"></a>Aumentar o tamanho de um banco de dados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como aumentar o tamanho de um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. O banco de dados é expandido ao aumentar o tamanho de um arquivo de dados ou de log existente ou ao adicionar um novo arquivo ao banco de dados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para aumentar o tamanho de um banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Você não pode adicionar ou remover um arquivo enquanto uma instrução BACKUP está em execução.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-increase-the-size-of-a-database"></a>Para aumentar o tamanho de um banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados para aumentá-lo e clique em **Propriedades**.  
  
3.  Em **Propriedades do Banco de Dados**, selecione a página **Arquivos** .  
  
4.  Para aumentar o tamanho de um arquivo existente, aumente o valor na coluna **Tamanho inicial (MB)** para o arquivo. Você deve aumentar o tamanho do banco de dados em pelo menos 1 megabyte.  
  
5.  Para aumentar o tamanho do banco de dados adicionando um novo arquivo, clique em **Adicionar** e, depois, digite os valores para o novo arquivo. Para obter mais informações, consulte [adicionar dados ou arquivos de Log para um banco de dados](../../relational-databases/databases/add-data-or-log-files-to-a-database.md).  
  
6.  Clique em **OK**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-increase-the-size-of-a-database"></a>Para aumentar o tamanho de um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo aumenta o tamanho do arquivo `test1dat3`.  
  
 [!code-sql[DatabaseDDL#AlterDatabase5](../../relational-databases/databases/codesnippet/tsql/increase-the-size-of-a-d_1.sql)]  
  
 Para obter mais exemplos, consulte [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar arquivos de dados ou de log a um banco de dados](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)   
 [Reduzir um banco de dados](../../relational-databases/databases/shrink-a-database.md)  
  
  
