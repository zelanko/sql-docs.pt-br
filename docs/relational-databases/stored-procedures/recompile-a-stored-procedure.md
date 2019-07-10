---
title: Recompilar um procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sp_recompile
- WITH RECOMPILE clause
- recompiling stored procedures
- stored procedures [SQL Server], recompiling
ms.assetid: b90deb27-0099-4fe7-ba60-726af78f7c18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 21298500f7d5bc135b8e9068c97e2928d1853b6f
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67583580"
---
# <a name="recompile-a-stored-procedure"></a>Recompilar um procedimento armazenado
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Este tópico descreve como recompilar um procedimento armazenado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Há três modos de fazer isso: a opção **WITH RECOMPILE** na definição do procedimento ou quando o procedimento é chamado, a dica de consulta **RECOMPILE** em instruções individuais ou usando o procedimento armazenado do sistema **sp_recompile**. Este tópico descreve como usar a opção WITH RECOMPILE ao criar uma definição de procedimento e executar um procedimento existente. Também descreve como usar o procedimento armazenado do sistema sp_recompile para recompilar um procedimento existente.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para recompilar um procedimento armazenado usando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Quando um procedimento é compilado pela primeira vez ou recompilado, o plano de consulta do procedimento é otimizado para o estado atual do banco de dados e seus objetos. Se um banco de dados passar por alterações significativas em seus dados ou estrutura, a recompilação de um procedimento atualizará e otimizará o plano de consulta do procedimento para essas alterações. Isso pode melhorar o desempenho do processamento do procedimento.  
  
-   Há momentos em que a recompilação de procedimento deve ser forçada e outros em que ela ocorre automaticamente. A recompilação automática ocorre sempre que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é reiniciado. Isso também ocorrerá se uma tabela subjacente referenciada pelo procedimento tiver passado por alterações de design físicas.  
  
-   Outro motivo para forçar a recompilação de um procedimento é neutralizar o comportamento “sugador de parâmetro” da compilação de procedimento. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa procedimentos armazenados, quaisquer valores de parâmetro usados pelo procedimento em sua compilação são incluídos como parte da geração do plano de consulta. Se esses valores representam aqueles típicos com os quais o procedimento é chamado subsequentemente, então o procedimento beneficia-se do plano de consulta cada vez que ele é compilado e executado. Se valores de parâmetros no procedimento forem frequentemente atípicos, forçar uma recompilação do procedimento e um novo plano baseado em valores de parâmetros diferentes poderá melhorar o desempenho.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece recompilação no nível da instrução de procedimentos. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recompila procedimentos armazenados, apenas a instrução que causou a recompilação é compilada, e não o procedimento completo.  
  
-   Se certas consultas em um procedimento usarem valores atípicos ou temporários regularmente, o desempenho do procedimento poderá ser melhorado com o uso da dica de consulta RECOMPILE nessas consultas. Como apenas as consultas que usam a dica de consulta serão recompiladas, em vez de o procedimento completo, o comportamento de recompilação no nível da instrução no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]será imitado. Além de usar os valores de parâmetro atuais do procedimento, a dica de consulta RECOMPILE também usa os valores de todas as variáveis locais no procedimento armazenado quando você compila a instrução. Para obter mais informações, veja [Dica de consulta (Transact-SQL)](../../t-sql/queries/hints-transact-sql-query.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Opção**WITH RECOMPILE**  
 Se a opção for usada quando a definição de procedimento for criada, serão necessárias as permissões CREATE PROCEDURE no banco de dados e ALTER no esquema no qual o procedimento está sendo criado.  
  
 Se essa opção for usada em uma instrução EXECUTE, as permissões de EXECUTE serão necessárias no procedimento. As permissões não são necessárias na instrução EXECUTE em si, mas permissões de execução são necessárias no procedimento referenciado na instrução EXECUTE. Para obter mais informações, veja [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
 Dica de consulta **RECOMPILE**  
 Esse recurso é usado quando o procedimento é criado e a dica é incluída em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] no procedimento. Portanto, isso requer a permissão CREATE PROCEDURE no banco de dados e a permissão ALTER no esquema no qual o procedimento está sendo criado.  
  
 Procedimento armazenado do sistema**sp_recompile**  
 Exige a permissão ALTER no procedimento especificado.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>Para recompilar um procedimento armazenado usando a opção WITH RECOMPILE  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo cria a definição de procedimento.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
    DROP PROCEDURE dbo.uspProductByVendor;  
GO  
CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
WITH RECOMPILE  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
    FROM Purchasing.Vendor AS v   
    JOIN Purchasing.ProductVendor AS pv   
      ON v.BusinessEntityID = pv.BusinessEntityID   
    JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID  
    WHERE v.Name LIKE @Name;  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>Para recompilar um procedimento armazenado usando a opção WITH RECOMPILE  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo cria um procedimento simples que retorna todos os funcionários (com os nomes e sobrenomes fornecidos), os cargos e os nomes de departamento em uma exibição.  
  
     E copie e cole o segundo exemplo de código na janela de consulta e clique em **Executar**. Isso executa o procedimento e recompila o plano de consulta do procedimento.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXECUTE HumanResources.uspGetAllEmployees WITH RECOMPILE;  
GO  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-sprecompile"></a>Para recompilar um procedimento armazenado usando sp_recompile  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo cria um procedimento simples que retorna todos os funcionários (com os nomes e sobrenomes fornecidos), os cargos e os nomes de departamento em uma exibição.  
  
     Em seguida, copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Isso não executa o procedimento, mas marca-o para recompilação de modo que seu plano de consulta seja atualizada na próxima vez em que o procedimento for executado.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'HumanResources.uspGetAllEmployees';  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um procedimento armazenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Modificar um procedimento armazenado](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Renomear um procedimento armazenado](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [Exibir a definição de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [Exibir as dependências de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
  
