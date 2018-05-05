---
title: Carregando os Drivers da Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7890c38877d05a69118a7c61ffe7261d1c9e91e2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Carregando os Drivers da Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página fornece instruções para carregar o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] no processo do PHP espaço.  
  
Você pode baixar os drivers pré-criados para sua plataforma do [Drivers da Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) página do Github do projeto. Cada pacote de instalação contém arquivos de driver SQLSRV e PDO_SQLSRV em variants threads e não-threaded. No Windows, eles também estão disponíveis em variantes de 32 bits e 64 bits. Consulte [requisitos de sistema para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md) para obter uma lista dos arquivos de driver que estão contidos em cada pacote. O arquivo de driver deve corresponder a versão do PHP, arquitetura e threadedness do seu ambiente do PHP.

No Linux e macOS, os drivers podem opcionalmente ser instalados usando PECL, como encontrado na [tutorial de instalação](../../connect/php/installation-tutorial-linux-mac.md).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Movendo o arquivo de driver para o diretório de extensões  
O arquivo de driver deve estar localizado em um diretório em que o tempo de execução do PHP pode encontrá-lo. É mais fácil de colocar o arquivo de driver no diretório de extensões do PHP padrão - para localizar o diretório padrão, execute `php -i | sls extension_dir` no Windows ou `php -i | grep extension_dir` no Linux/macOS. Se você não estiver usando o diretório de extensão padrão, especifique um diretório no arquivo de configuração do PHP (php.ini) usando o **extension_dir** opção. Por exemplo, no Windows, se você colocou o arquivo de driver seu `c:\php\ext` diretório, adicione a seguinte linha ao php.ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Carregando o driver na inicialização do PHP  
Para carregar o driver SQLSRV quando o PHP é iniciado, mova um arquivo de driver no diretório de extensões. Então, siga estas etapas:  
  
1.  Para habilitar o **SQLSRV** driver, modificar **php.ini** adicionando a seguinte linha à seção de extensões, alterando o nome do arquivo como apropriado:  
  
    No Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    No Linux, se você tiver baixado os binários predefinidos para a sua distribuição: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Se você tiver compilado o SQLSRV binário de origem ou com PECL, ele será em vez disso, nomeado sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  Para habilitar o **PDO_SQLSRV** driver, a extensão de objetos de dados do PHP (PDO) deve estar disponível, como uma extensão interna ou como uma extensão carregada dinamicamente.

    No Windows, os binários do PHP pré-compilada vêm com PDO interna, portanto, não há necessidade de modificar ini para carregá-lo. Se, no entanto, você ter compilado PHP da fonte especificado uma extensão PDO separada a ser criado, ele será nomeado `php_pdo.dll`, você deve copiá-lo para o diretório de extensões e adicione a seguinte linha ao php.ini:  
    ```
    extension=php_pdo.dll  
    ```
    No Linux, se você tiver instalado o PHP usando o Gerenciador de pacote do sistema, o PDO provavelmente é instalado como uma extensão carregada dinamicamente denominada pdo.so. A extensão PDO deve ser carregada antes da extensão do PDO_SQLSRV ou carregamento falhará. Extensões geralmente são carregadas usando arquivos. ini individuais, e esses arquivos são lidos após php.ini. Portanto, se pdo.so é carregado por meio de seu próprio arquivo. ini, um arquivo separado, carregando o driver PDO_SQLSRV após PDO é necessário. 

    Para descobrir qual diretório estão localizados os arquivos. ini de extensão específica, execute `php --ini` e anote a pasta listada em `Scan for additional .ini files in:`. Localizar o arquivo que carrega pdo.so - ele provavelmente é prefixado por um número, como 10 pdo.ini. O prefixo numérico indica a ordem de carregamento de arquivos. ini, enquanto os arquivos que não têm um prefixo numérico são carregados em ordem alfabética. Crie um arquivo para carregar o arquivo do driver PDO_SQLSRV chamado 30-pdo_sqlsrv.ini (qualquer número maior do que aquele que prefixos pdo.ini funciona) ou pdo_sqlsrv.ini (se pdo.ini não é prefixado por um número) e adicione a seguinte linha, alterando o nome do arquivo como apropriadas:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Como com SQLSRV, se você tiver compilado o binário PDO_SQLSRV da fonte ou com PECL, ele será em vez disso, nomeado pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    Copie esse arquivo para o diretório que contém outros arquivos. ini. 

    Se você tiver compilado PHP de origem com suporte PDO interno, você não precisa de um arquivo. ini separado e você pode adicionar a linha apropriada acima para php.ini.
  
3.  Reinicie o servidor Web.  
  
> [!NOTE]  
> Para determinar se o driver foi carregado com êxito, execute um script que chama [phpinfo ()](http://php.net/manual/en/function.phpinfo.php).  
  
Para obter mais informações sobre **php.ini** diretivas, consulte [descrição das principais diretivas do php.ini](http://php.net/manual/en/ini.core.php).  
  
## <a name="see-also"></a>Consulte também  
[Guia de Introdução com os Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Requisitos de sistema para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Programação de guia para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referência de API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
