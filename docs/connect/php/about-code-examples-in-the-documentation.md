---
title: Sobre exemplos de código na documentação | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1520106fa39e850bf09d78a5eeee955fba1260fb
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606736"
---
# <a name="about-code-examples-in-the-documentation"></a>Sobre exemplos de código na documentação
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>Comentários sobre os exemplos de código
Há vários pontos a observar quando você executar os exemplos de código na documentação do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] :  
  
-   Quase todos os exemplos pressupõem que o SQL Server 2008 ou posterior e o banco de dados AdventureWorks estejam instalados no computador local.  
  
    Para obter informações sobre como baixar as edições gratuitas e as versões de avaliação do SQL Server, consulte [SQL Server](https://go.microsoft.com/fwlink/?LinkID=120193).  
  
    Para obter informações sobre como baixar e instalar o banco de dados AdventureWorks, consulte a [página do AdventureWorks no repositório Github de exemplos do SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works).
  
-   Quase todos os exemplos de código nesta documentação destinam-se à execução na linha de comando, que permite o teste automatizado de todos os exemplos de código. Para obter informações sobre como executar o PHP na linha de comando, consulte [Using PHP from the command line](https://php.net/manual/en/features.commandline.php).  
  
-   Embora os exemplos sejam criados para execução na linha de comando, todos eles podem ser executados por meio de invocação em um navegador sem fazer nenhuma alteração no script. Para formatar a saída perfeitamente, substitua cada "\n" por "\<\/br >" em cada exemplo antes de invocá-lo em um navegador.  
  
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
  
## <a name="see-also"></a>Consulte Também  
[Visão geral dos Microsoft Drivers for PHP for SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
  
