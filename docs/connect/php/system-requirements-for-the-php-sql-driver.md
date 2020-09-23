---
title: Requisitos do sistema para Microsoft Drivers for PHP
description: Os Microsoft Drivers for PHP for SQL Server dão suporte a uma grande variedade de versões do PHP, de sistemas operacionais e de versões do SQL Server.
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e0ae11dd3a13ac8b2071943c49ef1ae4b8c400f4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540460"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Requisitos do sistema para os Microsoft Drivers for PHP for SQL Server

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este artigo lista os componentes que devem ser instalados em seu sistema para acessar dados em um SQL Server ou no Banco de Dados SQL do Azure usando o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].

As versões 3.2 e posteriores dos Drivers PHP da Microsoft para SQL Server são oficialmente compatíveis. Para obter detalhes completos sobre os ciclos de vida de suporte e sobre os requisitos dos drivers PHP, confira a [matriz de suporte](microsoft-php-drivers-for-sql-server-support-matrix.md).

## <a name="php"></a>PHP

Para obter informações sobre como baixar e instalar os últimos binários estáveis do PHP, confira o [site do PHP](https://php.net).  Os Drivers da Microsoft para PHP e para SQL Server exigem as versões corretas do PHP, conforme detalhado no [Suporte à versão do PHP](microsoft-php-drivers-for-sql-server-support-matrix.md#php-version-support).

-   A versão correta do arquivo de driver deve ser habilitada com a versão do PHP correspondente. Confira as [Versões do Driver](#driver-versions) para obter informações sobre os diferentes arquivos de driver.  Para baixar os drivers, confira [Baixar Microsoft Drivers for PHP for SQL Server](download-drivers-php-sql-server.md). Para obter informações sobre como configurar o driver para o PHP, confira [Carregando os Microsoft Drivers for PHP for SQL Server](loading-the-php-sql-driver.md).

-   Um servidor Web é necessário. O servidor Web deve ser configurado para executar o PHP. Para obter informações sobre como hospedar aplicativos PHP com o IIS, confira o [tutorial no site da Web do PHP](http://docs.php.net/manual/da/install.windows.iis7.php).

    O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] foi testado usando o IIS 10 com FastCGI.

    > [!NOTE]
    > A Microsoft fornece suporte somente para o IIS.

## <a name="odbc-driver"></a>Driver ODBC

É necessário ter a versão correta do Microsoft ODBC Driver for SQL Server no computador em que o PHP está em execução. É possível baixar todas as versões do driver para plataformas compatíveis [nesta página](../odbc/download-odbc-driver-for-sql-server.md).

Caso esteja baixando a versão Windows do driver em uma versão de 64 bits do Windows, o instalador de ODBC de 64 bits instalará os drivers de 32 bits e de 64 bits. Caso tenha uma versão de 32 bits do Windows, use o instalador ODBC x86. Em plataformas não Windows, somente as versões de 64 bits do driver estão disponíveis.

|Versão do driver PHP &#8594;<br />&#8595; Versão do driver ODBC|5.8|5.6|5,3|5.2|4.3|4,0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC Driver 17+ |Sim|Sim|Sim|Sim|   |   |   |
|ODBC Driver 13.1|Sim|Sim|Sim|Sim|Sim|Sim|   |
|ODBC Driver 13  |   |   |   |   |   |Sim|   |
|ODBC Driver 11  |Sim|Sim|Sim|Sim|Sim|Sim|Sim|

Caso esteja usando o driver SQLSRV, o [sqlsrv_client_info](sqlsrv-client-info.md) retornará informações sobre qual versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft ODBC Driver for SQL Server está sendo usada pelo [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Se estiver usando o driver PDO_SQLSRV, use [PDO::getAttribute](pdo-getattribute.md) para descobrir a versão.

## <a name="sql-server"></a>SQL Server

Confira [versões de banco de dados com suporte](microsoft-php-drivers-for-sql-server-support-matrix.md#sql-server-version-certified-compatibility) para saber detalhes sobre quais versões do SQL Server têm suporte.

## <a name="operating-systems"></a>Sistemas operacionais

Confira os [sistemas operacionais compatíveis](microsoft-php-drivers-for-sql-server-support-matrix.md#supported-operating-systems) para obter detalhes sobre quais sistemas operacionais são compatíveis.

## <a name="driver-versions"></a>Versões de driver

Esta seção lista os arquivos de driver incluídos em cada versão do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Cada pacote de instalação contém arquivos de driver SQLSRV e PDO_SQLSRV em variantes com thread e sem thread. No Windows, eles também estão disponíveis em variantes de 32 bits e 64 bits. Para configurar o driver e usar com o runtime do PHP, siga as instruções de instalação em [Como carregar os Drivers da Microsoft para PHP e para SQL Server](loading-the-php-sql-driver.md).

Nas versões compatíveis do Linux e do macOS, os drivers apropriados podem ser instalados usando o sistema de pacotes PECL do PHP, seguindo as [Instruções de instalação do Linux e do macOS](installation-tutorial-linux-mac.md). Como alternativa é possível baixar binários predefinidos para sua plataforma na página de projetos do GitHub [Drivers da Microsoft para PHP e para SQL Server](https://github.com/Microsoft/msphpsql/releases). As tabelas abaixo listam os arquivos encontrados nos pacotes binários predefinidos.

**Drivers 5.8 da Microsoft para PHP e para SQL Server:**

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|
|---------------|:---------------:|:----------------:|---------------------|
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|não |php7.dll de 32 bits|
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sim|php7ts.dll de 32 bits|
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|não |php7.dll de 64 bits|
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sim|php7ts.dll de 64 bits|
|php_sqlsrv_73_nts.dll de 32 bits<br />php_pdo_sqlsrv_73_nts.dll de 32 bits|7.3|não |php7.dll de 32 bits|
|php_sqlsrv_73_ts.dll de 32 bits <br />php_pdo_sqlsrv_73_ts.dll de 32 bits |7.3|sim|php7ts.dll de 32 bits|
|php_sqlsrv_73_nts.dll de 64 bits<br />php_pdo_sqlsrv_73_nts.dll de 64 bits|7.3|não |php7.dll de 64 bits|
|php_sqlsrv_73_ts.dll de 64 bits <br />php_pdo_sqlsrv_73_ts.dll de 64 bits |7.3|sim|php7ts.dll de 64 bits|
|php_sqlsrv_74_nts.dll de 32 bits<br />php_pdo_sqlsrv_74_nts.dll de 32 bits|7.4|não |php7.dll de 32 bits|
|php_sqlsrv_74_ts.dll de 32 bits <br />php_pdo_sqlsrv_74_ts.dll de 32 bits |7.4|sim|php7ts.dll de 32 bits|
|php_sqlsrv_74_nts.dll de 64 bits<br />php_pdo_sqlsrv_74_nts.dll de 64 bits|7.4|não |php7.dll de 64 bits|
|php_sqlsrv_74_ts.dll de 64 bits <br />php_pdo_sqlsrv_74_ts.dll de 64 bits |7.4|sim|php7ts.dll de 64 bits|

No Linux, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|não |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|sim|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|não |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|sim|
|php_sqlsrv_74_nts.so<br />php_pdo_sqlsrv_74_nts.so|7.4|não |
|php_sqlsrv_74_ts.so <br />php_pdo_sqlsrv_74_ts.so |7.4|sim|

**Microsoft Drivers 5.6 para PHP para SQL Server:**

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|
|---------------|:---------------:|:----------------:|---------------------|
|php_sqlsrv_71_nts.dll de 32 bits<br />php_pdo_sqlsrv_71_nts.dll de 32 bits|7.1|não |php7.dll de 32 bits|
|php_sqlsrv_71_ts.dll de 32 bits <br />php_pdo_sqlsrv_71_ts.dll de 32 bits |7.1|sim|php7ts.dll de 32 bits|
|php_sqlsrv_71_nts.dll de 64 bits<br />php_pdo_sqlsrv_71_nts.dll de 64 bits|7.1|não |php7.dll de 64 bits|
|php_sqlsrv_71_ts.dll de 64 bits <br />php_pdo_sqlsrv_71_ts.dll de 64 bits |7.1|sim|php7ts.dll de 64 bits|
|php_sqlsrv_72_nts.dll de 32 bits<br />php_pdo_sqlsrv_72_nts.dll de 32 bits|7.2|não |php7.dll de 32 bits|
|php_sqlsrv_72_ts.dll de 32 bits <br />php_pdo_sqlsrv_72_ts.dll de 32 bits |7.2|sim|php7ts.dll de 32 bits|
|php_sqlsrv_72_nts.dll de 64 bits<br />php_pdo_sqlsrv_72_nts.dll de 64 bits|7.2|não |php7.dll de 64 bits|
|php_sqlsrv_72_ts.dll de 64 bits <br />php_pdo_sqlsrv_72_ts.dll de 64 bits |7.2|sim|php7ts.dll de 64 bits|
|php_sqlsrv_73_nts.dll de 32 bits<br />php_pdo_sqlsrv_73_nts.dll de 32 bits|7.3|não |php7.dll de 32 bits|
|php_sqlsrv_73_ts.dll de 32 bits <br />php_pdo_sqlsrv_73_ts.dll de 32 bits |7.3|sim|php7ts.dll de 32 bits|
|php_sqlsrv_73_nts.dll de 64 bits<br />php_pdo_sqlsrv_73_nts.dll de 64 bits|7.3|não |php7.dll de 64 bits|
|php_sqlsrv_73_ts.dll de 64 bits <br />php_pdo_sqlsrv_73_ts.dll de 64 bits |7.3|sim|php7ts.dll de 64 bits|

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
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|não |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|sim|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|não |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|sim|

**Microsoft Drivers 4.0 for PHP for SQL Server:**

No Windows, as seguintes versões do driver estão incluídas:

|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|
|---------------|:---------------:|:----------------:|---------------------|
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|não|php7.dll de 32 bits|
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|sim|php7ts.dll de 32 bits|
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|não|php7.dll de 64 bits|
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|sim|php7ts.dll de 64 bits|

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

## <a name="see-also"></a>Consulte Também

- [Introdução aos Drivers da Microsoft para PHP para SQL Server](getting-started-with-the-php-sql-driver.md)
- [Guia de programação do Microsoft Drivers para PHP para SQL Server](programming-guide-for-php-sql-driver.md)
- [Referência da API do driver SQLSRV](sqlsrv-driver-api-reference.md)
- [Referência da API do Driver PDO_SQLSRV](pdo-sqlsrv-driver-reference.md)
