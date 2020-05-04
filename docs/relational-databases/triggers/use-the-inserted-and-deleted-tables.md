---
title: Usar as tabelas inseridas e excluídas | Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- inserted tables
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- INSTEAD OF triggers
- deleted tables
- INSERT statement [SQL Server], DML triggers
- DML triggers, deleted or inserted tables
ms.assetid: ed84567f-7b91-4b44-b5b2-c400bda4590d
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 242ae654ede8a827b89e630369965faee4505840
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220691"
---
# <a name="use-the-inserted-and-deleted-tables"></a>Usar as tabelas inseridas e excluídas
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  As instruções de gatilho DML usam duas tabelas especiais: a tabela excluída e as tabelas inseridas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria e gerencia automaticamente essas tabelas. É possível usar essas tabelas temporárias, residentes na memória, para testar os efeitos de algumas modificações de dados e para definir critérios para ações de gatilhos DML. Você não pode modificar diretamente os dados nas tabelas nem executar operações DDL (linguagem de definição de dados) nas tabelas, como CREATE INDEX.  
  
 Nos gatilhos DML, as tabelas inseridas e excluídas são usadas principalmente para executar o seguinte:  
  
-   Estender a integridade referencial entre as tabelas.  
  
-   Inserir ou atualizar dados nas tabelas adjacentes da exibição.  
  
-   Testar quanto a erros e aplicar as ações com base no erro.  
  
-   Identificar a diferença entre o estado de uma tabela antes e depois da modificação dos dados e executar ações com base nessa diferença.  
  
 A tabela excluída armazena cópias das linhas afetadas durante as instruções DELETE e UPDATE. Durante a execução da instrução DELETE ou UPDATE, as linhas são excluídas da tabela de gatilhos e transferidas para a tabela excluída. A tabela excluída e a tabela de gatilhos geralmente não têm nenhuma linha em comum.  
  
 A tabela inserida armazena cópias das linhas afetadas durante as instruções INSERT e UPDATE. Durante uma transação de inserção ou de atualização, novas linhas são adicionadas à tabela inserida e à tabela de gatilho. As linhas na tabela inserida são cópias das novas linhas na tabela de gatilhos.  
  
 Uma transação de atualização é semelhante à operação de exclusão seguida por uma operação de inserção, as linhas antigas são copiadas primeiro na tabela excluída e, em seguida, as novas linhas são copiadas na tabela de gatilhos e na tabela inserida.  
  
 Quando você definir os critérios para o gatilho, use adequadamente as tabelas inseridas e excluídas para a ação que acionou o gatilho. Embora referenciando a tabela excluída quando testar INSERT ou a tabela inserida quando testar DELETE não cause qualquer erro, essas tabelas de teste de gatilhos não contêm nenhuma linha nesses casos.  
  
