---
title: Sobre exemplos de código na documentação
description: Há vários pontos a observar ao executar os exemplos de código na documentação do Microsoft Drivers for PHP for SQL Server.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c90f2f1a420f1ab40f99a2fe83c928890e37e621
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81631886"
---
# <a name="about-code-examples-in-the-documentation"></a>Sobre exemplos de código na documentação
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>Comentários sobre os exemplos de código
Há vários pontos a observar quando você executar os exemplos de código na documentação do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] :  
  
-   Quase todos os exemplos assumem que o SQL Server 2008 ou posterior e o banco de dados AdventureWorks estejam instalados no computador local.  
  
    Para obter informações sobre como baixar as edições gratuitas e as versões de avaliação do SQL Server, consulte [SQL Server](https://go.microsoft.com/fwlink/?LinkID=120193).  
  
    Para obter informações sobre como baixar e instalar o banco de dados AdventureWorks, confira a [página do AdventureWorks no repositório do GitHub de exemplos do SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works).
  
-   Quase todos os exemplos de código nesta documentação destinam-se à execução na linha de comando, que permite o teste automatizado de todos os exemplos de código. Para obter informações sobre como executar o PHP na linha de comando, consulte [Using PHP from the command line](https://php.net/manual/en/features.commandline.php).  
  
-   Embora os exemplos sejam criados para execução na linha de comando, todos eles podem ser executados por meio de invocação em um navegador sem fazer nenhuma alteração no script. Para obter uma formatação de saída apropriada, substitua cada "\n" por "\<\/br>" em cada exemplo antes de invocá-lo em um navegador.  
  
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
  
    Para obter mais informações sobre tratamento de erros e avisos, consulte [Handling Errors and Warnings](handling-errors-and-warnings.md).  
  
## <a name="see-also"></a>Consulte Também  
[Visão geral dos Microsoft Drivers for PHP for SQL Server](overview-of-the-php-sql-driver.md)
  
