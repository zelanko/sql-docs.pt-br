---
title: IDENTITY (propriedade) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY property
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY property
- autonumbers, identity numbers
ms.assetid: 8429134f-c821-4033-a07c-f782a48d501c
caps.latest.revision: 27
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0d7279f49be627b85ee227968cb6f7f6d22436e1
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38031664"
---
# <a name="create-table-transact-sql-identity-property"></a>CREATE TABLE (Transact-SQL) IDENTITY (Propriedade)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Cria uma coluna de identidade em uma tabela. Esta propriedade é usada com as instruções CREATE TABLE e ALTER TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  A propriedade IDENTITY é diferente da propriedade**Identity** de SQL-DMO que expõe a propriedade de identidade de linha de uma coluna.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
IDENTITY [ (seed , increment) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *seed*  
 É o valor usado para a primeira linha carregada na tabela.  
  
 *increment*  
 É o valor de incremento adicionado ao valor de identidade da linha anterior que foi carregada.  
  
 Você deve especificar seed e increment, ou nenhum dos dois. Se nenhum for especificado, o padrão será (1,1).  
  
## <a name="remarks"></a>Remarks  
 As colunas de identidade podem ser usadas para gerar valores de chave. A propriedade de identidade em uma coluna garante o seguinte:  
  
-   Cada novo valor é gerado com base nos valores de seed e increment atuais.  
  
-   Cada novo valor para uma transação específica é diferente de outras transações simultâneas na tabela.  
  
 A propriedade de identidade em uma coluna não garante o seguinte:  
  
-   **Exclusividade do valor** – a exclusividade deve ser imposta usando um **PRIMARY KEY** ou restrição **UNIQUE** ou índice **UNIQUE**.  
  
-   **Valores consecutivos em uma transação** – não é garantido que uma transação que insere várias linhas vá obter valores consecutivos para as linhas porque as demais inserções simultâneas podem ocorrer na tabela. Se os valores precisarem ser consecutivos, a transação deverá usar um bloqueio exclusivo na tabela ou usar o nível de isolamento **SERIALIZABLE**.  
  
-   **Valores consecutivos após o reinício do servidor ou outras falhas** – o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode armazenar em cache valores de identidade por questões de desempenho e alguns dos valores atribuídos podem ser perdidos durante uma falha de banco de dados ou uma reinicialização do servidor. Isso pode resultar em intervalos no valor de identidade após a inserção. Se não forem aceitos intervalos, o aplicativo deverá usar seu próprio mecanismo para gerar valores de chave. Usar um gerador de sequência com a opção **NOCACHE** pode limitar os intervalos de transações que nunca são confirmadas.  
  
-   **Reutilização de valores** – para determinada propriedade de identidade com seed/increment específicos, os valores de identidade não são reutilizados pelo mecanismo. Se uma instrução de inserção específica falhar ou se a instrução de inserção for revertida, os valores de identidade consumidos serão perdidos e não serão gerados novamente. Isso pode resultar em intervalos quando os valores de identidade subsequentes são gerados.  
  
 Essas restrições são parte do design para melhorar o desempenho, e por serem aceitáveis em muitas situações comuns. Se você não pode usar valores de identidade devido a essas restrições, crie uma tabela separada contendo um valor atual e gerencie o acesso à tabela e a atribuição de número com seu aplicativo.  
  
 Se uma tabela com uma coluna de identidade for publicada para replicação, a coluna de identidade deverá ser gerenciada de uma forma apropriada para o tipo de replicação usado. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 Apenas uma coluna de identidade pode ser criada por tabela.  
  
 Em tabelas com otimização de memória, a semente e o incremento devem ser definidos para 1.1. Configurar seed ou increment como um valor diferente de 1 resulta no seguinte erro: o uso de valores seed e increment diferentes de 1 não é compatível com tabelas com otimização de memória.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-identity-property-with-create-table"></a>A. Usando a propriedade IDENTITY com CREATE TABLE  
 O exemplo a seguir cria uma nova tabela que usa a propriedade `IDENTITY` para um número de identificação automaticamente incrementando.  
  
```  
USE AdventureWorks2012;  
  
IF OBJECT_ID ('dbo.new_employees', 'U') IS NOT NULL  
   DROP TABLE new_employees;  
GO  
CREATE TABLE new_employees  
(  
 id_num int IDENTITY(1,1),  
 fname varchar (20),  
 minit char(1),  
 lname varchar(30)  
);  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Karin', 'F', 'Josephs');  
  
INSERT new_employees  
   (fname, minit, lname)  
VALUES  
   ('Pirkko', 'O', 'Koskitalo');  
```  
  
### <a name="b-using-generic-syntax-for-finding-gaps-in-identity-values"></a>B. Usando sintaxe genérica para localizar intervalos em valores de identidade  
 O exemplo a seguir mostra a sintaxe genérica para localizar intervalos em valores de identidade quando os dados são removidos.  
  
> [!NOTE]  
>  A primeira parte do script [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir foi criada apenas para fins de ilustração. Você pode executar o script [!INCLUDE[tsql](../../includes/tsql-md.md)] que inicia com o comentário: `-- Create the img table`.  
  
```  
-- Here is the generic syntax for finding identity value gaps in data.  
-- The illustrative example starts here.  
SET IDENTITY_INSERT tablename ON;  
DECLARE @minidentval column_type;  
DECLARE @maxidentval column_type;  
DECLARE @nextidentval column_type;  
SELECT @minidentval = MIN($IDENTITY), @maxidentval = MAX($IDENTITY)  
    FROM tablename  
IF @minidentval = IDENT_SEED('tablename')  
   SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('tablename')  
   FROM tablename t1  
   WHERE $IDENTITY BETWEEN IDENT_SEED('tablename') AND   
      @maxidentval AND  
      NOT EXISTS (SELECT * FROM tablename t2  
         WHERE t2.$IDENTITY = t1.$IDENTITY +   
            IDENT_INCR('tablename'))  
ELSE  
   SELECT @nextidentval = IDENT_SEED('tablename');  
SET IDENTITY_INSERT tablename OFF;  
-- Here is an example to find gaps in the actual data.  
-- The table is called img and has two columns: the first column   
-- called id_num, which is an increasing identification number, and the   
-- second column called company_name.  
-- This is the end of the illustration example.  
  
-- Create the img table.  
-- If the img table already exists, drop it.  
-- Create the img table.  
IF OBJECT_ID ('dbo.img', 'U') IS NOT NULL  
   DROP TABLE img;  
GO  
CREATE TABLE img (id_num int IDENTITY(1,1), company_name sysname);  
INSERT img(company_name) VALUES ('New Moon Books');  
INSERT img(company_name) VALUES ('Lucerne Publishing');  
-- SET IDENTITY_INSERT ON and use in img table.  
SET IDENTITY_INSERT img ON;  
  
DECLARE @minidentval smallint;  
DECLARE @nextidentval smallint;  
SELECT @minidentval = MIN($IDENTITY) FROM img  
 IF @minidentval = IDENT_SEED('img')  
    SELECT @nextidentval = MIN($IDENTITY) + IDENT_INCR('img')  
    FROM img t1  
    WHERE $IDENTITY BETWEEN IDENT_SEED('img') AND 32766 AND  
      NOT    EXISTS (SELECT * FROM img t2  
          WHERE t2.$IDENTITY = t1.$IDENTITY + IDENT_INCR('img'))  
 ELSE  
    SELECT @nextidentval = IDENT_SEED('img');  
SET IDENTITY_INSERT img OFF;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_INCR &#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITY &#40;função&#41; &#40;Transact-SQL&#41;](../../t-sql/functions/identity-function-transact-sql.md)   
 [IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md)   
 [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
