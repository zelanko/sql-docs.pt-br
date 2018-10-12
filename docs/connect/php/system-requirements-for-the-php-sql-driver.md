---
title: Requisitos do sistema para os Microsoft Drivers for PHP for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/23/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c01d4f6af72fdc487b559a12f31bfcb447971cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603796"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Requisitos do sistema para os Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este documento lista os componentes que devem ser instalados em seu sistema para acessar dados em um SQL Server ou banco de dados SQL usando o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].

As versões 3.1 e posterior do Microsoft PHP Drivers para SQL Server são suportadas oficialmente. Para obter detalhes completos sobre os ciclos de vida de suporte e requisitos, incluindo versões anteriores dos drivers de PHP, consulte a [matriz de suporte](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md).

## <a name="php"></a>PHP

Para obter informações sobre como baixar e instalar os últimos binários estáveis do PHP, confira o [site do PHP](http://php.net).  O Microsoft Drivers for PHP para SQL Server exigem as seguintes versões do PHP:

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595; Versão do PHP|as versões 5.3 e 5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|7.2|7.2.1+ no Windows<br/>7.2.0+ em outras plataformas | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |5.6.4 +  |        |
|5.5|       |       |       |5.5.16 + |5.5.16 + |
|5.4|       |       |       |5.4.32  |5.4.32  |

-   Uma versão do arquivo do driver deve estar no seu diretório de extensões do PHP. Ver [versões de Driver](#driver-versions) para obter informações sobre os diferentes arquivos de driver.  Para baixar os drivers, confira [Baixar Microsoft Drivers for PHP for SQL Server](download-drivers-php-sql-server.md). Para obter informações sobre como configurar o driver para o PHP, confira [Carregando os Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md).

-   Um servidor Web é necessário. O servidor Web deve ser configurado para executar o PHP. Para obter informações sobre como hospedar aplicativos PHP com o IIS, consulte a [tutorial no site de web do PHP](http://php.net/manual/fa/install.windows.iis.php).  

    O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] foi testado usando o IIS 10 com FastCGI.  

    > [!NOTE]  
    > A Microsoft fornece suporte somente para o IIS.  

-   Versão 5.3 do Microsoft Drivers for PHP para SQL Server será a última para dar suporte a PHP 7.0.

## <a name="odbc-driver"></a>Driver ODBC

A versão correta do Microsoft ODBC Driver para SQL Server é necessária no computador que está executando o PHP. Você pode baixar todas as versões suportadas do driver para plataformas com suporte no [nesta página](https://docs.microsoft.com/en-us/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017).

Se você estiver baixando a versão do Windows do driver em uma versão de 64 bits do Windows, o instalador de ODBC 64-bit instala drivers ODBC de 32 bits e 64 bits. Se você usar uma versão de 32 bits do Windows, use o ODBC x86 instalador. Em plataformas não Windows, versões de 64 bits somente do driver estão disponíveis.

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595;Versão do Driver ODBC|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|---|
|ODBC Driver 17+ |S|S| | | | |
|ODBC Driver 13.1|S|S|S|S| | |
|ODBC Driver 13  | | | |S| | |
|ODBC Driver 11  |S|S|S|S|S|S|

Se você estiver usando o driver SQLSRV, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) retorna informações sobre qual versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft ODBC Driver for SQL Server está sendo usado pelo [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Se estiver usando o driver PDO_SQLSRV, use [PDO::getAttribute](../../connect/php/pdo-getattribute.md) para descobrir a versão.  

## <a name="sql-server"></a>SQL Server

Há suporte para bancos de dados SQL do Azure. Para obter informações, confira [Conectando-se ao Banco de Dados SQL do Microsoft Azure](../../connect/php/connecting-to-microsoft-azure-sql-database.md).

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595; Versão do SQL Server|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|---|
|Banco de dados SQL do Azure        |S|S|S| | | |
|Instância Gerenciada do SQL do Azure|S|S|S| | | |
|Azure SQL Data Warehouse  |S|S|S| | | |
|SQL Server 2017           |S|S|S| | | |
|SQL Server 2016           |S|S|S|S| | |
|SQL Server 2014           |S|S|S|S|S|S|
|SQL Server 2012           |S|S|S|S|S|S|
|SQL Server 2008 R2        |S|S|S|S|S|S|
|SQL Server 2008           | | | |S|S|S|

## <a name="operating-systems"></a>Sistemas operacionais
Sistemas operacionais com suporte para as versões do driver são da seguinte maneira:

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595; Sistema operacional|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|---|
|Windows Server 2016                      |S|S|S| | | |
|Windows Server 2012 R2                   |S|S|S|S|S|S|
|Windows Server 2012                      |S|S|S|S|S|S|
|Windows Server 2008 R2 SP1               | | | |S|S|S|
|Windows Server 2008 SP2                  | | | |S|S|S|
|Windows 10                               |S|S|S|S| | |
|Windows 8.1                              |S|S|S|S|S|S|
|Windows 8                                | | |S|S|S|S|
|Windows 7 SP1                            | | | |S|S|S|
|Windows Vista SP2                        | | | |S|S|S|
|Ubuntu 18.04 (64 bits)                    |S| | | | | |
|Ubuntu 17.10 (64 bits)                    |S|S| | | | |
|Ubuntu 16.04 (64 bits)                    |S|S|S|S| | |
|Ubuntu 15.10 (64 bits)                    | | |S| | | |
|Ubuntu 15.04 (64 bits)                    | | | |S| | |
|Debian 9 (64 bits)                        |S|S| | | | |
|Debian 8 (64 bits)                        |S|S|S| | | |
|Red Hat Enterprise Linux 7 (64 bits)      |S|S|S|S| | |
|SuSE Enterprise Linux 12 (64 bits)        |S|S| | | | |
|macOS High Sierra (64 bits)               |S| | | | | |
|macOS Sierra (64 bits)                    |S|S|S| | | |
|macOS El Capitan (64 bits)                |S|S|S| | | |

## <a name="driver-versions"></a>Versões de driver  
Esta seção lista os arquivos de driver que são incluídos com cada versão do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Cada pacote de instalação contém arquivos de driver SQLSRV e PDO_SQLSRV na variantes de threads e não-threaded. No Windows, eles também estão disponíveis no variantes de 32 bits e 64 bits. Para configurar o driver para uso com o tempo de execução do PHP, siga as instruções de instalação em [carregando os Drivers da Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md).

Em versões compatíveis do Linux e macOS, os drivers apropriados podem ser instalados usando o sistema de pacote PECL do PHP, seguindo a [instruções de instalação do Linux e macOS](../../connect/php/installation-tutorial-linux-mac.md). Como alternativa, você pode baixar os binários pré-criados para sua plataforma do [Drivers da Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) página do projeto do Github – as tabelas abaixo listam os arquivos encontrados nos pacotes binários pré-criados.

**Microsoft Drivers 5.3 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|não |php7.dll de 32 bits|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sim|php7ts.dll de 32 bits|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|não |php7.dll de 64 bits|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sim|php7ts.dll de 64 bits|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|não |php7.dll de 32 bits|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sim|php7ts.dll de 32 bits|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|não |php7.dll de 64 bits|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sim|php7ts.dll de 64 bits|   
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|não |php7.dll de 32 bits|  
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sim|php7ts.dll de 32 bits|  
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|não |php7.dll de 64 bits|  
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sim|php7ts.dll de 64 bits|  

No Linux, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.SO <br />php_pdo_sqlsrv_7_nts.SO |7.0|não |
|php_sqlsrv_7_ts.SO  <br />php_pdo_sqlsrv_7_ts.SO  |7.0|sim|
|php_sqlsrv_71_nts.SO<br />php_pdo_sqlsrv_71_nts.SO|7.1|não |
|php_sqlsrv_71_ts.SO <br />php_pdo_sqlsrv_71_ts.SO |7.1|sim|  
|php_sqlsrv_72_nts.SO<br />php_pdo_sqlsrv_72_nts.SO|7.2|não |
|php_sqlsrv_72_ts.SO <br />php_pdo_sqlsrv_72_ts.SO |7.2|sim|

**Microsoft Drivers 5.2 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|não |php7.dll de 32 bits|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sim|php7ts.dll de 32 bits|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|não |php7.dll de 64 bits|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sim|php7ts.dll de 64 bits|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|não |php7.dll de 32 bits|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sim|php7ts.dll de 32 bits|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|não |php7.dll de 64 bits|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sim|php7ts.dll de 64 bits|   
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|não |php7.dll de 32 bits|  
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sim|php7ts.dll de 32 bits|  
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|não |php7.dll de 64 bits|  
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sim|php7ts.dll de 64 bits|  

No Linux, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.SO <br />php_pdo_sqlsrv_7_nts.SO |7.0|não |
|php_sqlsrv_7_ts.SO  <br />php_pdo_sqlsrv_7_ts.SO  |7.0|sim|
|php_sqlsrv_71_nts.SO<br />php_pdo_sqlsrv_71_nts.SO|7.1|não |
|php_sqlsrv_71_ts.SO <br />php_pdo_sqlsrv_71_ts.SO |7.1|sim|  
|php_sqlsrv_72_nts.SO<br />php_pdo_sqlsrv_72_nts.SO|7.2|não |
|php_sqlsrv_72_ts.SO <br />php_pdo_sqlsrv_72_ts.SO |7.2|sim|

**Microsoft Drivers 4.3 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|não |php7.dll de 32 bits|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sim|php7ts.dll de 32 bits|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|não |php7.dll de 64 bits|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sim|php7ts.dll de 64 bits|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|não |php7.dll de 32 bits|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sim|php7ts.dll de 32 bits|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|não |php7.dll de 64 bits|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sim|php7ts.dll de 64 bits|   

No Linux, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.SO <br />php_pdo_sqlsrv_7_nts.SO |7.0|não |
|php_sqlsrv_7_ts.SO  <br />php_pdo_sqlsrv_7_ts.SO  |7.0|sim|
|php_sqlsrv_71_nts.SO<br />php_pdo_sqlsrv_71_nts.SO|7.1|não |
|php_sqlsrv_71_ts.SO <br />php_pdo_sqlsrv_71_ts.SO |7.1|sim|  

**Microsoft Drivers 4.0 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|não|php7.dll de 32 bits|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|sim|php7ts.dll de 32 bits|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|não|php7.dll de 64 bits|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|sim|php7ts.dll de 64 bits|   

No Linux, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.SO <br />php_pdo_sqlsrv_7_nts.SO |7.0|não |
|php_sqlsrv_7_ts.SO  <br />php_pdo_sqlsrv_7_ts.SO  |7.0|sim|

**Microsoft Drivers 3.2 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|não|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sim|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|não|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sim|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|não|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|sim|php5ts.dll|  

**Microsoft Drivers 3.1 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|não|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sim|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|não|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sim|php5ts.dll|  

## <a name="see-also"></a>Consulte Também  
[Guia de Introdução com os Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Guia de programação para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referência da API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
