---
title: Como carregar Drivers da Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
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
ms.openlocfilehash: e3c6614425cf8796bd7ec462a62f9410b9ca5857
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936387"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Carregando os Drivers da Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página apresenta instruções para carregar os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] no espaço de processo do PHP.  
  
Você pode baixar os drivers pré-criados para sua plataforma na página de projeto [drivers da Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) github. Cada pacote de instalação contém arquivos de driver SQLSRV e PDO_SQLSRV em variantes threaded e não threaded. No Windows, eles também estão disponíveis em variantes de 32 bits e 64 bits. Consulte [requisitos de sistema para os drivers da Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md) para obter uma lista dos arquivos de driver contidos em cada pacote. O arquivo de driver deve corresponder à versão do PHP, à arquitetura e ao threadedness do seu ambiente PHP.

No Linux e no macOS, os drivers podem ser instalados como alternativa usando o PECL, conforme encontrado no [tutorial de instalação](../../connect/php/installation-tutorial-linux-mac.md).

Você também pode criar os drivers da origem ao compilar PHP ou usando `phpize`. Se você optar por criar os drivers da origem, terá a opção de criá-los estaticamente no php em vez de criá-los como extensões compartilhadas adicionando `--enable-sqlsrv=static --with-pdo_sqlsrv=static` (no Linux e MacOS) ou `--enable-sqlsrv=static --with-pdo-sqlsrv=static` ( `./configure` no Windows) ao comando quando Compilando PHP. Para obter mais informações sobre o sistema de compilação `phpize`do PHP e, consulte a [documentação do PHP](http://php.net/manual/install.php).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Movendo o arquivo de driver para o diretório de extensões  
O arquivo de driver deve estar localizado em um diretório onde o tempo de execução do PHP possa encontrá-lo. É mais fácil colocar o arquivo de driver em seu diretório de extensão PHP padrão-para localizar o diretório padrão, execute `php -i | sls extension_dir` no Windows ou `php -i | grep extension_dir` no linux/MacOS. Se você não estiver usando o diretório de extensão padrão, especifique um diretório no arquivo de configuração do PHP (PHP. ini), usando a opção **extension_dir** . Por exemplo, no Windows, se você colocou o arquivo de driver em seu `c:\php\ext` diretório, adicione a seguinte linha a php. ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Carregando o driver na inicialização do PHP  
Para carregar o driver SQLSRV quando o PHP é iniciado, coloque antes o arquivo do driver no diretório de extensões. Então, siga estas etapas:  
  
1.  Para habilitar o driver **sqlsrv** , modifique **php. ini** adicionando a seguinte linha à seção extensão, alterando o nome de arquivo conforme apropriado:  
  
    No Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    No Linux, se você tiver baixado os binários predefinidos para sua distribuição: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Se você tiver compilado o binário SQLSRV a partir da origem ou com PECL, ele será nomeado sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  Para habilitar o driver **PDO_SQLSRV** , a extensão PDO (objetos de dados php) deve estar disponível, seja como uma extensão interna ou como uma extensão carregada dinamicamente.

    No Windows, os binários do PHP pré-criados vêm com PDO interno, portanto, não há necessidade de modificar o php. ini para carregá-lo. Se, no entanto, você tiver compilado o php da origem e especificado uma extensão PDO separada para ser compilado, ele `php_pdo.dll`será nomeado e você deverá copiá-lo para o diretório de extensão e adicionar a seguinte linha a php. ini:  
    ```
    extension=php_pdo.dll  
    ```
    No Linux, se você tiver instalado o PHP usando o Gerenciador de pacotes do sistema, o PDO provavelmente será instalado como uma extensão carregada dinamicamente chamada pdo.so. A extensão PDO deve ser carregada antes da extensão PDO_SQLSRV ou o carregamento falhará. Normalmente, as extensões são carregadas usando arquivos. ini individuais, e esses arquivos são lidos após php. ini. Portanto, se pdo.so for carregado por meio de seu próprio arquivo. ini, um arquivo separado carregando o driver PDO_SQLSRV após PDO é necessário. 

    Para descobrir em qual diretório os arquivos. ini específicos da extensão estão localizados, execute `php --ini` e observe o diretório listado em `Scan for additional .ini files in:`. Localize o arquivo que carrega pdo.so--provavelmente é prefixado por um número, como 10-PDO. ini. O prefixo numérico indica a ordem de carregamento dos arquivos. ini, enquanto os arquivos que não têm um prefixo numérico são carregados alfabeticamente. Crie um arquivo para carregar o arquivo de driver PDO_SQLSRV chamado 30-pdo_sqlsrv. ini (qualquer número maior do que o prefixo PDO. ini funciona) ou PDO_SQLSRV. ini (se PDO. ini não for prefixado por um número) e adicione a seguinte linha a ele, alterando o nome do arquivo como desejado  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Assim como acontece com o SQLSRV, se você tiver compilado o binário PDO_SQLSRV a partir de source ou com PECL, ele será nomeado PDO_SQLSRV. portanto:
    ```
    extension=pdo_sqlsrv.so
    ```
    Copie esse arquivo para o diretório que contém os outros arquivos. ini. 

    Se você tiver compilado o PHP da origem com suporte de PDO interno, você não precisará de um arquivo. ini separado e poderá adicionar a linha apropriada acima ao PHP. ini.
  
3.  Reinicie o servidor Web.  
  
> [!NOTE]  
> Para determinar se o driver foi carregado com êxito, execute um script que chama [phpinfo()](https://php.net/manual/en/function.phpinfo.php).  
  
Para obter mais informações sobre as diretivas do **php.ini**, veja [Descrição das principais diretivas do php.ini](https://php.net/manual/en/ini.core.php).  
  
## <a name="see-also"></a>Consulte Também  
[Introdução aos Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Requisitos do sistema para os Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Guia de programação para o Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referência da API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
