---
title: 'Etapa 4: Conectar atenda com flexibilidade ao SQL com PHP | Microsoft Docs'
ms.custom: 
ms.date: 01/22/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8013474f-48e9-43d5-ab89-7b0504044468
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f3b9f6615c5adc6a1ec838e690cee8c55b32843
ms.sourcegitcommit: d7dcbcebbf416298f838a39dd5de6a46ca9f77aa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="step-4-connect-resiliently-to-sql-with-php"></a>Etapa 4: Conectar-se de forma resiliente ao SQL com PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  
O programa de demonstração foi projetado para que um erro transitório (isto é qualquer código de erro com o prefixo '08' conforme listado neste [apêndice](https://docs.microsoft.com/en-us/sql/odbc/reference/appendixes/appendix-a-odbc-error-codes)) durante a tentativa de conexão de clientes potenciais para uma nova tentativa. Mas um erro temporário durante o comando de consulta faz com que o programa descarte a conexão e crie uma nova conexão, antes de tentar novamente o comando de consulta. Não recomendamos ou Desaconselhamos essa opção de design. O programa de demonstração ilustra alguns da flexibilidade de design que está disponível para você.  
  
O comprimento deste exemplo de código se deve principalmente à lógica de exceção de captura.   
  
O [sqlsrv_query()](../../connect/php/sqlsrv-query.md) função pode ser usada para recuperar um conjunto de resultados de uma consulta no banco de dados SQL. Essencialmente, essa função aceita qualquer objeto de conexão e consulta e retorna um conjunto de resultados, que pode ser iterado com o uso de [sqlsrv_fetch_array()](../../connect/php/sqlsrv-fetch-array.md). 
  
```php

    <?php  
        // Variables to tune the retry logic.    
        $connectionTimeoutSeconds = 30;  // Default of 15 seconds is too short over the Internet, sometimes.  
        $maxCountTriesConnectAndQuery = 3;  // You can adjust the various retry count values.  
        $secondsBetweenRetries = 4;  // Simple retry strategy.  
        $errNo = 0;  
        $serverName = "tcp:yourdatabase.database.windows.net,1433";  
        $connectionOptions = array("Database"=>"AdventureWorks",  
           "Uid"=>"yourusername", "PWD"=>"yourpassword", "LoginTimeout" => $connectionTimeoutSeconds);  
        $conn = null;  
        $arrayOfTransientErrors = array('08001', '08002', '08003', '08004', '08007', '08S01'); 
        for ($cc = 1; $cc <= $maxCountTriesConnectAndQuery; $cc++) {  
            // [A.2] Connect, which proceeds to issue a query command.  
            $conn = sqlsrv_connect($serverName, $connectionOptions);    
            if ($conn === true) {  
                echo "Connection was established";  
                echo "<br>";  
  
                $tsql = "SELECT Name FROM Production.ProductCategory";  
                $stmt = sqlsrv_query($conn, $tsql);  
                if ($stmt === false) {
                    echo "Error in query execution";  
                    echo "<br>";  
                    die(print_r(sqlsrv_errors(), true));  
                }
                while($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {     
                    echo $row['Name'] . "<br/>" ;
                }  
                sqlsrv_free_stmt($stmt);  
                sqlsrv_close( $conn); 
                break;  
            } else {    
                // [A.4] Check whether the error code is on the whitelist of transients.  
                $isTransientError = false;  
                $errorCode = '';
                if (($errors = sqlsrv_errors()) != null) {
                    foreach ($errors as $error) {  
                        $errorCode = $error['code'];
                        $isTransientError = in_array($errorCode, $arrayOfTransientErrors);
                        if ($isTransientError) {
                            break;
                        }
                    }
                }  
                if (!$isTransientError) { 
                    // it is a static persistent error...
                    echo("Persistent error suffered with error code = $errorCode. Program will terminate.");  
                    echo "<br>";  
                    // [A.5] Either the connection attempt or the query command attempt suffered a persistent error condition.  
                    // Break the loop, let the hopeless program end.  
                    exit(0);  
                }  
                // [A.6] It is a transient error from an attempt to issue a query command.  
                // So let this method reloop and try again. However, we recommend that the new query  
                // attempt should start at the beginning and establish a new connection.  
                if ($cc >= $maxCountTriesConnectAndQuery) {  
                    echo "Transient errors suffered in too many retries - $cc. Program will terminate.";  
                    echo "<br>";  
                    exit(0);  
                }  
                echo("Transient error encountered with error code = $errorCode. Program might retry by itself.");    
                echo "<br>";  
                echo "$cc attempts so far. Might retry.";  
                echo "<br>";  
                // A very simple retry strategy, a brief pause before looping.  
                sleep(1*$secondsBetweenRetries);  
            }  
            // [A.3] All has gone well, so let the program end.  
        }  
    ?>
```
