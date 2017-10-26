---
title: "Notas de versão do Driver SQL de PHP | Microsoft Docs"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2c63079bda91844995540aade94bac397be6b94c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="release-notes-for-the-php-sql-driver"></a>Notas de versão do driver SQL do PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico discute o que foi adicionado em cada versão do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

## <a name="whats-new-in-version-43"></a>Novidades na versão 4.3

- Suporte para PHP 7.1
- Suporte para Mac OS Serra e Mac OS El Capitan
- Suporte para Ubuntu 15.10 e 8 Debian
- Suporte removido para Ubuntu 15.04
- Suporte para grupos de disponibilidade AlwaysOn, por meio da resolução de IP de rede transparente. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md). 
- Adicionado suporte para o tipo de dados sql_variant com limitação.
- Suporte para resiliência de Conexão ocioso no Windows. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).
- Suporte para Linux e macOS a pooling de Conexão. Para obter mais informações, consulte [Pooling de Conexão](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).
- Suporte para autenticação do Active Directory do Azure com ActiveDirectoryPassword e SqlPassword. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).
  
## <a name="whats-new-in-version-40"></a>Novidades na versão 4.0 

- Suporte para PHP 7.0  
- Suporte completo de 64 bits
- Suporte para Ubuntu 15.04, Ubuntu 16.04 e RedHat 7

## <a name="whats-new-in-version-32"></a>Novidades da versão 3.2 

- Suporte para PHP 5.6   
- Inclui as atualizações mais recentes para versões anteriores do PHP 5.5 e 5.4   
- Exige o Microsoft ODBC Driver 11 para SQL Server  
  
## <a name="whats-new-in-version-31"></a>Novidades da versão 3.1
 
- Suporte para PHP 5.5  
- Requer o Microsoft ODBC Driver 11 para SQL Server. As versões anteriores exigem o SQL Native Client.  
  
## <a name="whats-new-in-version-30"></a>Novidades da versão 3.0  

- Suporte para PHP 5.4.  O PHP 5.2 não tem suporte na versão 3 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
- A opção de conexão AttachDBFileName é adicionada. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).  
- Suporte para o LocalDB, adicionado no [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]. Para obter mais informações, consulte [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).
- A opção de conexão AttachDBFileName é adicionada. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).  
- Suporte para recursos de alta disponibilidade e recuperação de desastres. Para obter mais informações, consulte [PHP Driver for SQL Server Support for High Availability, Disaster Recovery](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)(Driver do PHP para o suporte do SQL Server para alta disponibilidade e recuperação de desastre).
- Suporte para cursores do lado do cliente (armazenando em cache um conjunto de resultados na memória). Para obter mais informações, consulte [tipos de Cursor &#40; Driver SQLSRV &#41; ](../../connect/php/cursor-types-sqlsrv-driver.md) e [tipos de Cursor &#40; Driver PDO_SQLSRV &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- O atributo PDO::ATTR_EMULATE_PREPARES foi adicionado. Para obter mais informações, consulte [PDO](../../connect/php/pdo-prepare.md).  
  
## <a name="whats-new-in-version-20"></a>Novidades da versão 2.0  
Na versão 2.0, foi adicionado suporte para o driver PDO_SQLSRV. Para obter mais informações, consulte [Referência do driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md).  
  
## <a name="see-also"></a>Consulte também  
[Visão geral do driver SQL de PHP](../../connect/php/overview-of-the-php-sql-driver.md)
  

