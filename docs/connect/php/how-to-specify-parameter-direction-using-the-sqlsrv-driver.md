---
title: 'Como: especificar a direção de parâmetro usando o Driver SQLSRV | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b4004fa498c01e73c99204bb0d36ac4bded66a9b
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>Como especificar a direção do parâmetro com o driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico descreve como usar o driver SQLSRV para especificar a direção do parâmetro ao chamar um procedimento armazenado. A direção do parâmetro é especificado quando você cria uma matriz de parâmetros (etapa 3) que é passada para [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
### <a name="to-specify-parameter-direction"></a>Para especificar a direção do parâmetro  
  
1.  Defina uma consulta Transact-SQL que chame um procedimento armazenado. Use pontos de interrogação (?) em vez dos parâmetros a serem passados ao procedimento armazenado. Por exemplo, essa cadeia de caracteres chama um procedimento armazenado (UpdateVacationHours) que aceita dois parâmetros:  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > Chamar os procedimentos armazenados usando a sintaxe canônica é a prática recomendada. Para obter mais informações sobre a sintaxe canônica, consulte [chamando um procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md).  
  
2.  Inicialize ou atualize as variáveis do PHP correspondentes aos espaços reservados na consulta Transact-SQL. Por exemplo, o código a seguir inicializa os dois parâmetros para o procedimento armazenado UpdateVacationHours:  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    > Variáveis que são inicializadas ou atualizadas para **null**, **DateTime**ou tipos de fluxo não podem ser usadas como parâmetros de saída.  
  
3.  Use suas variáveis PHP da etapa 2 para criar ou atualizar uma matriz de valores de parâmetros que correspondam, em sequência, aos espaços reservados do parâmetro na cadeia de caracteres Transact-SQL. Especifique a direção de cada parâmetro na matriz. A direção de cada parâmetro é determinada em uma das duas maneiras: por padrão (para parâmetros de entrada) ou usando **SQLSRV_PARAM _\***  constantes (para parâmetros de saída e bidirecional). Por exemplo, o código a seguir especifica o parâmetro *$employeeId* como um parâmetro de entrada e o parâmetro *$usedVacationHours* como um parâmetro bidirecional:  
  
    ```  
    $params = array(  
                     array($employeeId, SQLSRV_PARAM_IN),  
                     array($usedVacationHours, SQLSRV_PARAM_INOUT)  
                    );  
    ```  
  
    Para entender a sintaxe para especificar a direção do parâmetro em geral, suponha que *$var1*, *$var2*e *$var3* correspondam aos parâmetros de entrada, saída e bidirecional, respectivamente. Você pode especificar a direção do parâmetro das seguintes maneiras:  
  
    -   Especificar implicitamente o parâmetro de entrada, especificar explicitamente o parâmetro de saída e especificar explicitamente um parâmetro bidirecional:  
  
        ```  
        array(   
               array($var1),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
    -   Especificar explicitamente o parâmetro de entrada, especificar explicitamente o parâmetro de saída e especificar explicitamente um parâmetro bidirecional:  
  
        ```  
        array(   
               array($var1, SQLSRV_PARAM_IN),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
4.  Execute a consulta com [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou com [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) e [sqlsrv_execute](../../connect/php/sqlsrv-execute.md). Por exemplo, o código a seguir usa a conexão *$conn* para executar a consulta *$tsql* com valores de parâmetros especificados em *$params*:  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>Consulte também  
[Como recuperar parâmetros de saída usando o driver SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
