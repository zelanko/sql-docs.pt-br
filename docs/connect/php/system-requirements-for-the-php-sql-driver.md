---
title: Requisitos do sistema para o Driver SQL de PHP | Microsoft Docs
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: 93
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba7e8cde4b8d3b77effca06b00303984223551f5
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-for-the-php-sql-driver"></a>Requisitos de sistema para o driver SQL do PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Para acessar dados em um SQL Server ou banco de dados do SQL Azure usando o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], você deve ter os seguintes componentes instalados no seu computador:  
  
-   PHP é necessário. Para obter informações sobre como baixar e instalar os binários estáveis mais recentes, consulte [http://php.net](http://go.microsoft.com/fwlink/?LinkId=101876).  Os Drivers da Microsoft para PHP para SQL Server requerem as seguintes versões:
  
|Versão dos Drivers da Microsoft para PHP para SQL Server|Versões do PHP com suporte|  
|----------------------------------------------------|--------------------------|  
|4.3|PHP 7.0 e PHP 7.1| 
|4.0|PHP 7.0|  
|3.2|PHP 5.6.4+ ou<br /><br />PHP 5.5.16+ ou<br /><br />PHP 5.4.32|  
|3.1|PHP 5.5.16+ ou<br /><br />PHP 5.4.32|  
|3.0|PHP 5.4.32 ou<br /><br />PHP 5.3.0|  
|2.0|PHP 5.3.0 ou<br /><br />PHP 5.2.4 ou<br /><br />PHP 5.2.13|  
  
-   Uma versão do arquivo do driver deve estar no seu diretório de extensões do PHP. Consulte Versões de driver mais adiante neste tópico para obter informações sobre os diferentes arquivos de driver. Consulte [Carregando o driver SQL do PHP](../../connect/php/loading-the-php-sql-driver.md)  para obter informações sobre como configurar o driver para o tempo de execução do PHP. Para baixar os drivers, consulte [Microsoft Drivers for PHP for SQL Server](http://www.microsoft.com/download/details.aspx?id=20098).  
  
-   Um servidor Web é necessário. O servidor Web deve ser configurado para executar o PHP. Para obter informações sobre como hospedar aplicativos PHP com os serviços de informações da Internet (IIS) 6.0, consulte [Using FastCGI to Host PHP Applications on IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=117131). Para obter informações sobre como hospedar aplicativos do PHP com o IIS 7.0, consulte [Using FastCGI to Host PHP Applications on IIS 7.0](http://go.microsoft.com/fwlink/?LinkId=117132).  
  
    O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] foi testado usando o IIS 6 e o IIS 7 com FastCGI.  
  
    > [!NOTE]  
    > A Microsoft fornece suporte somente para o IIS.  
  
-   A versão correta do Microsoft ODBC Driver para SQL Server ou SQL Server Native Client é necessária no computador em que o PHP está sendo executado.  Se você estiver usando um sistema operacional de 64 bits, o instalador ODBC de 64 bits instala drivers ODBC de 32 bits e 64 bits. Se você usar um sistema operacional de 32 bits, use o ODBC x86 instalador.

|Versão dos Drivers da Microsoft para PHP para SQL Server|Versão do Driver ODBC da Microsoft para SQL Server ou SQL Server Native Client|  
|----------------------------------------------------|--------------------------|
|4.3|Microsoft ODBC Driver 11 para SQL Server ou o Microsoft ODBC Driver 13.1 para SQL Server. Para baixar o Microsoft ODBC Driver, consulte o [Microsoft ODBC Driver 11 para a página do SQL Server](http://www.microsoft.com/download/details.aspx?id=36434) ou [Microsoft ODBC Driver 13.1 para a página do SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=53339)|    
|4.0|Microsoft ODBC Driver 11 para SQL Server ou o Microsoft ODBC Driver 13 para SQL Server. Para baixar o Microsoft ODBC Driver, consulte o [Microsoft ODBC Driver 11 para a página do SQL Server](http://www.microsoft.com/download/details.aspx?id=36434) ou [Microsoft ODBC Driver 13 para a página do SQL Server](https://www.microsoft.com/download/details.aspx?id=50420)|  
|3.2 ou <br><br> 3.1|Microsoft ODBC Driver 11 para SQL Server. Para baixar o Microsoft ODBC Driver, consulte o [Microsoft ODBC Driver 11 para a página do SQL Server](http://www.microsoft.com/download/details.aspx?id=36434)|   
|3.0|Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Native Client. Você pode baixar o Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Native Client na [página do SQL Server 2012 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=236805)| 
|2.0|Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro_md.md)] Native Client:<br /><br />[Baixar o pacote X86](http://go.microsoft.com/fwlink/?LinkID=188400&clcid=0x409) para sistemas operacionais de 32 bits <br /><br />[Baixar o pacote X64](http://go.microsoft.com/fwlink/?LinkID=188401&clcid=0x409) para sistemas operacionais de 64 bits|  

  
Se você estiver usando o driver SQLSRV, [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) retorna informações sobre qual versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Native Client ou o Microsoft ODBC Driver para SQL Server está sendo usado pelo [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Se você estiver usando o driver PDO_SQLSRV, você pode usar [PDO:: GetAttribute](../../connect/php/pdo-getattribute.md) para descobrir a versão.  



## <a name="database-versions"></a>Versões de banco de dados
-   Há suporte para bancos de dados SQL do Azure. Para obter informações, consulte [se conectar ao banco de dados SQL do Microsoft Azure](../../connect/php/connecting-to-microsoft-azure-sql-database.md). 

- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]versão 4.3 suporte do SQL Server 2008 R2 e posterior
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]suporte da versão 4.0 do SQL Server 2008 e posterior
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]suporte da versão 3.1 do SQL Server 2008 e posterior
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]suporte da versão 2.0 e 3.0 do SQL Server 2005 e versões posterior


## <a name="driver-versions"></a>Versões de driver  
Esta seção lista os drivers que estão incluídos com cada versão do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
Para configurar o driver para uso com o tempo de execução do PHP, siga as instruções de instalação em [carregando o Driver SQL de PHP](../../connect/php/loading-the-php-sql-driver.md).  
  
**Drivers da Microsoft 4.3 para PHP para SQL Server:**  

No Windows, para 4.3 as seguintes versões do driver estão instaladas:
  
|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|não|php7.dll de 32 bits| 
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|sim|php7ts.dll de 32 bits| 
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|não|php7.dll de 64 bits|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|sim|php7ts.dll de 64 bits| 
|php_sqlsrv_71_nts_x86.dll<br /><br />php_pdo_sqlsrv_71_nts_x86.dll|7.1|não|php7.dll de 32 bits|  
|php_sqlsrv_71_ts_x86.dll<br /><br />php_pdo_sqlsrv_71_ts_x86.dll|7.1|sim|php7ts.dll de 32 bits|  
|php_sqlsrv_71_nts_x64.dll<br /><br />php_pdo_sqlsrv_71_nts_x64.dll|7.1|não|php7.dll de 64 bits|  
|php_sqlsrv_71_ts_x64.dll<br /><br />php_pdo_sqlsrv_71_ts_x64.dll|7.1|sim|php7ts.dll de 64 bits|   
  
**Drivers da Microsoft 4.0 para PHP para SQL Server:**  

No Windows, para o 4.0 as seguintes versões do driver estão instaladas:
  
|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|não|php7.dll de 32 bits|  
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|sim|php7ts.dll de 32 bits|  
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|não|php7.dll de 64 bits|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|sim|php7ts.dll de 64 bits|   
  
Nas versões com suporte do Linux, a versão apropriada do sqlsrv e/ou pdo_sqlsrv pode ser instalada usando o sistema de pacotes PECL do PHP. 
  
**A versão 3.2 dos Drivers da Microsoft para PHP para SQL Server instala as seguintes versões do driver:**  
  
|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|não|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|sim|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|não|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|sim|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br /><br />php_pdo_sqlsrv_56_nts.dll|5.6|não|php5.dll|  
|php_sqlsrv_56_ts.dll<br /><br />php_pdo_sqlsrv_56_ts.dll|5.6|sim|php5ts.dll|  
  
**A versão 3.1 dos Drivers da Microsoft para PHP para SQL Server instala as seguintes versões do driver:**  
  
|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|não|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|sim|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|não|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|sim|php5ts.dll|  
  
**A versão 3.0 dos Drivers da Microsoft para PHP para SQL Server instala as seguintes versões do driver:**  
  
|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts.dll<br /><br />php_pdo_sqlsrv_53_nts.dll|5.3|não|php5.dll|  
|php_sqlsrv_53_ts.dll<br /><br />php_pdo_sqlsrv_53_ts.dll|5.3|sim|php5ts.dll|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|não|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|sim|php5ts.dll|  
  
**A versão 2.0 dos Drivers da Microsoft para PHP para SQL Server instala as seguintes versões do driver:**  
  
|Arquivo de driver|Versão do PHP|Thread-safe?|Usar com este .dll do PHP|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts_vc6.dll<br /><br />php_pdo_sqlsrv_53_nts_vc6.dll|5.3|não|php5.dll|  
|php_sqlsrv_53_nts_vc9.dll<br /><br />php_pdo_sqlsrv_53_nts_vc9.dll|5.3|não|php5.dll|  
|php_sqlsrv_53_ts_vc6.dll<br /><br />php_pdo_sqlsrv_53_ts_vc6.dll|5.3|sim|php5ts.dll|  
|php_sqlsrv_53_ts_vc9.dll<br /><br />php_pdo_sqlsrv_53_ts_vc9.dll|5.3|sim|php5ts.dll|  
|php_sqlsrv_52_nts_vc6.dll<br /><br />php_pdo_sqlsrv_52_nts_vc6.dll|5.2|não|php5.dll|  
|php_sqlsrv_52_ts_vc6.dll<br /><br />php_pdo_sqlsrv_52_ts_vc6.dll|5.2|sim|php5ts.dll|  
  
Se o nome do arquivo do driver contiver "vc9", ele deverá ser usado com uma versão do PHP compilada com Visual C++ 9.0.  
## <a name="operating-systems"></a>Sistemas operacionais 
Sistemas operacionais com suporte para as versões do driver são da seguinte maneira:

-   4.3:
    -   Windows Server 2012  
    -   Windows Server 2012 R2
    -   Windows Server 2016 
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10
    -   Ubuntu 15.10 (64 bits)
    -   Ubuntu 16.04 (64 bits)
    -   Debian 8 (64 bits)
    -   Red Hat Enterprise Linux 7 (64 bits)
    -   Mac OS Serra (64 bits)
    -   Mac OS El Capitan (64 bits)
    
-   4.0:  
    -   Windows Server 2008 SP2
    -   Windows Server 2008 R2 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows Vista SP2  
    -   Windows 7 SP1  
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10 
    -   Ubuntu 15.04 (64 bits)
    -   Ubuntu 16.04 (64 bits)
    -   Red Hat Enterprise Linux 7 (64 bits)

 
-   3.2 e 3.1:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows 8  
    -   Windows 8.1  
  
  
-   3.0:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  


-   2.0:
    -   [!INCLUDE[winxpsvr](../../includes/winxpsvr_md.md)] Service Pack 1  
    -   Windows XP Service Pack 3  
    -   Windows Vista Service Pack 1 ou posterior  
    -   Windows Server 2008  
    -   Windows Server 2008 R2  
    -   Windows 7  
  
## <a name="see-also"></a>Consulte também  
[Introdução ao driver SQL de PHP](../../connect/php/getting-started-with-the-php-sql-driver.md)
[Guia de programação para o driver SQL de PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  

