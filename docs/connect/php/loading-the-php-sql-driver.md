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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ce26b4800250cab25a6db6f5b3ed7ebf0b1d9bd
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922866"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Carregando os Drivers da Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página apresenta instruções para carregar os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] no espaço de processo do PHP.  
  
Você pode baixar os drivers predefinidos para sua plataforma da página do projeto GitHub [Microsoft Drivers para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases). Cada pacote de instalação contém arquivos de driver SQLSRV e PDO_SQLSRV em variantes com thread e sem thread. No Windows, eles também estão disponíveis em variantes de 32 bits e 64 bits. Confira [Requisitos do Sistema para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md) para obter uma lista dos arquivos de driver contidos em cada pacote. O arquivo de driver deve corresponder à versão do PHP, à arquitetura e aos threads do seu ambiente PHP.

No Linux e no macOS, os drivers também podem ser instalados usando o PECL, conforme encontrado no [tutorial de instalação](../../connect/php/installation-tutorial-linux-mac.md).

Você também pode criar os drivers com base na origem ao criar o PHP ou usando `phpize`. Se optar por criar os drivers com base na origem, você terá a opção de criá-los estaticamente no PHP em vez de criá-los como extensões compartilhadas adicionando `--enable-sqlsrv=static --with-pdo_sqlsrv=static` (no Linux e macOS) ou `--enable-sqlsrv=static --with-pdo-sqlsrv=static` (no Windows) ao comando `./configure` ao criar o PHP. Para obter mais informações sobre o sistema de build do PHP e `phpize`, confira a [documentação do PHP](http://php.net/manual/install.php).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Movendo o arquivo de driver para o diretório de extensões  
O arquivo de driver deve estar localizado em um diretório em que o runtime do PHP possa encontrá-lo. É mais fácil colocar o arquivo de driver em seu diretório de extensões do PHP padrão – para localizar o diretório padrão, execute `php -i | sls extension_dir` no Windows ou `php -i | grep extension_dir` no Linux/macOS. Se você não estiver usando o diretório de extensões padrão, especifique um diretório no arquivo de configuração do PHP (php.ini), usando a opção **extension_dir**. Por exemplo, no Windows, se você colocar o arquivo de driver em seu diretório `c:\php\ext`, adicione a seguinte linha a php.ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Carregando o driver na inicialização do PHP  
Para carregar o driver SQLSRV quando o PHP é iniciado, coloque antes o arquivo do driver no diretório de extensões. Então, siga estas etapas:  
  
1.  Para habilitar o driver **SQLSRV**, modifique **php.ini** adicionando a seguinte linha à seção da extensão, alterando o nome do arquivo conforme apropriado:  
  
    No Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    No Linux, se você tiver baixado os binários predefinidos para sua distribuição: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Se você tiver compilado o binário SQLSRV com base na origem ou com PECL, ele terá o nome sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  Para habilitar o driver **PDO_SQLSRV**, a extensão PDO (Objetos de Dados do PHP) deve estar disponível, como uma extensão interna ou carregada dinamicamente.

    No Windows, os binários do PHP predefinidos vêm com PDO interno, portanto, não há necessidade de modificar o php.ini para carregá-lo. Se, no entanto, você tiver compilado o PHP com base na origem e especificado que uma extensão PDO separada deva ser criada, ele terá o nome `php_pdo.dll` e você deverá copiá-lo para o diretório de extensões e adicionar a seguinte linha a php.ini:  
    ```
    extension=php_pdo.dll  
    ```
    No Linux, se você tiver instalado o PHP usando o gerenciador de pacotes do sistema, o PDO provavelmente será instalado como uma extensão carregada dinamicamente chamada pdo.so. A extensão PDO deve ser carregada antes da extensão PDO_SQLSRV ou o carregamento falhará. Normalmente, as extensões são carregadas usando arquivos .ini individuais, os quais são lidos após php.ini. Portanto, se pdo.so for carregado por meio do próprio arquivo .ini dele, será necessário um arquivo separado que carrega o driver PDO_SQLSRV após PDO. 

    Para descobrir em qual diretório os arquivos .ini específicos da extensão estão localizados, execute `php --ini` e observe o diretório listado em `Scan for additional .ini files in:`. Localize o arquivo que carrega pdo.so – ele provavelmente será prefixado por um número, como 10-pdo.ini. O prefixo numérico indica a ordem de carregamento dos arquivos .ini, enquanto os arquivos que não têm um prefixo numérico são carregados alfabeticamente. Crie um arquivo para carregar o arquivo de driver PDO_SQLSRV denominado 30-pdo_sqlsrv.ini (qualquer número maior do que aquele que é o prefixo de pdo.ini funciona) ou pdo_sqlsrv.ini (se pdo.ini não estiver prefixado por um número) e adicione a seguinte linha a ele, alterando o nome do arquivo conforme apropriado:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Como ocorre com SQLSRV, se você tiver compilado o binário PDO_SQLSRV com base na origem ou com PECL, ele terá o nome pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    Copie esse arquivo para o diretório que contém os outros arquivos .ini. 

    Se você tiver compilado o PHP com base na origem com suporte de PDO interno, você não precisará de um arquivo .ini separado e poderá adicionar a linha apropriada acima ao php.ini.
  
3.  Reinicie o servidor Web.  
  
> [!NOTE]  
> Para determinar se o driver foi carregado com êxito, execute um script que chama [phpinfo()](https://php.net/manual/en/function.phpinfo.php).  
  
Para obter mais informações sobre as diretivas do **php.ini**, veja [Descrição das principais diretivas do php.ini](https://php.net/manual/en/ini.core.php).  
  
## <a name="see-also"></a>Consulte Também  
[Introdução aos Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Requisitos do sistema para os Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Guia de programação do Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referência da API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
