---
title: Excluir tabelas (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table deletions [SQL Server]
- deleting tables
- removing tables
- dropping tables
ms.assetid: ca6aa3e9-9885-44c3-bafc-aec441fd97ec
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3c9dc1c5650c98a925ff79a9bc78917a80d73656
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909894"
---
# <a name="delete-tables-database-engine"></a>Excluir tabelas (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Você pode excluir (descartar) uma tabela de seu banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!CAUTION]  
>  Pense cuidadosamente antes de excluir uma tabela. Se as consultas, as exibições, as funções definidas pelo usuário, os procedimentos armazenados ou os programas existentes se referirem a essa tabela, a exclusão do nome tornará esses objetivos inválidos.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para excluir uma tabela usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Você não pode descartar uma tabela que é referenciada por uma restrição FOREIGN KEY. A restrição FOREIGN KEY que faz referência ou a tabela de referência deve ser primeiramente descartada. Se a tabela de referência e a tabela que contém a chave primária forem descartadas na mesma instrução DROP TABLE, a tabela de referência deverá ser listada em primeiro lugar.  
  
-   Quando uma tabela for descartada, as regras ou os padrões da tabela perderão sua associação e quaisquer restrições ou gatilhos associados à tabela serão descartados automaticamente. Se você recriar uma tabela, deverá associar novamente as regras e padrões apropriados, recriar quaisquer gatilhos e adicionar todas as restrições necessárias.  
  
-   Se você remover uma tabela que contém uma coluna **varbinary (max)** com o atributo FILESTREAM, os dados armazenados no sistema de arquivos não serão removidos.  
  
-   DROP TABLE e CREATE TABLE não devem ser executados na mesma tabela no mesmo lote. Caso contrário, poderá ocorrer um erro inesperado.  
  
-   Qualquer exibição ou procedimento armazenado que faça referência à tabela descartada deverá ser excluído ou modificado explicitamente para remover a referência à tabela.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER no esquema ao qual a tabela pertence, permissão CONTROL na tabela ou associação na função de banco de dados fixa **db_ddladmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-table-from-the-database"></a>Para excluir uma tabela do banco de dados  
  
1.  No Pesquisador de Objetos, selecione a tabela que deseja excluir.  
  
2.  Clique com o botão direito do mouse na tabela e escolha **Excluir** no menu de atalho.  
  
3.  Uma caixa de mensagem solicitará que você confirme a exclusão. Clique em **Sim**.  

    > [!NOTE]  
    >  A exclusão de uma tabela automaticamente remove qualquer relação associada a ela.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-delete-a-table-in-query-editor"></a>Para excluir uma tabela no Editor de Consultas  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    DROP TABLE dbo.PurchaseOrderDetail;  
  
    ```  
  
 Para obter mais informações, veja [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  
  
  
