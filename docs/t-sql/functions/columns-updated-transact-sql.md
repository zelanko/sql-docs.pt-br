---
title: COLUMNS_UPDATED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COLUMNS_UPDATED_TSQL
- COLUMNS_UPDATED
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS_UPDATED function
- testing columns
- column testing [SQL Server]
- updated columns
ms.assetid: 765fde44-1f95-4015-80a4-45388f18a42c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 29d95c36ddd87b41183eabc543ff3cfd7907b991
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064629"
---
# <a name="columnsupdated-transact-sql"></a>COLUMNS_UPDATED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essa função retorna um padrão de bit **varbinary** que indica as colunas inseridas ou atualizadas de uma tabela ou exibição. Use [!INCLUDE[tsql](../../includes/tsql-md.md)] em qualquer lugar no corpo de um gatilho INSERT ou UPDATE do `COLUMNS_UPDATED` para testar se o gatilho deve executar determinadas ações.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COLUMNS_UPDATED ( )   
```  
  
## <a name="return-types"></a>Tipos de retorno
**varbinary**
  
## <a name="remarks"></a>Remarks  
`COLUMNS_UPDATED` testa para UPDATE ou INSERT as ações executadas em várias colunas. Para testar as tentativas de UPDATE ou INSERT em uma coluna, use [UPDATE()](../../t-sql/functions/update-trigger-functions-transact-sql.md).
  
`COLUMNS_UPDATED` retorna um ou mais bytes ordenados da esquerda para a direita. O bit mais à direita de cada byte é o bit menos significativo. O mais à direita do byte mais à esquerda representa a primeira coluna na tabela; o próximo bit à esquerda representa a segunda coluna, e assim por diante. `COLUMNS_UPDATED` retornará vários bytes se a tabela na qual o gatilho foi criado contiver mais que oito colunas, ficando o byte menos significativo na extrema esquerda. `COLUMNS_UPDATED` retorna TRUE para todas as colunas em ações INSERT porque as colunas têm valores explícitos ou implícitos (NULL) inseridos.
  
Para testar as atualizações ou inserções feitas em colunas específicas, a sintaxe deve ser seguida por um operador bit a bit e um bitmask inteiro das colunas testadas. Por exemplo, digamos que a tabela **t1** contenha as colunas **C1**, **C2**, **C3**, **C4** e **C5**. Para verificar se as colunas **C2**, **C3** e **C4** foram todas atualizadas com sucesso (tendo a tabela **t1** um gatilho UPDATE), siga a sintaxe com **& 14**. Para testar se apenas a coluna **C2** foi atualizada, especifique **& 2**. Veja o [Exemplo A](#a-using-columns_updated-to-test-the-first-eight-columns-of-a-table) e o [Exemplo B](#b-using-columns_updated-to-test-more-than-eight-columns) para obter exemplos reais.
  
Use `COLUMNS_UPDATED` em qualquer lugar dentro de um gatilho INSERT ou UPDATE do [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
A coluna ORDINAL_POSITION da exibição INFORMATION_SCHEMA.COLUMNS não é compatível com o padrão de bit de colunas retornadas por `COLUMNS_UPDATED`. Para obter um padrão de bit compatível com `COLUMNS_UPDATED`, veja a propriedade `ColumnID` da função do sistema `COLUMNPROPERTY` ao consultar a exibição `INFORMATION_SCHEMA.COLUMNS`, como mostrado no exemplo a seguir.
  
```sql
SELECT TABLE_NAME, COLUMN_NAME,  
    COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME),  
    COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
```  

Se um gatilho se aplicar a uma coluna, o `COLUMNS_UPDATED` retornará como `true` ou `1`, mesmo que o valor da coluna permaneça inalterado. Isso é por design, e o gatilho deve implementar a lógica de negócios que determina se a operação de inserir/atualizar/excluir é permitida ou não. 
  
## <a name="column-sets"></a>Conjuntos de colunas
Quando um conjunto de coluna é definido em uma tabela, a função `COLUMNS_UPDATED` comporta-se das seguintes maneiras:
-   Ao atualizar explicitamente uma coluna membro do conjunto de colunas, o bit correspondente para aquela coluna é definido como 1, e o bit do conjunto de colunas é definido como 1.  
-   Ao atualizar explicitamente um conjunto de colunas, o bit do conjunto de colunas é definido como 1 e os bits para todas as colunas esparsas na tabela são definidos como 1.  
-   Para operações de inserção, todos os bits são definidos como 1.  
  
     Porque alterações a um conjunto de coluna fazem os bits de todas as colunas no conjunto de colunas serem redefinidos como 1, colunas inalteradas em um conjunto de colunas parecerão modificadas. Veja [Usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md) para obter mais informações sobre conjuntos de colunas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-columnsupdated-to-test-the-first-eight-columns-of-a-table"></a>A. Usando COLUMNS_UPDATED para testar as primeiras oito colunas de uma tabela  
Este exemplo cria duas tabelas: `employeeData` e `auditEmployeeData`. A tabela `employeeData` contém informações de folha de pagamento confidenciais de funcionários, e membros do departamento de recursos humanos podem modificá-las. Se o SSN (número do seguro social), o salário anual ou o número da conta bancária de um funcionário for alterado, um registro de auditoria será gerado e inserido na tabela de auditoria `auditEmployeeData`.
  
Com a função `COLUMNS_UPDATED()`, podemos rapidamente testar quaisquer alterações feitas a colunas contendo informações confidenciais de funcionários. Usar `COLUMNS_UPDATED()` dessa forma funcionará apenas quando você estiver tentando detectar alterações nas primeiras oito colunas da tabela.
  
```sql
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'employeeData')  
   DROP TABLE employeeData;  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'auditEmployeeData')  
   DROP TABLE auditEmployeeData;  
