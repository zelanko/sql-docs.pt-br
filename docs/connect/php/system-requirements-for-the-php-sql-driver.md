---
title: Requisitos do sistema para os Microsoft Drivers for PHP for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
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
ms.openlocfilehash: b601d4fbb02b489aca228acb719cfe8bad834dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992572"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Requisitos do sistema para os Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este documento lista os componentes que devem ser instalados em seu sistema para acessar dados em um SQL Server ou em um banco de dados [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]SQL do Azure usando o.

As versões 3,1 e posteriores dos drivers do Microsoft PHP para SQL Server são oficialmente suportadas. Para obter detalhes completos sobre os requisitos e os ciclos de vida de suporte, incluindo versões anteriores dos drivers do PHP, consulte a [matriz de suporte](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md).

## <a name="php"></a>PHP

Para obter informações sobre como baixar e instalar os últimos binários estáveis do PHP, confira o [site do PHP](https://php.net).  Os drivers da Microsoft para PHP para SQL Server exigem as seguintes versões do PHP:

|PHP para versão do driver SQL Server&#8594;<br />&#8595; Versão do PHP|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|:---:|---|---|---|---|---|---|---|
|7.3|7.3.0+ | | | | | | |
|7.2|7.2 +<sup>1</sup>|7.2 +<sup>1</sup>|7.2 +<sup>1</sup>| | | | |
|7.1|7.1.0+ |7.1.0+ |7.1.0+ |7.1.0+ |       |        |        |
|7.0|       |7.0.0+ |7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |       |       |5.6.4+  |        |
|5.5|       |       |       |       |       |5.5.16+ |5.5.16+ |
|5.4|       |       |       |       |       |5.4.32  |5.4.32  |

1. As versões 7.2.1 e posteriores têm suporte no Windows, enquanto as versões 7.2.0 e posteriores têm suporte no Linux e no macOS.

-   Uma versão do arquivo do driver deve estar no seu diretório de extensões do PHP. Consulte [versões de driver](#driver-versions) para obter informações sobre os diferentes arquivos de driver.  Para baixar os drivers, confira [Baixar Microsoft Drivers for PHP for SQL Server](../../connect/php/download-drivers-php-sql-server.md). Para obter informações sobre como configurar o driver para o PHP, confira [Carregando os Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md).

-   Um servidor Web é necessário. O servidor Web deve ser configurado para executar o PHP. Para obter informações sobre como hospedar aplicativos PHP com o IIS, consulte o [tutorial no site do PHP](http://docs.php.net/manual/da/install.windows.iis7.php).

    O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] foi testado usando o IIS 10 com FastCGI.  

    > [!NOTE]  
    > A Microsoft fornece suporte somente para o IIS.  

## <a name="odbc-driver"></a>Driver ODBC

A versão correta do Microsoft ODBC Driver for SQL Server é necessária no computador no qual o PHP está em execução. Você pode baixar todas as versões com suporte do driver para plataformas com suporte nesta [página](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017).

Se você estiver baixando a versão do Windows do driver em uma versão de 64 bits do Windows, o instalador ODBC 64-bit instalará drivers ODBC de 32 bits e de 64 bits. Se você usar uma versão de 32 bits do Windows, use o instalador ODBC x86. Em plataformas não Windows, somente as versões de 64 bits do driver estão disponíveis.

|PHP para versão do driver SQL Server&#8594;<br />&#8595; Versão do ODBC Driver|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC Driver 17+ |S|S|S| | | | |
|ODBC Driver 13.1|S|S|S|S|S| | |
|ODBC Driver 13  | | | | |S| | |
|ODBC Driver 11  |S|S|S|S|S|S|S|

Se você estiver usando o driver sqlsrv, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) retornará informações sobre qual versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft ODBC driver for SQL Server está [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]sendo usada pelo. Se estiver usando o driver PDO_SQLSRV, use [PDO::getAttribute](../../connect/php/pdo-getattribute.md) para descobrir a versão.  

## <a name="sql-server"></a>SQL Server

Há suporte para bancos de dados SQL do Azure. Para obter informações, confira [Conectando-se ao Banco de Dados SQL do Microsoft Azure](../../connect/php/connecting-to-microsoft-azure-sql-database.md).

|PHP para versão do driver SQL Server&#8594;<br />&#8595; Versão do SQL Server|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Banco de dados SQL do Azure        |S|S|S|S| | | |
|Instância Gerenciada do SQL do Azure|S|S|S|S| | | |
|Azure SQL Data Warehouse  |S|S|S|S| | | |
|SQL Server 2017           |S|S|S|S| | | |
|SQL Server 2016           |S|S|S|S|S| | |
|SQL Server 2014           |S|S|S|S|S|S|S|
|SQL Server 2012           |S|S|S|S|S|S|S|
|SQL Server 2008 R2        |S|S|S|S|S|S|S|
|SQL Server 2008           | | | | |S|S|S|

## <a name="operating-systems"></a>Sistemas operacionais
Os sistemas operacionais com suporte para cada versão do driver são os seguintes:

|PHP para versão do driver SQL Server&#8594;<br />&#8595; Sistema operacional|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |S  |S  |S  |S  |   |   |   |
|Windows Server 2012 R2              |S  |S  |S  |S  |S  |S  |S  |
|Windows Server 2012                 |S  |S  |S  |S  |S  |S  |S  |
|Windows Server 2008 R2 SP1          |   |   |   |   |S  |S  |S  |
|Windows Server 2008 SP2             |   |   |   |   |S  |S  |S  |
|Windows 10                          |S  |S  |S  |S  |S  |   |   |
|Windows 8.1                         |S  |S  |S  |S  |S  |S  |S  |
|Windows 8                           |   |   |   |S  |S  |S  |S  |
|Windows 7 SP1                       |   |   |   |   |S  |S  |S  |
|Windows Vista SP2                   |   |   |   |   |S  |S  |S  |
|Ubuntu 18,10 (64 bits)               |S  |   |   |   |   |   |   |
|Ubuntu 18, 4 (64 bits)               |S  |S  |   |   |   |   |   |
|Ubuntu 17,10 (64 bits)               |   |S  |S  |   |   |   |   |
|Ubuntu 16, 4 (64 bits)               |S  |S  |S  |S  |S  |   |   |
|Ubuntu 15,10 (64 bits)               |   |   |   |S  |   |   |   |
|Ubuntu 15, 4 (64 bits)               |   |   |   |   |S  |   |   |
|Debian 9 (64 bits)                   |S  |S  |S  |   |   |   |   |
|Debian 8 (64 bits)                   |S  |S  |S  |S  |   |   |   |
|Red Hat Enterprise Linux 7 (64 bits) |S  |S  |S  |S  |S  |   |   |
|SuSE Enterprise Linux 15 (64 bits)   |S  |   |   |   |   |   |   |
|SuSE Enterprise Linux 12 (64 bits)   |S  |S  |S  |   |   |   |   |
|macOS Mojave (64 bits)               |S  |   |   |   |   |   |   |
|macOS High Sierra (64 bits)          |S  |S  |   |   |   |   |   |
|macOS Sierra (64 bits)               |S  |S  |S  |S  |   |   |   |
|macOS El Capitan (64 bits)           |   |S  |S  |S  |   |   |   |

## <a name="driver-versions"></a>Versões de driver  
Esta seção lista os arquivos de driver incluídos em cada versão do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Cada pacote de instalação contém arquivos de driver SQLSRV e PDO_SQLSRV em variantes threaded e não threaded. No Windows, eles também estão disponíveis em variantes de 32 bits e 64 bits. Para configurar o driver para uso com o tempo de execução do PHP, siga as instruções de instalação em [carregando os drivers da Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md).

Nas versões com suporte do Linux e do macOS, os drivers apropriados podem ser instalados usando o sistema de pacotes PECL do PHP, seguindo as [instruções de instalação do Linux e do MacOS](../../connect/php/installation-tutorial-linux-mac.md). Como alternativa, você pode baixar binários pré-criados para sua plataforma na página de projeto [drivers da Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) GitHub--as tabelas abaixo listam os arquivos encontrados nos pacotes binários predefinidos.

**Microsoft Drivers 5.6 para PHP para SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|não |32 bits Php7. dll|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sim|32 bits php7ts. dll|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|não |64 bits Php7. dll|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sim|64 bits php7ts. dll|   
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|não |32 bits Php7. dll|  
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sim|32 bits php7ts. dll|  
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|não |64 bits Php7. dll|  
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sim|64 bits php7ts. dll|  
|php_sqlsrv_73_nts.dll de 32 bits<br />php_pdo_sqlsrv_73_nts.dll de 32 bits|7.3|não |32 bits Php7. dll|  
|php_sqlsrv_73_ts.dll de 32 bits <br />php_pdo_sqlsrv_73_ts.dll de 32 bits |7.3|sim|32 bits php7ts. dll|  
|php_sqlsrv_73_nts.dll de 64 bits<br />php_pdo_sqlsrv_73_nts.dll de 64 bits|7.3|não |64 bits Php7. dll|  
|php_sqlsrv_73_ts.dll de 64 bits <br />php_pdo_sqlsrv_73_ts.dll de 64 bits |7.3|sim|64 bits php7ts. dll|  

No Linux, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|não |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sim|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|não |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sim|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|não |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|sim|

**Microsoft Drivers 5.3 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|não |32 bits Php7. dll|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sim|32 bits php7ts. dll|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|não |64 bits Php7. dll|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sim|64 bits php7ts. dll|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|não |32 bits Php7. dll|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sim|32 bits php7ts. dll|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|não |64 bits Php7. dll|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sim|64 bits php7ts. dll|   
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|não |32 bits Php7. dll|  
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sim|32 bits php7ts. dll|  
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|não |64 bits Php7. dll|  
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sim|64 bits php7ts. dll|  

No Linux, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|não |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sim|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|não |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sim|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|não |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sim|

**Microsoft Drivers 5.2 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|não |32 bits Php7. dll|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sim|32 bits php7ts. dll|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|não |64 bits Php7. dll|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sim|64 bits php7ts. dll|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|não |32 bits Php7. dll|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sim|32 bits php7ts. dll|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|não |64 bits Php7. dll|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sim|64 bits php7ts. dll|   
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|não |32 bits Php7. dll|  
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sim|32 bits php7ts. dll|  
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|não |64 bits Php7. dll|  
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sim|64 bits php7ts. dll|  

No Linux, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|não |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sim|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|não |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sim|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|não |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sim|

**Microsoft Drivers 4.3 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts.dll de 32 bits <br />php_pdo_sqlsrv_7_nts.dll de 32 bits |7.0|não |32 bits Php7. dll|
|php_sqlsrv_7_ts.dll de 32 bits  <br />php_pdo_sqlsrv_7_ts.dll de 32 bits  |7.0|sim|32 bits php7ts. dll|
|php_sqlsrv_7_nts.dll de 64 bits <br />php_pdo_sqlsrv_7_nts.dll de 64 bits |7.0|não |64 bits Php7. dll|  
|php_sqlsrv_7_ts.dll de 64 bits  <br />php_pdo_sqlsrv_7_ts.dll de 64 bits  |7.0|sim|64 bits php7ts. dll|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|não |32 bits Php7. dll|  
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sim|32 bits php7ts. dll|  
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|não |64 bits Php7. dll|  
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sim|64 bits php7ts. dll|   

No Linux, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|não |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sim|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|não |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sim|  

**Microsoft Drivers 4.0 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|não|32 bits Php7. dll|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|sim|32 bits php7ts. dll|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|não|64 bits Php7. dll|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|sim|64 bits php7ts. dll|   

No Linux, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|não |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sim|

**Microsoft Drivers 3.2 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|não|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sim|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|não|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sim|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|não|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|sim|php5ts.dll|  

**Microsoft Drivers 3.1 for PHP for SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|não|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sim|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|não|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sim|php5ts.dll|  

## <a name="see-also"></a>Consulte Também  
[Introdução aos Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Guia de programação para o Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referência da API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
