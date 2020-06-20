---
title: Executar operações de índice online | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index online operations [SQL Server]
- online index operations
- ONLINE option
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4d09bd99a0eaec5fdb433bd8c33351d7622957a2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049868"
---
# <a name="perform-index-operations-online"></a>Executar operações de índice online
  Este tópico descreve como criar, recriar ou descartar índices online no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção ONLINE permite acesso simultâneo de usuários aos dados da tabela subjacente ou de índice cluster e qualquer índice não cluster associado durante essas operações de índice. Por exemplo, enquanto um índice cluster estiver sendo recriado por um usuário, esse usuário e os outros poderão continuar atualizando e consultando os dados subjacentes. Quando você executa operações de DDL (linguagem de definição de dados) offline, como a compilação ou recompilação de um índice clusterizado, essas operações mantêm bloqueios exclusivos nos dados subjacentes e índices associados. Isso evita modificações e consultas aos dados subjacentes até que a operação de índice esteja concluída.  
  
> [!NOTE]  
>  As operações de índice online não estão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para recriar um índice online, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Nós recomendamos a execução de operações de índice online em ambientes empresariais que funcionam 24 horas por dia, sete dias por semana, nos quais a necessidade para atividade de usuário simultânea durante as operações de índice é vital.  
  
-   A opção ONLINE está disponível nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir.  
  
    -   [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql)  
  
    -   [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql)  
  
    -   [DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql)  
  
    -   [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) (para adicionar ou remover restrições UNIQUE ou PRIMARY KEY com a opção de índice CLUSTERED)  
  
-   Por obter mais informações sobre limitação e restrições sobre como criar, recriar ou descartar índices online, consulte [Diretrizes para operações de índice online](guidelines-for-online-index-operations.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-rebuild-an-index-online"></a>Para recriar um índice online  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o banco de dados que contém a tabela na qual você deseja recriar um índice online.  
  
2.  Expanda a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja recriar um índice online.  
  
4.  Expanda a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice que você quer recriar online e selecione **Propriedades**.  
  
6.  Em **Selecione uma página**, selecione **Opções**.  
  
7.  Selecione **Permitir processamento DML online**e selecione **Verdadeiro** na lista.  
  
8.  Clique em **OK**.  
  
9. Clique com o botão direito do mouse no índice que você quer recriar online e selecione **Recompilar**.  
  
10. Na caixa de diálogo **Recriar Índices** , verifique se o índice correto está na grade **Índices a serem recriados** e clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-rebuild-or-drop-an-index-online"></a>Para criar, recriar ou descartar um índice online  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo reconstrói um online existente  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER INDEX AK_Employee_NationalIDNumber ON HumanResources.Employee  
    REBUILD WITH (ONLINE = ON);  
    GO  
    ```  
  
     O exemplo a seguir exclui um índice clusterizado online e move a tabela resultante (heap) para o grupo de arquivos `NewGroup` usando a cláusula `MOVE TO` . As exibições do catálogo `sys.indexes`, `sys.tables`e `sys.filegroups` são consultadas para verificar o posicionamento do índice e da tabela nos grupos de arquivos antes e depois da movimentação.  
  
     [!code-sql[IndexDDL#DropIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/dropindex.sql#dropindex4)]  
  
 Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
  
  
