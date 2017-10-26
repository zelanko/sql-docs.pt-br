---
title: "Visão geral do Driver SQL de PHP | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 66559249-34c0-409d-b919-9b5bf0c4c9ec
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4badc426f6dbff44784bd8487b04bc0665d959ad
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="overview-of-the-php-sql-driver"></a>Visão geral do driver SQL de PHP

![Um círculo seta download](../../ssdt/media/download.png)[para baixar o driver do PHP para SQL Server](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] é uma extensão do PHP que fornece acesso a dados do SQL Server 2005 e versões posteriores, incluindo o banco de dados do SQL Azure. A extensão fornece uma interface de procedimento (o driver SQLSRV) e uma interface orientada a objeto (o driver PDO_SQLSRV) para acessar dados em todas as versões (inclusive a versão Express) começando com o SQL Server 2005 (suporte para PHP para SQL Server versões 3.1 e posteriores começa com o SQL Server 2008). A API do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] inclui suporte para Autenticação do Windows, transações, associação de parâmetros, streaming, acesso a metadados e tratamento de erro.  
  
Para usar o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] deve ter a versão correta do SQL Server Native Client ou Microsoft ODBC Driver instalado no mesmo computador do PHP está em execução.  Para obter mais informações, consulte [Requisitos de sistema para o driver SQL do PHP](../../connect/php/system-requirements-for-the-php-sql-driver.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|---------|---------------|  
| ![Um círculo seta download](../../ssdt/media/download.png)[para baixar o driver do PHP para SQL Server](../sql-connection-libraries.md#anchor-20-drivers-relational-access) | Links para baixar drivers e código-fonte para o Microsoft PHP Driver for SQL Server. |
|[Notas de versão do driver SQL do PHP](../../connect/php/release-notes-for-the-php-sql-driver.md)|Lista os recursos que foram adicionados para as versões 4.0, 3.2, 3.1, 3.0 e 2.0.|  
|[Recursos de suporte para o driver SQL do PHP](../../connect/php/support-resources-for-the-php-sql-driver.md)|Fornece links para recursos que podem ser úteis ao desenvolver aplicativos que usam o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].|  
|[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)|Fornece informações que podem ser úteis quando você executar os exemplos de código desta documentação.|  
  
## <a name="reference"></a>Referência  
[Referência da API do driver JDBC](../../connect/php/sqlsrv-driver-api-reference.md)  
[Referência do driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
[Introdução ao Driver SQL de PHP](../../connect/php/getting-started-with-the-php-sql-driver.md)
[guia de programação para o Driver SQL de PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[aplicativo de exemplo &#40; Driver SQLSRV &#41;](../../connect/php/example-application-sqlsrv-driver.md)

