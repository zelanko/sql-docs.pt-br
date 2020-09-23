---
title: Visão geral dos Microsoft Drivers para PHP para SQL Server
description: Conheça uma visão geral dos Drivers Microsoft SQLSRV e PDO_SQSRV para PHP para SQL Server e como usá-los em um aplicativo PHP para acesso ao banco de dados.
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 66559249-34c0-409d-b919-9b5bf0c4c9ec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 556d13a5b29a53b323b41bc9b697d7ad934ca143
ms.sourcegitcommit: f7c9e562d6048f89d203d71685ba86f127d8d241
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/12/2020
ms.locfileid: "90042777"
---
# <a name="overview-of-the-microsoft-drivers-for-php-for-sql-server"></a>Visão geral dos Microsoft Drivers para PHP para SQL Server

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] é uma extensão do PHP que fornece acesso a dados ao SQL Server 2005 e versões posteriores, incluindo o Banco de Dados SQL do Azure. A extensão fornece uma interface de procedimento com o driver SQLSRV e uma interface orientada a objeto com o driver PDO_SQLSRV para acessar dados em todas as versões do SQL Server, incluindo o Express, que começa com o SQL Server 2005. O suporte para as versões 3.1 e posteriores dos drivers começa com o SQL Server 2008. A API do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] inclui suporte para Autenticação do Windows, transações, associação de parâmetros, streaming, acesso a metadados e tratamento de erro.  
  
Para usar o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], você deve ter a versão correta do SQL Server Native Client ou do Microsoft ODBC Driver instalada no mesmo computador que o PHP está em execução.  Para obter mais informações, confira [Requisitos do sistema para os drivers da Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|---------|---------------|  
| ![Download-DownArrow-Circled](../../ssms/media/download-icon.png)[Para baixar os drivers para PHP para SQL Server](download-drivers-php-sql-server.md) | Links para baixar os Microsoft Drivers para PHP para SQL Server. |
|[Notas de versão dos Microsoft Drivers for PHP for SQL Server](../../connect/php/release-notes-php-sql-driver.md)|Lista os recursos que foram adicionados às versões 4.0, 3.2, 3.1, 3.0 e 2.0.|  
|[Recursos de suporte para os drivers da Microsoft para PHP para SQL Server](../../connect/php/support-resources-for-the-php-sql-driver.md)|Fornece links para recursos que podem ser úteis ao desenvolver aplicativos que usam o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].|  
|[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)|Fornece informações que podem ser úteis quando você executar os exemplos de código desta documentação.|  
| &nbsp; | &nbsp; |

## <a name="reference"></a>Referência

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Referência do driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

## <a name="see-also"></a>Consulte Também

[Introdução aos Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)  
[Guia de programação do Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)  
[Aplicativo de exemplo &#40;driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
