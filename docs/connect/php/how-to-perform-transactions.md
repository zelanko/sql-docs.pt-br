---
title: 'Como: executar transações | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction support
ms.assetid: f4643b85-f929-4919-8951-23394bc5bfa7
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a2a2d041ba99ded7a8d611620ce288593b341a6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38015783"
---
# <a name="how-to-perform-transactions"></a>Como executar transações
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O driver SQLSRV dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] oferece três funções para a execução de transações:  
  
-   [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)  
  
-   [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)  
  
-   [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)  
  
O driver PDO_SQLSRV oferece três métodos para a execução de transações:  
  
-   [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md)  
  
-   [PDO::commit](../../connect/php/pdo-commit.md)  
  
-   [PDO::rollback](../../connect/php/pdo-rollback.md)  
  
Para obter um exemplo, consulte [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) .  
  
O restante deste tópico explica e demonstra como usar o driver SQLSRV para executar transações.  
  
## <a name="remarks"></a>Remarks  
As etapas para executar uma transação podem ser resumidas da seguinte forma:  
  
1.  Inicie a transação com **sqlsrv_begin_transaction**.  
  
2.  Verifique o êxito ou a falha de cada consulta que é parte da transação.  
  
3.  Se adequado, confirme a transação com **sqlsrv_commit**. Caso contrário, reverta a transação com **sqlsrv_rollback**. Depois de chamar **sqlsrv_commit** ou **sqlsrv_rollback**, o driver será retornado para o modo de confirmação automática.  
  
    Por padrão, o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] está no modo de confirmação automática. Isso significa que todas as consultas são confirmadas automaticamente quando obtêm êxito, exceto se foram designadas como parte de uma transação explícita usando **sqlsrv_begin_transaction**.  
  
    Se uma transação explícita não for confirmada com **sqlsrv_commit**, ela será revertida no fechamento da conexão ou no encerramento do script.  
  
    Não use o Transact-SQL inserido para executar transações. Por exemplo, não execute uma instrução com "BEGIN TRANSACTION" como a consulta Transact-SQL para iniciar uma transação. O comportamento transacional esperado não pode ser garantido ao usar o Transact-SQL inserido para executar transações.  
  
    As funções do **sqlsrv** listadas anteriormente devem ser usadas para executar transações.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
O exemplo a seguir executa várias consultas como parte de uma transação. Se todas as consultas forem bem-sucedidas, a transação será confirmada. Se uma das consultas falhar, a transação será revertida.  
  
O exemplo tenta excluir uma ordem de venda da tabela *Sales.SalesOrderDetail* e ajustar os níveis de estoque de produto na tabela *Product.ProductInventory* para cada produto na ordem de venda. Essas consultas estão incluídas em uma transação porque todas as consultas devem ter êxito para que o banco de dados reflita com precisão o estado dos pedidos e a disponibilidade do produto.  
  
A primeira consulta no exemplo recupera identificações e quantidades de produto para uma identificação especificada de ordem de venda. Esta consulta não faz parte da transação. No entanto, o script será encerrado se essa consulta falhar porque as identificações e quantidades de produto são necessárias para concluir consultas que fazem parte da transação subsequente.  
  
As consultas resultantes (exclusão da ordem de venda e atualização das quantidades de estoque do produto) são parte da transação.  
  
O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
### <a name="code"></a>Código  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Begin transaction. */  
if( sqlsrv_begin_transaction($conn) === false )   
{   
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set the Order ID.  */  
$orderId = 43667;  
  
/* Execute operations that are part of the transaction. Commit on  
success, roll back on failure. */  
if (perform_trans_ops($conn, $orderId))  
{  
     //If commit fails, roll back the transaction.  
     if(sqlsrv_commit($conn))  
     {  
         echo "Transaction committed.\n";  
     }  
     else  
     {  
         echo "Commit failed - rolling back.\n";  
         sqlsrv_rollback($conn);  
     }  
}  
else  
{  
     "Error in transaction operation - rolling back.\n";  
     sqlsrv_rollback($conn);  
}  
  
/*Free connection resources*/  
sqlsrv_close( $conn);  
  
/*----------------  FUNCTION: perform_trans_ops  -----------------*/  
function perform_trans_ops($conn, $orderId)  
{  
    /* Define query to update inventory based on sales order info. */  
    $tsql1 = "UPDATE Production.ProductInventory   
              SET Quantity = Quantity + s.OrderQty   
              FROM Production.ProductInventory p   
              JOIN Sales.SalesOrderDetail s   
              ON s.ProductID = p.ProductID   
              WHERE s.SalesOrderID = ?";  
  
    /* Define the parameters array. */  
    $params = array($orderId);  
  
    /* Execute the UPDATE statement. Return false on failure. */  
    if( sqlsrv_query( $conn, $tsql1, $params) === false ) return false;  
  
    /* Delete the sales order. Return false on failure */  
    $tsql2 = "DELETE FROM Sales.SalesOrderDetail   
              WHERE SalesOrderID = ?";  
    if(sqlsrv_query( $conn, $tsql2, $params) === false ) return false;  
  
    /* Return true because all operations were successful. */  
    return true;  
}  
?>  
```  
  
### <a name="comments"></a>Comentários  
Com a finalidade de nos concentrarmos no comportamento da transação, alguns tratamentos de erro recomendados não estão incluídos no exemplo anterior. Para um aplicativo de produção, é recomendável verificar qualquer chamada para um **sqlsrv** de função para erros e tratá-las adequadamente.
  
## <a name="see-also"></a>Consulte Também  
[Atualizando dados &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[Transações (Mecanismo de Banco de Dados)](https://msdn.microsoft.com/library/ms190612.aspx)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
