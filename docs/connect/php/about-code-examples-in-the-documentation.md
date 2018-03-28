---
title: Sobre exemplos de código na documentação do | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
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
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a5515db3c5b98ddb0c3645016eade20ecf4f224b
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="about-code-examples-in-the-documentation"></a>Sobre exemplos de código na documentação
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>Comentários sobre os exemplos de código
Há vários pontos a observar quando você executar os exemplos de código na documentação do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] :  
  
-   Quase todos os exemplos assumem que SQL Server 2008 ou posterior e o banco de dados AdventureWorks estejam instalados no computador local.  
  
    Para obter informações sobre como baixar as edições gratuitas e as versões de avaliação do SQL Server, consulte [SQL Server](http://go.microsoft.com/fwlink/?LinkID=120193).  
  
    Para obter informações sobre como baixar e instalar o banco de dados AdventureWorks, consulte o [página AdventureWorks no repositório do Github de exemplos do SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works).
  
-   Quase todos os exemplos de código nesta documentação destinam-se à execução na linha de comando, que permite o teste automatizado de todos os exemplos de código. Para obter informações sobre como executar o PHP na linha de comando, consulte [Using PHP from the command line](http://php.net/manual/en/features.commandline.php).  
  
-   Embora exemplos destinam-se para ser executado a partir da linha de comando, cada exemplo pode ser executado por meio de invocação de um navegador sem fazer qualquer alteração no script. Para formatar a saída satisfatoriamente, substitua cada "\n" por "\<\/br >" em cada exemplo antes de invocá-lo em um navegador.  
  
-   Com a finalidade de manter cada exemplo com um foco restrito, o tratamento de erros correto não é feito em todos os exemplos. É recomendável que qualquer chamada para uma função **sqlsrv** ou um método PDO passe por verificação de erros e seja tratada de acordo com as necessidades do aplicativo.  
  
    Uma maneira fácil de obter informações de erro quando um erro é encontrado é sair do script com a seguinte linha de código:  
  
    ```  
    die( print_r( sqlsrv_errors(), true));  
    ```  
  
    Ou, se você estiver usando o PDO,  
  
    ```  
    print_r ($stmt->errorInfo());  
    die();  
    ```  
  
    Para obter mais informações sobre tratamento de erros e avisos, consulte [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).  
  
## <a name="see-also"></a>Consulte também  
[Visão geral dos Drivers da Microsoft para PHP para SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
  
