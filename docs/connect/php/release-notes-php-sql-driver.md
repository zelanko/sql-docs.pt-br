---
title: Notas sobre a versão para os Microsoft Drivers para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-dapugl, kenvh
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23ac53a8515f55dfc0cad282fd14294e5f285af9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935913"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Notas de versão dos Microsoft Drivers for PHP for SQL Server

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página discute o que foi adicionado em cada versão do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

<!--
Hello, We are standardizing the format of content inside our Release Notes (or What's New) articles.
Instead of bullets (or paragraphs), we have shifted to the 2-column format you see for H2 **What's New in Version 5.6**.
It is not necessary to reformat all the older H2 sections in this Release Notes file, but.....

Going forward, please be sure to use the 2-column format.

Also, all Release Notes .md file names now must begin with 'release-notes-*.md'.  And no filler words.
The 5.6 edition of this file is being renamed.....
FROM:  'release-notes-for-the-php-sql-driver.md'
TO  :  'release-notes-php-sql-driver.md'

For any questions, ask GeneMi or CraigG.
Thanks a lot.  2019-03-28  (DevO= 1467988)
-->

## <a name="whats-new-in-version-56"></a>Novidades da versão 5.6

| Novo item | Detalhes |
| :------- | :------ |
| Suporte para PHP 7.3. | &nbsp; |
| Cancelado suporte para PHP 7,0. | &nbsp; |
| Suporte para o Microsoft ODBC Driver 17,3 em todas as plataformas. | &nbsp; |
| Suporte para macOS Mojave. | Requer o driver ODBC 17,3 ou superior. |
| Suporte para Ubuntu 18,10 e SuSE Linux 15. | Ambos exigem o driver ODBC 17,3 ou superior. |
| Descartado o suporte para Linux Ubuntu 17,10 e macOS El Capitan. | &nbsp; |
| Suporte para token de acesso do Azure AD. | No Linux e no macOS, o requer o driver ODBC 17.2 + e unixODBC 2.3.6 +. |
| Suporte para autenticação com o Azure AD usando a identidade gerenciada para recursos do Azure. | Requer o driver ODBC 17.3 +. |
| Novas funcionalidades de busca | &bull;&nbsp; Novo sinalizador PDO:: SQLSRV_ATTR_FETCHES_DATETIME_TYPE para pdo_sqlsrv retornar DateTime como objetos.<br/><br/>&bull;&nbsp; Adicione a opção ReturnDatesAsStrings ao nível de instrução para sqlsrv.<br/><br/>&bull;&nbsp; Novas opções nos níveis de conexão e de instrução para ambos os drivers para formatação de valores decimais nos resultados obtidos. |
| Suporte para compilação estática de drivers se os usuários optarem por criar a partir da origem. | &nbsp; |
| Desempenho aprimorado armazenando em cache metadados em buscas e acelerando conversões de cadeias de caracteres Unicode. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="whats-new-in-version-53"></a>Novidades da versão 5.3

- Suporte para o Microsoft ODBC Driver 17,2 em todas as plataformas
- Suporte para macOS High Sierra (requer o driver ODBC 17 e superior)
- Suporte para Azure Key Vault para Always Encrypted para funcionalidades básicas de CRUD, de forma que Always Encrypted recurso esteja disponível para todas as plataformas Windows, Linux ou macOS com suporte [usando Always Encrypted com os drivers php para SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
- Suporte para Ubuntu 18, 4 LTS (requer o driver ODBC 17,2)
- Suporte para resiliência de conexão no Linux ou macOS também (requer o driver ODBC 17,2)

## <a name="whats-new-in-version-52"></a>Novidades da versão 5.2

- Suporte para PHP 7.2.1 e up no Windows e 7.2.0 e em outras plataformas
- Suporte para o Microsoft ODBC Driver 17
  - A versão 17 agora é o padrão em todas as plataformas
- Suporte para Ubuntu 17,10, Debian 9 e SuSE Enterprise Linux 12
- Cancelado suporte para Ubuntu 15,10
- Suporte para Always Encrypted com funcionalidades CRUD no Windows. Para saber mais, confira [Como usar Always Encrypted com o PHP Drivers para SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
  - Suporte para o repositório de certificados do Windows
  - Só há suporte para Always Encrypted com o Microsoft ODBC Driver 17 e posterior
- Suporte para localidades não UTF8 no Linux e no macOS
  - As localidades não UTF8 no Linux e no macOS só têm suporte com o Microsoft ODBC Driver 17 e posterior
- Suporte para o SQL Data Warehouse do Azure
- Suporte para a Instância Gerenciada do SQL do Azure (Versão prévia privada estendida)

## <a name="whats-new-in-version-43"></a>Novidades da versão 4.3

- Suporte para PHP 7.1
- Suporte para macOS Sierra e macOS El Capitan
- Suporte para Ubuntu 15,10 e Debian 8
- Cancelado suporte para Ubuntu 15, 4
- Suporte para grupos de disponibilidade Always On por meio da resolução de IP de rede transparente. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).
- Adicionado suporte para tipo de dados sql_variant com limitação.
- Suporte à resiliência de conexão ociosa no Windows. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).
- Suporte a pooling de conexão para Linux e macOS. Para obter mais informações, confira [Pooling de conexão](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).
- Suporte para autenticação de Azure Active Directory com ActiveDirectoryPassword e SQLPassword. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).

## <a name="whats-new-in-version-40"></a>Novidades da versão 4.0

- Suporte para PHP 7.0  
- Suporte completo a 64 bits
- Suporte para Ubuntu 15, 4, Ubuntu 16, 4 e RedHat 7

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
- Suporte para o LocalDB, adicionado no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Para obter mais informações, consulte [suporte para LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).
- A opção de conexão AttachDBFileName é adicionada. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).  
- Suporte para recursos de alta disponibilidade e recuperação de desastres. Para saber mais, confira [Suporte para alta disponibilidade, recuperação de desastre](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).
- Suporte para cursores do lado do cliente (armazenando em cache um conjunto de resultados na memória). Para obter mais informações, confira [Tipos de cursor &#40;Driver SQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md) e [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- O atributo PDO::ATTR_EMULATE_PREPARES foi adicionado. Para obter mais informações, confira [PDO::prepare](../../connect/php/pdo-prepare.md).  

## <a name="whats-new-in-version-20"></a>Novidades da versão 2.0

Na versão 2.0, foi adicionado suporte para o driver PDO_SQLSRV. Para obter mais informações, consulte [Referência do driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md).  

## <a name="see-also"></a>Consulte Também

[Visão geral dos Microsoft Drivers for PHP for SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
