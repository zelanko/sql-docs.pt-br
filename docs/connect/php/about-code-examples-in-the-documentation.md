---
title: "Sobre exemplos de código na documentação do | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
caps.latest.revision: "31"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e9218af7938f3d60548a145936ba1645d4db824
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="about-code-examples-in-the-documentation"></a>Sobre exemplos de código na documentação
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Há vários pontos a observar quando você executar os exemplos de código na documentação do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] :  
  
-   Quase todos os exemplos assumem que o SQL Server 2005 ou posterior (SQL Server 2008 ou posterior se você estiver usando a versão 3.1) e o banco de dados AdventureWorks estejam instalados no computador local.  
  
    Para obter informações sobre como baixar as edições gratuitas e as versões de avaliação do SQL Server, consulte [SQL Server](http://go.microsoft.com/fwlink/?LinkID=120193).  
  
    Para obter informações sobre como baixar o banco de dados AdventureWorks, consulte [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=67739).  
  
    Para obter informações sobre como instalar o banco de dados AdventureWorks, consulte [Walkthrough: Installing the AdventureWorks Database](http://go.microsoft.com/fwlink/?LinkID=65819).  
  
-   Quase todos os exemplos de código nesta documentação destinam-se à execução na linha de comando, que permite o teste automatizado de todos os exemplos de código. Para obter informações sobre como executar o PHP na linha de comando, consulte [Using PHP from the command line](http://php.net/manual/en/features.commandline.php).  
  
-   Embora os exemplos tenham sido escritos para execução na linha de comando, todos eles podem ser executados por meio de invocação em um navegador sem fazer nenhuma alteração no script. Para obter a formatação de saída apropriada, substitua cada "\n" por "\<\/br >" em cada exemplo antes de invocá-lo em um navegador.  
  
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
[Visão geral do driver SQL de PHP](../../connect/php/overview-of-the-php-sql-driver.md)
  
