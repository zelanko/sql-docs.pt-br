---
title: Requisitos de sistema para os Drivers da Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/23/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: 93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23b8c2e8fe5545f19848f589a2a830c1d402c8d5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Requisitos de sistema para os Drivers da Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este documento lista os componentes que devem ser instalados em seu sistema para acessar dados em um SQL Server ou banco de dados do SQL Azure usando o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].

Versões 3.1 e posterior dos Drivers de PHP da Microsoft para SQL Server têm suporte oficialmente. Para obter detalhes completos sobre os ciclos de vida de suporte e requisitos, incluindo versões anteriores dos drivers de PHP, consulte o [matriz de suporte](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md).

## <a name="php"></a>PHP

Para obter informações sobre como baixar e instalar os binários do PHP estáveis mais recentes, consulte [o site do PHP](http://php.net).  Os Drivers da Microsoft para PHP para SQL Server requerem as seguintes versões do PHP:

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595;Versão do PHP|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|7.2|7.2.1+ no Windows<br/>7.2.0+ em outras plataformas | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |5.6.4 +  |        |
|5.5|       |       |       |5.5.16 + |5.5.16 + |
|5.4|       |       |       |5.4.32  |5.4.32  |

-   Uma versão do arquivo do driver deve estar no seu diretório de extensões do PHP. Consulte [versões de Driver](#driver-versions) para obter informações sobre os diferentes arquivos de driver.  Para baixar os drivers, consulte [baixar os Drivers da Microsoft para PHP para SQL Server](download-drivers-php-sql-server.md). Para obter informações sobre como configurar o driver para PHP, consulte [carregando os Drivers da Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md).

-   Um servidor Web é necessário. O servidor Web deve ser configurado para executar o PHP. Para obter informações sobre como hospedar aplicativos PHP no IIS, consulte o [tutorial no site do PHP](http://php.net/manual/fa/install.windows.iis.php).  

    O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] foi testado usando o IIS 10 com FastCGI.  

    > [!NOTE]  
    > A Microsoft fornece suporte somente para o IIS.  

## <a name="odbc-driver"></a>Driver ODBC

A versão correta do Microsoft ODBC Driver para SQL Server é necessária no computador no qual o PHP está sendo executado. Baixe os links a seguir:
- [Microsoft ODBC Driver 17 para SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=56567)
- [Microsoft ODBC Driver 13.1 para SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=53339)
- [Microsoft ODBC Driver 13 para SQL Server](https://www.microsoft.com/download/details.aspx?id=50420)
- [Microsoft ODBC Driver 11 para SQL Server](http://www.microsoft.com/download/details.aspx?id=36434)

Se você estiver usando um sistema operacional de 64 bits, o instalador ODBC de 64 bits instala drivers ODBC de 32 bits e 64 bits. Se você usar um sistema operacional de 32 bits, use o ODBC x86 instalador.

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595;Versão do Driver ODBC|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Driver ODBC 17  |S| | | | |
|ODBC Driver 13.1|S|S|S| | |
|ODBC Driver 13  | | |S| | |
|Driver ODBC 11  |S|S|S|S|S|

Se você estiver usando o driver SQLSRV, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) retorna informações sobre qual versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Microsoft ODBC Driver para SQL Server está sendo usado pelo [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Se você estiver usando o driver PDO_SQLSRV, você pode usar [PDO:: GetAttribute](../../connect/php/pdo-getattribute.md) para descobrir a versão.  

## <a name="sql-server"></a>SQL Server

Há suporte para bancos de dados SQL do Azure. Para obter informações, consulte [se conectar ao banco de dados SQL do Microsoft Azure](../../connect/php/connecting-to-microsoft-azure-sql-database.md).

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595;Versão do SQL Server|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Instância gerenciada do SQL Azure<br/> (Visualização privada estendida)|S|S| | | |
|Azure SQL Data Warehouse|S|S| | | |
|SQL Server 2017   |S|S| | | |
|SQL Server 2016   |S|S|S| | |
|SQL Server 2014   |S|S|S|S|S|
|SQL Server 2012   |S|S|S|S|S|
|SQL Server 2008 R2|S|S|S|S|S|
|SQL Server 2008   | | |S|S|S|

## <a name="operating-systems"></a>Sistemas operacionais
Sistemas operacionais com suporte para as versões do driver são da seguinte maneira:

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595;Sistema Operacional|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Windows Server 2016                      |S|S| | | |
|Windows Server 2012 R2                   |S|S|S|S|S|
|Windows Server 2012                      |S|S|S|S|S|
|Windows Server 2008 R2 SP1               | | |S|S|S|
|Windows Server 2008 SP2                  | | |S|S|S|
|Windows 10                               |S|S|S| | |
|Windows 8.1                              |S|S|S|S|S|
|Windows 8                                | |S|S|S|S|
|Windows 7 SP1                            | | |S|S|S|
|Windows Vista SP2                        | | |S|S|S|
|Ubuntu 17.10 (64 bits)                    |S| | | | |
|Ubuntu 16.04 (64 bits)                    |S|S|S| | |
|Ubuntu 15.10 (64 bits)                    | |S| | | |
|Ubuntu 15.04 (64 bits)                    | | |S| | |
|Debian 9 (64 bits)                        |S| | | | |
|Debian 8 (64 bits)                        |S|S| | | |
|Red Hat Enterprise Linux 7 (64 bits)      |S|S|S| | |
|Linux SuSE Enterprise 12 (64 bits)        |S| | | | |
|macOS Serra (64 bits)                    |S|S| | | |
|macOS El Capitan (64 bits)                |S|S| | | |

## <a name="driver-versions"></a>Versões de driver  
Esta seção lista os arquivos de driver que são incluídos com cada versão do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Cada pacote de instalação contém arquivos de driver SQLSRV e PDO_SQLSRV em variants threads e não-threaded. No Windows, eles também estão disponíveis em variantes de 32 bits e 64 bits. Para configurar o driver para uso com o tempo de execução do PHP, siga as instruções de instalação em [carregando os Drivers da Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md).

Em versões do Linux e macOS, os drivers apropriados podem ser instalados usando o sistema de pacote PECL do PHP, seguindo o [instruções de instalação do Linux e macOS](../../connect/php/installation-tutorial-linux-mac.md). Como alternativa, você pode baixar pré-compilada binários para sua plataforma do [Drivers da Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) página de projeto do Github-- as tabelas a seguir listam os arquivos encontrados nos pacotes binários pré-compiladas.

**Drivers da Microsoft 5.2 para PHP para SQL Server:**  

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
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|não |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sim|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|não |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sim|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|não |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sim|

**Drivers da Microsoft 4.3 para PHP para SQL Server:**  

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
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|não |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sim|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|não |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sim|  

**Drivers da Microsoft 4.0 para PHP para SQL Server:**  

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
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|não |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sim|

**Drivers da Microsoft 3.2 para PHP para SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|não|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sim|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|não|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sim|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|não|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|sim|php5ts.dll|  

**Drivers da Microsoft 3.1 para PHP para SQL Server:**  

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|não|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|sim|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|não|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|sim|php5ts.dll|  

## <a name="see-also"></a>Consulte também  
[Guia de Introdução com os Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Programação de guia para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referência de API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
