---
title: Habilitar o Stretch Database para uma tabela
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, enabling table
- enabling table for Stretch Database
ms.assetid: de4ac0c5-46ef-4593-a11e-9dd9bcd3ccdc
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 49d3f7fa266be69c767b0fb0450cc6898351f39b
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843813"
---
# <a name="enable-stretch-database-for-a-table"></a>Habilitar o Stretch Database para uma tabela
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Para configurar uma tabela para o Stretch Database, selecione **Stretch | Habilitar** para uma tabela no SQL Server Management Studio a fim de abrir o assistente **Habilitar Tabela para Stretch**. Você também pode usar o Transact-SQL para habilitar o Stretch Database em uma tabela existente ou para criar uma nova tabela com o Stretch Database habilitado.  
  
-   Se você armazenar dados frios em uma tabela separada, poderá migrar a tabela inteira.  
  
-   Se a tabela contiver dados quentes e frios, será possível especificar uma função de filtro para selecionar as linhas a serem migradas.    
 
 **Pré-requisitos**. Se você selecionar **Stretch | Habilitar** para uma tabela e ainda não tiver habilitado o Stretch Database para o banco de dados, o assistente configurará primeiro o banco de dados para o Stretch Database. Siga as etapas em [Comece executando o Assistente para Habilitar o Banco de Dados para Stretch](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md) em vez das etapas deste artigo.  
  
 **Permissões**. A habilitação do Stretch Database em um banco de dados ou em uma tabela requer permissões db_owner. A habilitação do Stretch Database em uma tabela também requer permissões ALTER na tabela.  

 > [!NOTE]
 > Mais tarde, se você desabilitar o Stretch Database, lembre-se de que desabilitar uma tabela ou um banco de dados do Stretch Database não excluirá o objeto remoto. Se você quiser excluir a tabela remota ou o banco de dados remoto, descarte-o(a) usando o Portal de Gerenciamento do Azure. Os objetos remotos continuam incorrendo em custos do Azure até que você os exclua manualmente.
 
##  <a name="EnableWizardTable"></a> Usar o assistente para habilitar o Stretch Database em uma tabela  
 **Iniciar o assistente**  
 1.  No SQL Server Management Studio, no Pesquisador de objetos, selecione a tabela na qual você deseja habilitar o Stretch.  
  
2.  Clique com o botão direito do mouse e selecione **Stretch**, e depois selecione **Habilitar** para iniciar o assistente.  
  
 **Introdução**  
 Verifique o objetivo do assistente e os pré-requisitos.  
  
 **Selecionar tabelas do banco de dados**  
 Confirme se a tabela que você quer habilitar é exibida e selecionada.  
  
 Você pode migrar uma tabela inteira ou especificar uma função de filtro simples no assistente. Se você desejar usar um tipo diferente de função de filtro para selecionar as linhas a serem migradas, siga um destes procedimentos.  
  
-   Saia do assistente e execute a instrução ALTER TABLE para habilitar o Stretch para a tabela e especificar uma função de filtro.  
  
-   Execute a instrução ALTER TABLE para especificar uma função de filtro depois que você sair do assistente. Para as etapas obrigatórias, consulte [Adicionar uma função de filtro após executar o assistente](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz).  
  
 A sintaxe ALTER TABLE é descrita posteriormente neste artigo.  
  
 **Resumo**  
 Examine os valores que você inseriu e as opções selecionadas no assistente. Em seguida, escolha **Concluir** para habilitar o Stretch.  
  
 **Resultados**  
 Analise os resultados.  
  
##  <a name="EnableTSQLTable"></a> Usar o Transact-SQL para habilitar o Stretch Database em uma tabela  
 Você pode habilitar o Stretch Database para uma tabela existente ou criar uma nova tabela com o Stretch Database habilitado usando Transact-SQL.  
  
### <a name="options"></a>Opções  
 Use as seguintes opções ao executar CREATE TABLE ou ALTER TABLE para habilitar o Stretch Database em uma tabela.  
  
-   Opcionalmente, use a cláusula `FILTER_PREDICATE = <function>` para especificar uma função a fim de selecionar linhas a serem migradas se a tabela contiver dados quentes e frios. O predicado deve chamar uma função embutida com valor de tabela. Para obter mais informações, consulte [Selecione linhas para migrar usando uma função de filtro](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). Se você não especificar uma função de filtro, a tabela inteira será migrada.  
  
    > [!IMPORTANT]  
    > Se você fornecer uma função de filtro precária, a migração de dados também será precária. O Stretch Database aplica a função de filtro à tabela usando o operador CROSS APPLY.  
  
-   Especifique `MIGRATION_STATE = OUTBOUND` para iniciar a migração de dados imediatamente ou  `MIGRATION_STATE = PAUSED` para adiar o início da migração de dados.  
  
### <a name="enable-stretch-database-for-an-existing-table"></a>Habilitar o Stretch Database para uma tabela existente  
 Para configurar uma tabela existente para o Stretch Database, execute o comando ALTER TABLE.  
  
 Aqui está um exemplo que migra a tabela inteira e começa a migração de dados imediatamente.  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 Aqui está um exemplo que migra apenas as linhas identificadas pela função com valor de tabela embutida `dbo.fn_stretchpredicate` e adia a migração de dados. Para obter mais informações sobre a função de filtro, veja [Select rows to migrate by using a filter function (Selecionar linhas a serem migradas usando uma função de filtro)](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
 GO
```  
  
 Para obter mais informações, consulte [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
### <a name="create-a-new-table-with-stretch-database-enabled"></a>Criar uma nova tabela com o Stretch Database habilitado  
 Para criar uma nova tabela com o Stretch Database habilitado, execute o comando CREATE TABLE.  
  
 Aqui está um exemplo que migra a tabela inteira e começa a migração de dados imediatamente.  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name>
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 Aqui está um exemplo que migra apenas as linhas identificadas pela função com valor de tabela embutida `dbo.fn_stretchpredicate` e adia a migração de dados. Para obter mais informações sobre a função de filtro, veja [Select rows to migrate by using a filter function (Selecionar linhas a serem migradas usando uma função de filtro)](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name> 
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
GO  
```  
  
 Para obter mais informações, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
  
