---
title: Carregando o Driver SQL de PHP | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cb2200b2c5d151981e9dcdf8322dd7c43b91c6ee
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="loading-the-php-sql-driver"></a>Carregando o driver SQL do PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico oferece instruções para carregar os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] no espaço de processo do PHP.  
  
Há duas opções para carregar um driver. O driver pode ser carregado quando o PHP é iniciado ou no tempo de execução do script PHP.  
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Movendo o arquivo de driver para o diretório de extensões  
Independentemente do procedimento usado, a primeira etapa é colocar o arquivo de driver em um diretório onde possa ser encontrado pelo tempo de execução do PHP. Portanto, coloque o arquivo de driver no diretório de extensões do PHP. Consulte [Requisitos de sistema para o driver SQL do PHP](../../connect/php/system-requirements-for-the-php-sql-driver.md) para obter uma lista dos arquivos do driver que são instalados com os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
Se necessário, especifique o local do diretório do arquivo do driver no arquivo de configuração do PHP (php.ini) usando o **extension_dir** opção. Por exemplo, se você colocar o arquivo do driver no diretório c:\php\ext, use esta opção:  
  
```  
extension_dir = "c:\PHP\ext"  
```  
  
## <a name="loading-the-driver-at-php-startup"></a>Carregando o driver na inicialização do PHP  
Para carregar os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] quando o PHP é iniciado, coloque antes o arquivo do driver no diretório de extensões. Então, siga estas etapas:  
  
1.  Para habilitar o **SQLSRV** driver, modificar **php.ini** , adicionando a seguinte linha à seção de extensões ou modificando a linha que já está lá:  
  
    No Windows (Este exemplo usa a versão 4.0 thread seguro do driver para PHP 7): 
    ```  
    extension=php_sqlsrv_7_ts.dll  
    ```  
    No Linux (Este exemplo usa a versão como instalado pelo PECL): 
    ```  
    extension=sqlsrv.so  
    ```  
    Para habilitar o **PDO_SQLSRV** driver, modificar **php.ini** , adicionando a seguinte linha à seção de extensões ou modificando a linha que já está lá:  
  
    No Windows (Este exemplo usa a versão 4.0 thread seguro do driver para PHP 7):
    ```  
    extension=php_pdo_sqlsrv_7_ts.dll  
    ```  
    No Linux (Este exemplo usa a versão como instalado pelo PECL):
    ```  
    extension=pdo_sqlsrv.so  
    ```  
  
2.  Se você quiser usar o **PDO_SQLSRV** driver, a extensão de objetos de dados do PHP (PDO) deve estar disponível, como uma extensão interna ou como uma extensão carregada dinamicamente. Se você precisar carregar o driver PDO_SQLSRV dinamicamente, a php_pdo.dll (ou pdo.so no Linux) deve estar presente no diretório de extensões e a linha a seguir deve estar no php.ini:

    No Windows:  
    ```
    extension=php_pdo.dll  
    ```  
    No Linux:  
    ```
    extension=pdo.so  
    ```  
  
3.  Reinicie o servidor Web.  
  
> [!NOTE]  
> Para determinar se o driver foi carregado com êxito, execute um script que chama [phpinfo ()](http://go.microsoft.com/fwlink/?LinkId=108678).  
  
Para obter mais informações sobre as diretivas do **php.ini** , consulte [Descrição das principais diretivas do php.ini](http://go.microsoft.com/fwlink/?LinkId=105817).  
  
## <a name="loading-the-driver-at-php-script-runtime"></a>Carregando o driver no tempo de execução do script PHP  
Para carregar os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] no tempo de execução do script, coloque antes o arquivo do driver no diretório de extensões. Em seguida, inclua a seguinte linha no início do script PHP que coincide com o nome do arquivo do driver:  
  
```  
dl('php_pdo_sqlsrv_7_ts.dll');  
```  
  
Para obter mais informações sobre funções PHP relacionadas ao carregamento dinâmico de extensões, consulte [dl](http://go.microsoft.com/fwlink/?LinkId=105818) e [extension_loaded.](http://go.microsoft.com/fwlink/?LinkId=105819)  
  
## <a name="see-also"></a>Consulte também  
[Introdução ao driver SQL de PHP](../../connect/php/getting-started-with-the-php-sql-driver.md)
[Requisitos de sistema para o driver SQL do PHP](../../connect/php/system-requirements-for-the-php-sql-driver.md)
[Guia de programação para o driver SQL de PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  

