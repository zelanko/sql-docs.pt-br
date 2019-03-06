---
title: Notas sobre a versão para os Microsoft Drivers para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c2e7377b1072c30e5c5ef038b93a88f0c222260
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744346"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Notas de versão dos Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página discute o que foi adicionado em cada versão do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

## <a name="whats-new-in-version-56"></a>Novidades da versão 5.6

- Suporte para PHP 7.3
- Suporte para o Microsoft ODBC Driver 17.3 em todas as plataformas
- Suporte para macOS Mojave (requer o ODBC Driver 17.3 ou superior)
- Suporte para 18.10 Ubuntu e Suse Linux 15 (ambos requerem que o ODBC Driver 17.3 ou superior)
- Retirada do suporte ao PHP 7.0
- Removido o suporte para Linux Ubuntu 17.10 e macOS El Capitan
- Suporte para o Token de acesso do AD do Azure (no Linux e macOS, requer o Driver ODBC 17.2 + e unixODBC 2.3.6+)
- Suporte para autenticação com o Azure AD usando a identidade gerenciado para recursos do Azure (exige o ODBC Driver 17.3 +)
- Novas funcionalidades de busca:
  - Novo sinalizador PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE para pdo_sqlsrv retornar a data e hora como objetos
  - Adicionar opção ReturnDatesAsStrings para o nível de instrução para sqlsrv
  - Novas opções nos níveis de conexão e instrução para ambos os drivers para a formatação de valores decimais nos resultados da buscados
- Suporte para a compilação estática dos drivers, se os usuários optarem por Compile da origem
- Melhorar o desempenho armazenando em cache os metadados em buscas e acelerando as conversões de cadeia de caracteres Unicode

## <a name="whats-new-in-version-53"></a>Novidades da versão 5.3

- Suporte para o Microsoft ODBC Driver 17.2 em todas as plataformas
- Suporte para macOS High Sierra (requer o ODBC Driver 17 e posterior)
- Para o Azure Key Vault para Always Encrypted básicas CRUD funcionalidades de tal que o recurso sempre criptografado está disponível a todos os suporte para plataformas Windows, Linux ou macOS [usando o Always Encrypted com os Drivers de PHP para SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
- Suporte do Ubuntu 18.04 LTS (requer o ODBC Driver 17.2)
- Suporte para resiliência de Conexão no Linux ou macOS também (requer o ODBC Driver 17.2)

## <a name="whats-new-in-version-52"></a>Novidades da versão 5.2

- Suporte para PHP 7.2.1 e até em Windows e 7.2.0 e até em outras plataformas
- Suporte do Microsoft ODBC Driver 17
  - Versão 17 agora é o padrão em todas as plataformas
- Suporte para Ubuntu 17.10, Debian 9 e Enterprise do Suse Linux 12
- Retirada do suporte ao Ubuntu 15.10
- Suporte para Always Encrypted com funcionalidades CRUD no Windows. Para obter mais informações, consulte [usando o Always Encrypted com os Drivers de PHP para SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
  - Suporte para a Windows Store de certificado
  - Always Encrypted só tem suporte com o Microsoft ODBC Driver 17 e acima
- Suporte para localidades não UTF8 no Linux e macOS
  - Localidades de não-UTF8 no Linux e macOS só têm suporte com o Microsoft ODBC Driver 17 e acima
- Suporte para o SQL Data Warehouse do Azure
- Suporte para a instância gerenciada do SQL do Azure (versão prévia privada estendida)


## <a name="whats-new-in-version-43"></a>Novidades da versão 4.3

- Suporte para PHP 7.1
- Suporte para macOS Sierra e macOS El Capitan
- Suporte para Ubuntu 15.10 e Debian 8
- Retirada do suporte ao Ubuntu 15.04
- Suporte para grupos de disponibilidade AlwaysOn por meio da resolução de IP de rede transparente. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).
- Adicionado suporte para o tipo de dados sql_variant com limitação.
- Suporte a resiliência de Conexão ocioso no Windows. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).
- Suporte para Linux e macOS de pooling de Conexão. Para obter mais informações, confira [Pooling de conexão](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).
- Suporte para autenticação do Azure Active Directory com o ActiveDirectoryPassword e SqlPassword. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).

## <a name="whats-new-in-version-40"></a>Novidades da versão 4.0

- Suporte para PHP 7.0  
- Suporte total a 64 bits
- Suporte para Ubuntu 15.04, Ubuntu 16.04 e RedHat 7

## <a name="whats-new-in-version-32"></a>Novidades da versão 3.2

- Suporte para PHP 5.6   
- Inclui as atualizações mais recentes para versões anteriores do PHP 5.5 e 5.4   
- Exige o Microsoft ODBC Driver 11 for SQL Server  

## <a name="whats-new-in-version-31"></a>Novidades da versão 3.1

- Suporte para PHP 5.5  
- Exige o Microsoft ODBC Driver 11 for SQL Server. As versões anteriores exigem o SQL Native Client.  

## <a name="whats-new-in-version-30"></a>Novidades da versão 3.0  

- Suporte para PHP 5.4.  O PHP 5.2 não tem suporte na versão 3 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
- A opção de conexão AttachDBFileName é adicionada. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).  
- Suporte para o LocalDB, adicionado no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Para obter mais informações, consulte [suporte para o LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).
- A opção de conexão AttachDBFileName é adicionada. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).  
- Suporte para recursos de alta disponibilidade e recuperação de desastres. Para obter mais informações, consulte [suporte para alta disponibilidade, recuperação de desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).
- Suporte para cursores do lado do cliente (armazenando em cache um conjunto de resultados na memória). Para obter mais informações, confira [Tipos de cursor &#40;Driver SQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md) e [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- O atributo PDO::ATTR_EMULATE_PREPARES foi adicionado. Para obter mais informações, confira [PDO::prepare](../../connect/php/pdo-prepare.md).  

## <a name="whats-new-in-version-20"></a>Novidades da versão 2.0  
Na versão 2.0, foi adicionado suporte para o driver PDO_SQLSRV. Para obter mais informações, consulte [Referência do driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md).  

## <a name="see-also"></a>Consulte Também  
[Visão geral dos Microsoft Drivers for PHP for SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
