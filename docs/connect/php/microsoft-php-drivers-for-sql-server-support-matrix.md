---
title: Matriz de suporte dos Microsoft Drivers for PHP
description: Esta página contém a matriz de suporte e a política de ciclo de vida de suporte para os Microsoft PHP Drivers for SQL Server.
ms.custom: ''
ms.date: 04/15/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
manager: ''
ms.openlocfilehash: 82d394cd3c940de43f8b9706b719515ed45d97a4
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632749"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Matriz de Suporte do Microsoft PHP Drivers para SQL Server

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página contém a matriz de suporte e a política de ciclo de vida de suporte para os Microsoft PHP Drivers for SQL Server.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Política e matriz de ciclo de vida de suporte do Microsoft PHP Drivers

A política de ciclo de vida de suporte da Microsoft (MSL) fornece informações transparentes e previsíveis sobre o ciclo de vida de suporte dos produtos da Microsoft. As versões de driver PHP 3.x, 4.x e 5.x têm cinco anos de suporte base a partir da data de lançamento do driver. O suporte base é definido no [site do ciclo de vida de suporte da Microsoft](https://support.microsoft.com/lifecycle).

As opções de suporte personalizado e estendido não estão disponíveis para os Microsoft PHP Drivers.

Há suporte para os Microsoft PHP Drivers a seguir até a data de Fim do Suporte indicada.

|Nome do driver|Versão do pacote de driver|Fim do Suporte Base|
|-|:-:|-|
|Microsoft PHP Drivers 5.8 para SQL Server|5.8|31 de janeiro de 2025|
|Microsoft PHP Drivers 5.6 para SQL Server|5.6|21 de fevereiro de 2024|
|Microsoft PHP Drivers 5.3 para SQL Server|5,3|20 de julho de 2023|
|Microsoft PHP Drivers 5.2 para SQL Server|5.2|9 de fevereiro de 2023|
|Microsoft PHP Drivers 4.3 para SQL Server|4.3|6 de julho de 2022|
|Microsoft PHP Drivers 4.0 para SQL Server|4,0|11 de julho de 2021|
|Microsoft PHP Drivers 3.2 para SQL Server|3.2|9 de março de 2020|
| &nbsp; | &nbsp; | &nbsp; |

Não há mais suporte para os Microsoft PHP Drivers a seguir.

|Nome do driver|Versão do pacote de driver|Fim do Suporte Base|
|-|:-:|-|
|Microsoft PHP Drivers 3.1 para SQL Server|3.1|12 de dezembro de 2019|
|Microsoft PHP Drivers 3.0 para SQL Server|3.0|6 de março de 2017|
|Microsoft PHP Drivers 2.0 para SQL Server|2,0|10 de agosto de 2015|
|Microsoft PHP Drivers 1.0 para SQL Server|1.0|28 de abril de 2014|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="sql-server-version-certified-compatibility"></a>Compatibilidade certificada com a versão do SQL Server
 A matriz a seguir lista as versões do SQL Server que foram testadas e certificadas como compatíveis com a versão do driver correspondente. Nós nos esforçamos para manter a compatibilidade com as versões anteriores do driver, mas apenas o driver com suporte mais recente é testado e certificado com as novas versões do SQL Server, à medida que o SQL Server é lançado.

|PHP para a versão &#8594; do driver do SQL Server<br />&#8595; Versão do SQL Server|5.8|5.6|5,3|5.2|4.3|4,0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Instância Gerenciada do Azure SQL|S|S|S|S|S| | |
|SQL Data Warehouse do Azure|S|S|S|S|S| | |
|SQL Server 2019         |S| | | | | | |
|Microsoft SQL Server 2017         |S|S|S|S|S| | |
|SQL Server 2016         |S|S|S|S|S|S| |
|SQL Server 2014         |S|S|S|S|S|S|S|
|SQL Server 2012         |S|S|S|S|S|S|S|
|SQL Server 2008 R2      | |S|S|S|S|S|S|
|SQL Server 2008         | | | | | |S|S|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="php-version-support"></a>Suporte à versão do PHP

As seguintes versões do PHP são compatíveis com a versão listada do Microsoft PHP Drivers:

|PHP para a versão &#8594; do driver do SQL Server<br />&#8595; Versão do PHP|5.8|5.6|5,3|5.2|4.3|4,0|3.2|
|:---:|---|---|---|---|---|---|---|
|7.4|7.4.0+          |                |                |                |       |        |        |
|7.3|7.3.0+          |7.3.0+          |                |                |       |        |        |
|7.2|7.2 +<sup>1</sup>|7.2 +<sup>1</sup>|7.2 +<sup>1</sup>|7.2 +<sup>1</sup>|       |        |        |
|7.1|                |7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |        |        |
|7.0|                |                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+  |        |
|5.6|                |                |                |                |       |        |5.6.4+  |
|5.5|                |                |                |                |       |        |5.5.16+ |
|5.4|                |                |                |                |       |        |5.4.32  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. As versões 7.2.1 e posteriores têm suporte no Windows, enquanto as versões 7.2.0 e posteriores têm suporte no Linux e no macOS.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

As versões a seguir do sistema operacional Windows são compatíveis com a versão listada do Microsoft PHP Drivers:

|PHP para a versão &#8594; do driver do SQL Server<br />&#8595; Sistema operacional|5.8|5.6|5,3|5.2|4.3|4,0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2019                 |S  |S  |   |   |   |   |   |
|Windows Server 2016                 |S  |S  |S  |S  |S  |   |   |
|Windows Server 2012 R2              |S  |S  |S  |S  |S  |S  |S  |
|Windows Server 2012                 |S  |S  |S  |S  |S  |S  |S  |
|Windows Server 2008 R2 SP1          |   |   |   |   |   |S  |S  |
|Windows Server 2008 R2              |   |   |   |   |   |   |   |
|Windows Server 2008 SP2             |   |   |   |   |   |S  |S  |
|Windows 10                          |S  |S  |S  |S  |S  |S  |   |
|Windows 8.1                         |S  |S  |S  |S  |S  |S  |S  |
|Windows 8                           |   |   |   |   |S  |S  |S  |
|Windows 7 SP1                       |   |   |   |   |   |S  |S  |
|Windows Vista SP2                   |   |   |   |   |   |S  |S  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

As seguintes versões dos sistemas operacionais Linux e macOS (somente 64 bit) são compatíveis com a versão listada do Microsoft PHP Drivers:

|Versão do driver PHP para SQL Server &#8594;<br />&#8595; Sistema operacional|5.8|5.6|5,3|5.2|4.3|4,0|3.2|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 19.10 (64 bits)               |S  |   |   |   |   |   |   |
|Ubuntu 18.10 (64 bits)               |   |S  |   |   |   |   |   |
|Ubuntu 18.04 (64 bits)               |S  |S  |S  |   |   |   |   |
|Ubuntu 17.10 (64 bits)               |   |   |S  |S  |   |   |   |
|Ubuntu 16.04 (64 bits)               |S  |S  |S  |S  |S  |S  |   |
|Ubuntu 15.10 (64 bits)               |   |   |   |   |S  |   |   |
|Ubuntu 15.04 (64 bits)               |   |   |   |   |   |S  |   |
|Debian 10 (64 bits)                  |S  |   |   |   |   |   |   |
|Debian 9 (64 bits)                   |S  |S  |S  |S  |   |   |   |
|Debian 8 (64 bits)                   |S  |S  |S  |S  |S  |   |   |
|Red Hat Enterprise Linux 8 (64 bits) |S  |   |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 bits) |S  |S  |S  |S  |S  |S  |   |
|Suse Enterprise Linux 15 (64 bits)   |S  |S  |   |   |   |   |   |
|Suse Enterprise Linux 12 (64 bits)   |S  |S  |S  |S  |   |   |   |
|Alpine Linux 3.11 (64 bits)<sup>1</sup>|S  |   |   |   |   |   |   |
|macOS Catalina (64 bits)             |S  |   |   |   |   |   |   |
|macOS Mojave (64 bits)               |S  |S  |   |   |   |   |   |
|macOS High Sierra (64 bits)          |S  |S  |S  |   |   |   |   |
|macOS Sierra (64 bits)               |   |S  |S  |S  |S  |   |   |
|macOS El Capitan (64 bits)           |   |   |S  |S  |S  |   |   |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> O suporte ao Alpine Linux é experimental na versão 5.8.0. A versão 5.8.1 introduz o suporte de produção.

## <a name="see-also"></a>Consulte Também

[Notas de Versão](release-notes-php-sql-driver.md)

[Recursos de suporte](support-resources-for-the-php-sql-driver.md)

[Requisitos do sistema](system-requirements-for-the-php-sql-driver.md)
