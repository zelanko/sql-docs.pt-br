---
title: Modificar um procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying stored procedures
- editing stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: 13396239-6100-48ce-aa34-461358d99c92
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a7cbc7981817a6c62db378976fe36a4dc753c6b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63015877"
---
# <a name="modify-a-stored-procedure"></a>Modificar um procedimento armazenado
    
##  <a name="Top"></a> Este tópico descreve como modificar um procedimento armazenado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de começar:**  [Limitações e Restrições](#Restrictions), [Segurança](#Security)  
  
-   **Para alterar um procedimento usando:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] não podem ser modificados para serem procedimentos armazenados CLR e vice-versa.  
  
 Se a definição de procedimento anterior foi criada com WITH ENCRYPTION ou WITH RECOMPILE, essas opções estarão habilitadas somente se tiverem sido incluídas na instrução ALTER PROCEDURE.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER PROCEDURE no procedimento.  
  
##  <a name="Procedures"></a> Como modificar um procedimento armazenado  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para modificar um procedimento no Management Studio**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados ao qual pertence o procedimento e expanda **Programação**.  
  
3.  Expanda **Procedimentos Armazenados**, clique com o botão direito do mouse no procedimento a modificar e clique em **Modificar**.  
  
4.  Modifique o texto do procedimento armazenado.  
  
5.  Para testar a sintaxe, no menu **Consulta** , clique em **Analisar**.  
  
6.  Para salvar as modificações na definição do procedimento, no menu **Consulta** , clique em **Executar**.  
  
7.  Para salvar a definição do procedimento atualizada, como um script [!INCLUDE[tsql](../../includes/tsql-md.md)] , no menu **Arquivo** , clique em **Salvar como**. Aceite o nome de arquivo ou substitua-o por um nome novo e, então, clique em **Salvar**.  
  
> [!IMPORTANT]  
>  Valide todas as entradas de usuário. Não concatene a entrada de usuário antes de validá-la. Nunca execute um comando construído por uma entrada de usuário inválida.  
  
###  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para modificar um procedimento no Editor de Consultas**  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e o banco de dados ao qual o procedimento pertence. Ou, na barra de ferramentas, selecione o banco de dados na lista de bancos de dados disponíveis. Neste exemplo, selecione o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
3.  No menu **Arquivo** , clique em **Nova Consulta**.  
  
4.  Copie e cole o exemplo a seguir no editor de consultas. O exemplo cria o procedimento `uspVendorAllInfo` , que retorna os nomes de todos os fornecedores no banco de dados [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , os produtos que eles fornecem, suas classificações de crédito e sua disponibilidade.  
  
    ```  
  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
5.  No menu **Arquivo** , clique em **Nova Consulta**.  
  
6.  Copie e cole o exemplo a seguir no editor de consultas. O exemplo modifica o procedimento `uspVendorAllInfo` . A cláusula EXECUTE AS CALLER é removida e o corpo do procedimento é modificado para retornar apenas os fornecedores que fornecem o produto especificado. As funções `LEFT` e `CASE` personalizam a aparência do conjunto de resultados.  
  
    ```  
    ALTER PROCEDURE Purchasing.uspVendorAllInfo  
        @Product varchar(25)   
    AS  
        SET NOCOUNT ON;  
        SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
        'Rating' = CASE v.CreditRating   
            WHEN 1 THEN 'Superior'  
            WHEN 2 THEN 'Excellent'  
            WHEN 3 THEN 'Above average'  
            WHEN 4 THEN 'Average'  
            WHEN 5 THEN 'Below average'  
            ELSE 'No rating'  
            END  
        , Availability = CASE v.ActiveFlag  
            WHEN 1 THEN 'Yes'  
            ELSE 'No'  
            END  
        FROM Purchasing.Vendor AS v   
        INNER JOIN Purchasing.ProductVendor AS pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product AS p   
          ON pv.ProductID = p.ProductID   
        WHERE p.Name LIKE @Product  
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
7.  Para salvar as modificações na definição do procedimento, no menu **Consulta** , clique em **Executar**.  
  
8.  Para salvar a definição do procedimento atualizada, como um script [!INCLUDE[tsql](../../includes/tsql-md.md)] , no menu **Arquivo** , clique em **Salvar como**. Aceite o nome de arquivo ou substitua-o por um nome novo e, então, clique em **Salvar**.  
  
9. Para executar o procedimento armazenado modificado, execute o exemplo a seguir.  
  
    ```  
    EXEC Purchasing.uspVendorAllInfo N'LL Crankarm';  
    GO  
  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-procedure-transact-sql)  
  
  