GO  
CREATE TABLE dbo.employeeData (  
   emp_id int NOT NULL PRIMARY KEY,  
   emp_bankAccountNumber char (10) NOT NULL,  
   emp_salary int NOT NULL,  
   emp_SSN char (11) NOT NULL,  
   emp_lname nchar (32) NOT NULL,  
   emp_fname nchar (32) NOT NULL,  
   emp_manager int NOT NULL  
   );  
GO  
CREATE TABLE dbo.auditEmployeeData (  
   audit_log_id uniqueidentifier DEFAULT NEWID() PRIMARY KEY,  
   audit_log_type char (3) NOT NULL,  
   audit_emp_id int NOT NULL,  
   audit_emp_bankAccountNumber char (10) NULL,  
   audit_emp_salary int NULL,  
   audit_emp_SSN char (11) NULL,  
   audit_user sysname DEFAULT SUSER_SNAME(),  
   audit_changed datetime DEFAULT GETDATE()  
   );  
GO  
CREATE TRIGGER dbo.updEmployeeData   
ON dbo.employeeData   
AFTER UPDATE AS  
/* Check whether columns 2, 3 or 4 have been updated. If any or all  
columns 2, 3 or 4 have been changed, create an audit record. The
bitmask is: power(2, (2-1)) + power(2, (3-1)) + power(2, (4-1)) = 14. To test   
whether all columns 2, 3, and 4 are updated, use = 14 instead of > 0  
(below). */
  
   IF (COLUMNS_UPDATED() & 14) > 0  
/* Use IF (COLUMNS_UPDATED() & 14) = 14 to see whether all columns 2, 3,   
and 4 are updated. */  
      BEGIN  
-- Audit OLD record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'OLD',   
            del.emp_id,  
            del.emp_bankAccountNumber,  
            del.emp_salary,  
            del.emp_SSN  
         FROM deleted del;  
  
-- Audit NEW record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'NEW',  
            ins.emp_id,  
            ins.emp_bankAccountNumber,  
            ins.emp_salary,  
            ins.emp_SSN  
         FROM inserted ins;  
   END;  
GO  
  
/* Inserting a new employee does not cause the UPDATE trigger to fire. */  
INSERT INTO employeeData  
   VALUES ( 101, 'USA-987-01', 23000, 'R-M53550M', N'Mendel', N'Roland', 32);  
GO  
  
/* Updating the employee record for employee number 101 to change the   
salary to 51000 causes the UPDATE trigger to fire and an audit trail to   
be produced. */  
  
UPDATE dbo.employeeData  
   SET emp_salary = 51000  
   WHERE emp_id = 101;  
GO  
SELECT * FROM auditEmployeeData;  
GO  
  
/* Updating the employee record for employee number 101 to change both   
the bank account number and social security number (SSN) causes the   
UPDATE trigger to fire and an audit trail to be produced. */  
  
UPDATE dbo.employeeData  
   SET emp_bankAccountNumber = '133146A0', emp_SSN = 'R-M53550M'  
   WHERE emp_id = 101;  
GO  
SELECT * FROM dbo.auditEmployeeData;  
  
GO  
```  
  
### <a name="b-using-columnsupdated-to-test-more-than-eight-columns"></a>B. Usando COLUMNS_UPDATED para testar mais de oito colunas  
Para testar atualizações que afetam outras colunas além das oito primeiras colunas da tabela, use a função `SUBSTRING` para testar o bit correto retornado por `COLUMNS_UPDATED`. Este exemplo testa as atualizações que afetam as colunas `3`, `5` e `9` na tabela `AdventureWorks2012.Person.Person`.
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.uContact2', N'TR') IS NOT NULL  
    DROP TRIGGER Person.uContact2;  
GO  
CREATE TRIGGER Person.uContact2 ON Person.Person  
AFTER UPDATE AS  
    IF ( (SUBSTRING(COLUMNS_UPDATED(), 1, 1) & 20 = 20)   
        AND (SUBSTRING(COLUMNS_UPDATED(), 2, 1) & 1 = 1) )   
    PRINT 'Columns 3, 5 and 9 updated';  
GO  
  
UPDATE Person.Person   
   SET NameStyle = NameStyle,  
      FirstName=FirstName,  
      EmailPromotion=EmailPromotion;  
GO  
```  
  
## <a name="see-also"></a>Confira também
[Operadores bit a bit &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
[UPDATE&#40;&#41; &#40;Transact-SQL&#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)
  
  
