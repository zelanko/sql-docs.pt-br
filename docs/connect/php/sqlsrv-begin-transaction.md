---
title: sqlsrv_begin_transaction | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_begin_transaction
apitype: NA
helpviewer_keywords:
- sqlsrv_begin_transaction
- transaction support
- API Reference, sqlsrv_begin_transaction
ms.assetid: 0b223bc8-4047-4329-9cbf-d350ab0fb886
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c83c62cf6a9ec637573682cc3b0193b173875a42
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35309195"
---
# <a name="sqlsrvbegintransaction"></a>sqlsrv_begin_transaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Inicia uma transação em uma conexão especificada. A transação atual inclui todas as instruções na conexão especificada que foram executadas após a chamada para **sqlsrv_begin_transaction** e antes de qualquer chamada para [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md) ou [sqlsrv_commit](../../connect/php/sqlsrv-commit.md).  
  
> [!NOTE]  
> O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] está no modo de confirmação automática por padrão. Isso significa que todas as consultas são confirmadas automaticamente quando obtêm êxito, exceto se foram designadas como parte de uma transação explícita usando **sqlsrv_begin_transaction**.  
  
> [!NOTE]  
> Se **sqlsrv_begin_transaction** for chamado após uma transação já ter sido iniciada na conexão, mas ainda não houver sido concluída chamando **sqlsrv_commit** ou **sqlsrv_rollback**, a chamada retornará **false** e um erro *Já em Transação* será adicionado à coleção de erros.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_begin_transaction( resource $conn)  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$conn*: a conexão com a qual a transação está associada.  
  
## <a name="return-value"></a>Valor retornado  
Um valor booliano: **true** se a transação foi iniciada com êxito. Caso contrário, **false**.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir executa duas consultas como parte de uma transação. Se ambas as consultas forem bem-sucedidas, a transação será confirmada. Se uma das consultas falhar (ou ambas), a transação será revertida.  
  
A primeira consulta no exemplo insere uma nova ordem de venda na tabela *Sales.SalesOrderDetail* do banco de dados AdventureWorks. A ordem é de cinco unidades do produto com a identificação 709. A segunda consulta reduz a quantidade de estoque do produto com a identificação do produto 709 em cinco unidades. Essas consultas estão incluídas em uma transação porque ambas devem ter êxito para que o banco de dados reflita com precisão o estado dos pedidos e a disponibilidade do produto.  
  
O exemplo supõe que SQL Server e o [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) banco de dados são instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initiate transaction. */  
/* Exit script if transaction cannot be initiated. */  
if ( sqlsrv_begin_transaction( $conn ) === false )  
{  
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true ));  
}  
  
/* Initialize parameter values. */  
$orderId = 43659; $qty = 5; $productId = 709;  
$offerId = 1; $price = 5.70;  
  
/* Set up and execute the first query. */  
$tsql1 = "INSERT INTO Sales.SalesOrderDetail   
                     (SalesOrderID,   
                      OrderQty,   
                      ProductID,   
                      SpecialOfferID,   
                      UnitPrice)  
          VALUES (?, ?, ?, ?, ?)";  
$params1 = array( $orderId, $qty, $productId, $offerId, $price);  
$stmt1 = sqlsrv_query( $conn, $tsql1, $params1 );  
  
/* Set up and execute the second query. */  
$tsql2 = "UPDATE Production.ProductInventory   
          SET Quantity = (Quantity - ?)   
          WHERE ProductID = ?";  
$params2 = array($qty, $productId);  
$stmt2 = sqlsrv_query( $conn, $tsql2, $params2 );  
  
/* If both queries were successful, commit the transaction. */  
/* Otherwise, rollback the transaction. */  
if( $stmt1 && $stmt2 )  
{  
     sqlsrv_commit( $conn );  
     echo "Transaction was committed.\n";  
}  
else  
{  
     sqlsrv_rollback( $conn );  
     echo "Transaction was rolled back.\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt1);  
sqlsrv_free_stmt( $stmt2);  
sqlsrv_close( $conn);  
?>  
```  
  
Com a finalidade de nos concentrarmos no comportamento da transação, alguns tratamentos de erro recomendados não estão incluídos no exemplo acima. Para um aplicativo de produção, recomenda-se que todas as chamadas para a função **sqlsrv** contenham verificação e tratamento de erros.  
  
> [!NOTE]  
> Não use o Transact-SQL inserido para executar transações. Por exemplo, não execute uma instrução com "BEGIN TRANSACTION" como a consulta Transact-SQL para iniciar uma transação. O comportamento transacional esperado não pode ser garantido ao usar o Transact-SQL inserido para executar transações.  
  
## <a name="see-also"></a>Consulte também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Como executar transações](../../connect/php/how-to-perform-transactions.md)

[Visão geral dos Drivers da Microsoft para PHP para SQL Server](../../connect/php/overview-of-the-php-sql-driver.md) 
  
