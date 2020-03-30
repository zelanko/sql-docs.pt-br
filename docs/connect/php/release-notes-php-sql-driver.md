---
title: Notas sobre a versão para os Microsoft Drivers para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/05/2020
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
ms.openlocfilehash: 30b4b646beda19bb36eb4e046fce86379f9242df
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80345422"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Notas de versão dos Microsoft Drivers for PHP for SQL Server

Esta página aborda o que foi adicionado em cada versão do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

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

## <a name="58"></a>5.8

![baixar](../../ssms/media/download-icon.png) [Baixar pacote do Windows](https://go.microsoft.com/fwlink/?linkid=2120362)  
[Tag de versão do GitHub (pacotes para Linux e macOS estão disponíveis aqui)](https://github.com/Microsoft/msphpsql/releases/tag/v5.8.0)

### <a name="version-information"></a>Informações da versão

- Número da versão: 5.8.0
- Lançado: 31 de janeiro de 2020

## <a name="whats-new-in-58"></a>Novidades na versão 5.8

| Novo item | Detalhes |
| :------- | :------ |
| Suporte adicionado para PHP 7.4. | &nbsp; |
| Suporte removido para PHP 7.1. | &nbsp; |
| Suporte adicionado para Microsoft ODBC Driver 17.5 em todas as plataformas. | &nbsp; |
| Suporte adicionado para Debian 10 e Red Hat 8. | Ambos exigem um Driver ODBC 17.4 ou superior. |
| Suporte adicionado para macOS Catalina, Alpine Linux 3.11<sup>1</sup> e Ubuntu 19.10. | Todos exigem um Driver ODBC 17.5 ou superior. |
| Suporte removido para SQL Server 2008 R2, macOS Sierra, Ubuntu 18.10 e Ubuntu 19.04. | &nbsp; |
| Suporte para opção de idioma durante a conexão com o SQL Server. | &nbsp; |
| Suporte para tipos de cadeia de caracteres estendidos do PHP introduzidos no PHP 7.2. | &nbsp; |
| Suporte para recuperação de metadados confidenciais da Classificação de Dados. | Requer SQL Server 2019 e o Driver ODBC 17.4.2 ou superior. |
| Suporte para Always Encrypted com enclaves seguros. | Requer o Driver ODBC 17.4 ou superior. |
| Opções configuráveis de suporte para configurações de localidade no Linux e no macOS. |
| Desempenho aprimorado ao armazenar metadados em cache nas buscas e omitir chamadas redundantes. | &nbsp; |
| &nbsp; | &nbsp; |

<sup>1</sup> O suporte ao Alpine Linux é experimental na versão 5.8.

## <a name="previous-releases"></a>Versões anteriores

## <a name="561"></a>5.6.1

![baixar](../../ssms/media/download-icon.png) [Baixar pacote do Windows](https://go.microsoft.com/fwlink/?linkid=2120446)  
[Tag de versão do GitHub (pacotes para Linux e macOS estão disponíveis aqui)](https://github.com/Microsoft/msphpsql/releases/tag/v5.6.1)

### <a name="version-information"></a>Informações da versão

- Número da versão: 5.6.1
- Lançado: 19 de março de 2019

## <a name="whats-new-in-561"></a>Novidades na versão 5.6.1

| Novo item | Detalhes |
| :------- | :------ |
| Correção de bug | Corrigidas as suposições feitas ao calcular os metadados de campo ou coluna que podem ter resultado no encerramento do aplicativo. |
| Correção de bug | Modificado o arquivo de configuração sqlsrv de forma a permitir que seja compilado de modo independente do pdo_sqlsrv. |
| Correção de bug | Corrigido o PDOStatement::getColumnMeta() para retornar como false quando algo errado ocorre. |
| &nbsp; | &nbsp; |

## <a name="56"></a>5.6

![baixar](../../ssms/media/download-icon.png) [Baixar pacote do Windows](https://go.microsoft.com/fwlink/?linkid=2120450)  
[Tag de versão do GitHub (pacotes para Linux e macOS estão disponíveis aqui)](https://github.com/Microsoft/msphpsql/releases/tag/v5.6.0)

### <a name="version-information"></a>Informações da versão

- Número da versão: 5.6.0
- Lançado: 21 de fevereiro de 2019

## <a name="whats-new-in-56"></a>Novidades na versão 5.6

| Novo item | Detalhes |
| :------- | :------ |
| Suporte para PHP 7.3. | &nbsp; |
| Suporte removido para PHP 7.0. | &nbsp; |
| Suporte para Microsoft ODBC Driver 17.3 em todas as plataformas. | &nbsp; |
| Suporte para macOS Mojave. | Requer o Driver ODBC 17.3 ou superior. |
| Suporte para Ubuntu 18.10 e Suse Linux 15. | Ambos exigem um Driver ODBC 17.3 ou superior. |
| Suporte removido para Linux Ubuntu 17.10 e macOS El Capitan. | &nbsp; |
| Suporte a token de acesso do Azure AD. | No Linux e no macOS, requer o Driver ODBC 17.2+ e unixODBC 2.3.6+. |
| Suporte para Autenticação com Azure AD usando Identidade Gerenciada para Recursos do Azure. | Requer o Driver ODBC 17.3+. |
| Novas funcionalidades de busca | &bull; &nbsp; Novo sinalizador PDO:: SQLSRV_ATTR_FETCHES_DATETIME_TYPE para pdo_sqlsrv retornar datetime como objetos.<br/><br/>&bull; &nbsp; Adicione a opção ReturnDatesAsStrings ao nível da instrução para sqlsrv.<br/><br/>&bull; &nbsp; Novas opções nos níveis de conexão e de instrução para os dois drivers para formatação de valores decimais nos resultados obtidos. |
| Suporte para compilação estática de drivers, caso os usuários optem por compilar da origem. | &nbsp; |
| Desempenho aprimorado ao armazenar metadados em cache nas buscas e acelerar as conversões de cadeias de caracteres Unicode. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="53"></a>5,3

![baixar](../../ssms/media/download-icon.png) [Baixar pacote do Windows](https://go.microsoft.com/fwlink/?linkid=2120447)  
[Tag de versão do GitHub (pacotes para Linux e macOS estão disponíveis aqui)](https://github.com/Microsoft/msphpsql/releases/tag/v5.3.0)

### <a name="version-information"></a>Informações da versão

- Número da versão: 5.3.0
- Lançado: 20 de julho de 2018

## <a name="whats-new-in-53"></a>Novidades na versão 5.3

- Suporte para Microsoft ODBC Driver 17.2 em todas as plataformas
- Suporte para macOS High Sierra (requer o Driver ODBC 17 e superior)
- Suporte para Azure Key Vault e para Always Encrypted para funcionalidades básicas de CRUD, de maneira que o recurso Always Encrypted esteja disponível em todas as plataformas compatíveis com Windows, Linux ou macOS. [Como usar o Always Encrypted com os Drivers PHP para SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
- Suporte para Ubuntu 18.04 LTS (requer o Driver ODBC 17.2)
- Suporte para resiliência da conexão no Linux ou no macOS (requer o Driver ODBC 17.2)

## <a name="52"></a>5.2

![baixar](../../ssms/media/download-icon.png) [Baixar pacote do Windows](https://go.microsoft.com/fwlink/?linkid=2120451)  
[Tag de versão do GitHub (pacotes para Linux e macOS estão disponíveis aqui)](https://github.com/Microsoft/msphpsql/releases/tag/v5.2.0)

### <a name="version-information"></a>Informações da versão

- Número da versão: 5.2.0
- Lançado: 23 de março de 2018

## <a name="whats-new-in-52"></a>Novidades na versão 5.2

- Suporte para PHP 7.2.1 e superior no Windows, além do 7.2.0 e superior em outras plataformas
- Suporte para Microsoft ODBC Driver 17
  - A versão 17 agora é padrão em todas as plataformas
- Suporte para Ubuntu 17.10, Debian 9 e Suse Enterprise Linux 12
- Suporte removido para Ubuntu 15.10
- Suporte para Always Encrypted com funcionalidades CRUD no Windows. Para saber mais, confira [Como usar Always Encrypted com o PHP Drivers para SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
  - Suporte para Repositório de Certificados do Windows
  - O Always Encrypted é compatível somente com o Microsoft ODBC Driver 17 e posterior
- Suporte para localidades não UTF8 no Linux e no macOS
  - As localidades não UTF8 no Linux e no macOS são compatíveis somente com o Microsoft ODBC Driver 17 e posterior
- Suporte para o SQL Data Warehouse do Azure
- Suporte para a Instância Gerenciada SQL do Azure

## <a name="43"></a>4.3

![baixar](../../ssms/media/download-icon.png) [Baixar pacote do Windows](https://go.microsoft.com/fwlink/?linkid=2120616)  
[Tag de versão do GitHub (pacotes para Linux e macOS estão disponíveis aqui)](https://github.com/Microsoft/msphpsql/releases/tag/v4.3.0)

### <a name="version-information"></a>Informações da versão

- Número da versão: 4.3.0
- Lançado: 6 de julho de 2017

## <a name="whats-new-in-43"></a>Novidades na versão 4.3

- Suporte para PHP 7.1
- Suporte para macOS Sierra e macOS El Capitan
- Suporte para Ubuntu 15.10 e Debian 8
- Suporte removido para Ubuntu 15.04
- Suporte a grupos de disponibilidade Always On por meio da Resolução IP de Rede Transparente. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).
- Suporte adicionado para o tipo de dados sql_variant com limitações.
- Suporte para Resiliência de Conexão Ociosa no Windows. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).
- Suporte ao pool de conexão para Linux e macOS. Para obter mais informações, confira [Pooling de conexão](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).
- Suporte para Autenticação do Azure Active Directory com ActiveDirectoryPassword e SqlPassword. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).

## <a name="40"></a>4,0

![baixar](../../ssms/media/download-icon.png) [Baixar pacote do Windows](https://go.microsoft.com/fwlink/?linkid=2120448)  
[Tag de versão do GitHub (pacotes para Linux e macOS estão disponíveis aqui)](https://github.com/microsoft/msphpsql/releases/tag/v4.0-RTW)

### <a name="version-information"></a>Informações da versão

- Número da versão: 4,0
- Lançado: 1º de julho de 2016

## <a name="whats-new-in-40"></a>Novidades na versão 4.0

- Suporte para PHP 7.0  
- Suporte completo de 64 bits
- Suporte para Ubuntu 15.04, Ubuntu 16.04 e RedHat 7

## <a name="32"></a>3.2

![baixar](../../ssms/media/download-icon.png) [Baixar pacote do Windows](https://go.microsoft.com/fwlink/?linkid=2120449)  
[Tag de versão do GitHub (pacotes para Linux e macOS estão disponíveis aqui)](https://github.com/microsoft/msphpsql/releases/tag/v3.2.0.0)

### <a name="version-information"></a>Informações da versão

- Número da versão: 3.2
- Lançado: 9 de março de 2015

## <a name="whats-new-in-32"></a>Novidades na versão 3.2

- Suporte para PHP 5.6  
- Inclui as atualizações mais recentes para versões anteriores do PHP 5.5 e 5.4  
- Exige o Microsoft ODBC Driver 11 for SQL Server  

## <a name="31"></a>3.1

[Tag de versão do GitHub (pacotes para Linux e macOS estão disponíveis aqui)](https://github.com/microsoft/msphpsql/releases/tag/v3.1.0.0)

### <a name="version-information"></a>Informações da versão

- Número da versão: 3.1
- Lançado: 12 de dezembro de 2014

## <a name="whats-new-in-31"></a>Novidades na versão 3.1

- Suporte para PHP 5.5  
- Exige o Microsoft ODBC Driver 11 for SQL Server. As versões anteriores exigem o SQL Native Client.  

## <a name="whats-new-in-30"></a>Novidades na versão 3.0  

- Suporte para PHP 5.4.  O PHP 5.2 não tem suporte na versão 3 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
- A opção de conexão AttachDBFileName é adicionada. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).  
- Suporte para o LocalDB, adicionado no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Para obter mais informações, confira [Suporte para LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).
- A opção de conexão AttachDBFileName é adicionada. Para obter mais informações, consulte [Connection Options](../../connect/php/connection-options.md).  
- Suporte para recursos de alta disponibilidade e recuperação de desastres. Para saber mais, confira [Suporte para alta disponibilidade, recuperação de desastre](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).
- Suporte para cursores do lado do cliente (armazenando em cache um conjunto de resultados na memória). Para obter mais informações, confira [Tipos de cursor &#40;Driver SQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md) e [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- O atributo PDO::ATTR_EMULATE_PREPARES foi adicionado. Para obter mais informações, confira [PDO::prepare](../../connect/php/pdo-prepare.md).  

## <a name="whats-new-in-20"></a>Novidades na versão 2.0

Na versão 2.0, foi adicionado suporte para o driver PDO_SQLSRV. Para obter mais informações, consulte [Referência do driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md).  

## <a name="see-also"></a>Consulte Também

[Visão geral dos Microsoft Drivers for PHP for SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
