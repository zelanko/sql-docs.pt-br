---
title: Como carregar Drivers da Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dd99ffa39de48dbf8839cbe06a8bb236fffbdf3
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606196"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Carregando os Drivers da Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página apresenta instruções para carregar os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] no espaço de processo do PHP.  
  
Você pode baixar os drivers predefinidos para sua plataforma do [Drivers da Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) página do projeto Github. Cada pacote de instalação contém arquivos de driver SQLSRV e PDO_SQLSRV na variantes de threads e não-threaded. No Windows, eles também estão disponíveis no variantes de 32 bits e 64 bits. Ver [requisitos do sistema para o Microsoft Drivers for PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md) para obter uma lista dos arquivos de driver que estão contidos em cada pacote. O arquivo de driver deve corresponder a versão do PHP, arquitetura e threadedness do seu ambiente do PHP.

No Linux e macOS, os drivers podem Alternativamente ser instalados usando PECL, como encontrado na [tutorial de instalação](../../connect/php/installation-tutorial-linux-mac.md).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Movendo o arquivo de driver para o diretório de extensões  
O arquivo de driver deve estar localizado em um diretório em que o tempo de execução do PHP pode encontrá-lo. É mais fácil de colocar o arquivo de driver no seu diretório de extensão do PHP padrão, para localizar o diretório padrão, execute `php -i | sls extension_dir` no Windows ou `php -i | grep extension_dir` no Linux/macOS. Se você não estiver usando o diretório de extensão padrão, especifique um diretório no arquivo de configuração do PHP (PHP. ini), usando o **extension_dir** opção. Por exemplo, no Windows, se você colocou o arquivo de driver no seu `c:\php\ext` diretório, adicione a seguinte linha ao PHP. ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Carregando o driver na inicialização do PHP  
Para carregar o driver SQLSRV quando o PHP é iniciado, coloque antes o arquivo do driver no diretório de extensões. Então, siga estas etapas:  
  
1.  Para habilitar o **SQLSRV** driver, modifique **PHP. ini** adicionando a seguinte linha à seção de extensões, alterando o nome do arquivo conforme apropriado:  
  
    No Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    No Linux, se você tiver baixado os binários pré-criados para a sua distribuição: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Se você tiver compilado o SQLSRV binário do código-fonte ou com PECL, ele será em vez disso, nomeado sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  Para habilitar o **PDO_SQLSRV** driver, a extensão de objetos de dados do PHP (PDO) deve estar disponível como uma extensão interna ou como uma extensão carregada dinamicamente.

    No Windows, os binários pré-criados do PHP vêm com PDO interno, portanto, não há necessidade de modificar o PHP. ini para carregá-lo. Se, no entanto, você tiver compilado PHP no código-fonte e especificou uma extensão PDO separada a ser criado, ele será denominado `php_pdo.dll`, você deve copiá-lo para seu diretório de extensão e adicione a seguinte linha ao PHP. ini:  
    ```
    extension=php_pdo.dll  
    ```
    No Linux, se você tiver instalado o PHP, usando o Gerenciador de pacotes do seu sistema, PDO provavelmente é instalado como uma extensão carregada dinamicamente chamada pdo.so. A extensão PDO deve ser carregada antes da extensão do PDO_SQLSRV ou carregamento falhará. Extensões geralmente são carregadas usando arquivos. ini individuais, e esses arquivos são lidos após PHP. ini. Portanto, se pdo.so é carregada por meio de seu próprio arquivo. ini, é necessário que um arquivo separado, carregando o driver PDO_SQLSRV após PDO. 

    Para descobrir qual diretório de arquivos. ini de extensão específicos estão localizados, execute `php --ini` e observe a pasta listada em `Scan for additional .ini files in:`. Localize o arquivo que carrega pdo.so – provavelmente, ele será prefixado por um número, como 10 pdo.ini. O prefixo numérico indica a ordem de carregamento de arquivos. ini, enquanto os arquivos que não têm um prefixo numérico são carregados em ordem alfabética. Crie um arquivo para carregar o arquivo do driver PDO_SQLSRV chamado 30-pdo_sqlsrv.ini (qualquer número maior do que aquele que prefixos pdo.ini funciona) ou pdo_sqlsrv.ini (se pdo.ini não está prefixado por um número) e adicione a seguinte linha a ele, alterando o nome do arquivo como apropriadas:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Como com SQLSRV, se você tiver compilado o PDO_SQLSRV binário do código-fonte ou com PECL, ele será em vez disso, ser denominado pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    Copie esse arquivo para o diretório que contém os outros arquivos. ini. 

    Se você tiver compilado o PHP de origem com suporte PDO interno, você não exige um arquivo. ini separado e você pode adicionar a linha apropriada acima em PHP. ini.
  
3.  Reinicie o servidor Web.  
  
> [!NOTE]  
> Para determinar se o driver foi carregado com êxito, execute um script que chama [phpinfo()](https://php.net/manual/en/function.phpinfo.php).  
  
Para obter mais informações sobre as diretivas do **php.ini**, veja [Descrição das principais diretivas do php.ini](https://php.net/manual/en/ini.core.php).  
  
## <a name="see-also"></a>Consulte Também  
[Guia de Introdução com os Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Requisitos do sistema para os Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Guia de programação para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referência da API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