> [!NOTE]  
>  Se as ações de gatilhos dependem do número de linhas que uma modificação de dados afeta, use os testes (como um exame de @@ROWCOUNT) para modificações de dados em várias linhas (uma instrução INSERT, DELETE ou UPDATE com base em uma instrução SELECT) e execute as ações apropriadas. Para obter mais informações, veja [Criar gatilhos DML para tratar várias linhas de dados](../../relational-databases/triggers/create-dml-triggers-to-handle-multiple-rows-of-data.md).
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não permite referências de coluna **text**, **ntext**ou **image** nas tabelas inseridas e excluídas para gatilhos AFTER. Entretanto, esses tipos de dados são incluídos somente para fins de compatibilidade com versões anteriores. O armazenamento preferencial para dados grandes é usar os tipos de dados **varchar(max)** , **nvarchar(max)** e **varbinary(max)** . Os gatilhos AFTER e INSTEAD OF dão suporte a dados **varchar(max)** , **nvarchar(max)** e **varbinary(max)** nas tabelas inseridas e excluídas. Para obter mais informações, veja [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 **Um exemplo do uso de tabela inserida em um gatilho para impor regras de negócio**  
  
 Como as restrições CHECK só podem referenciar as colunas nas quais a restrição de nível de coluna ou de nível de tabela é definida, qualquer restrição de tabela cruzada (neste caso, as regras de negócio) deverá ser definida como gatilho.  
  
 O exemplo a seguir cria um gatilho DML. Esse gatilho realiza uma verificação para ter certeza de que a avaliação de crédito do fornecedor é satisfatória quando for efetuar uma tentativa para inserir uma nova ordem de compra na tabela `PurchaseOrderHeader` . Para obter a avaliação de crédito do fornecedor correspondente à ordem de compra que acaba de ser inserida, a tabela `Vendor` deve ser referenciada e associada a uma tabela inserida. Se a classificação de crédito for muito baixa, uma mensagem será exibida e a inserção não será executada.
  
 [!code-sql[TriggerDDL#CreateTrigger3](../../relational-databases/triggers/codesnippet/tsql/use-the-inserted-and-del_1.sql)]  
  
## <a name="using-the-inserted-and-deleted-tables-in-instead-of-triggers"></a>Usando as tabelas inseridas e excluídas em gatilhos INSTEAD OF  
 As tabelas inseridas e excluídas passadas para os gatilhos INSTEAD OF definidos nas tabelas seguem as mesmas regras das tabelas inseridas e excluídas passadas para os gatilhos AFTER. O formato das tabelas inseridas e excluídas é o mesmo do formato da tabela na qual o gatilho INSTEAD OF está definido. Cada coluna das tabelas inseridas e excluídas é mapeada diretamente para uma coluna na tabela base.  
  
 As regras a seguir, relativas a quando uma instrução INSERT ou UPDATE, que faz referência a uma tabela com um gatilho INSTEAD OF, deve fornecer valores para colunas, são as mesmas, como se a tabela não tivesse um gatilho INSTEAD OF:  
  
-   Valores não podem ser especificados para colunas computadas ou colunas com tipo de dados **timestamp** .  
  
-   Valores não podem ser especificados com uma propriedade IDENTITY, a menos que IDENTITY_INSERT seja ON para aquela tabela. Quando IDENTITY_INSERT for ON, as instruções INSERT devem fornecer um valor.  
  
-   As instruções INSERT devem fornecer valores para todas as colunas NOT NULL que não têm restrições DEFAULT.  
  
-   Para qualquer coluna exceto computada, identidade ou colunas **timestamp** , os valores são opcionais para qualquer coluna que permita nulos ou qualquer coluna NOT NULL que tenha uma definição DEFAULT.  
  
 Quando uma instrução INSERT, UPDATE ou DELETE faz referência a uma exibição que tenha um gatilho INSTEAD OF, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] chama o gatilho em vez de tomar qualquer ação direta contra qualquer tabela. O gatilho deve usar as informações apresentadas nas tabelas inseridas e excluídas para construir as instruções necessárias para implementar a ação solicitada nas tabelas base, mesmo quando o formato das informações nas tabelas inseridas e excluídas construído para a exibição for diferente do formato dos dados nas tabelas base.  
  
 O formato das tabelas inseridas e excluídas passadas para o gatilho INSTEAD OF definido em uma exibição corresponde à lista de seleção da instrução SELECT definida para exibição. Por exemplo:   
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.EmployeeNames (BusinessEntityID, LName, FName)  
AS  
SELECT e.BusinessEntityID, p.LastName, p.FirstName  
FROM HumanResources.Employee AS e   
JOIN Person.Person AS p  
ON e.BusinessEntityID = p.BusinessEntityID;  
```  
  
 O conjunto de resultados desta exibição tem três colunas: uma coluna **int** e duas colunas **nvarchar** . As tabelas inseridas e excluídas passadas para um gatilho INSTEAD OF definido em uma exibição têm também uma coluna **int** denominada `BusinessEntityID`, uma coluna **nvarchar** denominada `LName`e uma coluna **nvarchar** denominada `FName`.  
  
 A lista de seleção de uma exibição pode também conter expressões que não mapeiam diretamente uma única coluna com base em tabelas. Algumas expressões de exibição, como um chamado de função ou de constante, podem não fazer referência a nenhuma coluna e podem ser ignoradas. Expressões complexas podem referenciar várias colunas, mesmo assim as colunas inseridas e excluídas têm apenas um valor para cada linha inserida. As mesmas questões se aplicam às expressões simples em uma exibição, caso elas façam referência a uma coluna computada que tenha uma expressão complexa. Um gatilho INSTEAD OF na exibição deve tratar desses tipos de expressões.  
  
  
