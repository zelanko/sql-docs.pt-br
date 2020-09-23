---
title: Matriz de suporte dos Microsoft Drivers for PHP
description: Esta página contém a matriz de suporte e a política de ciclo de vida de suporte para os Microsoft PHP Drivers for SQL Server.
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 778d9aa4ee666ba3719095508d5f5e28516f954d
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942145"
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
 A matriz a seguir lista as versões de banco de dados que foram testadas e certificadas como compatíveis com a versão do driver correspondente. Nós nos esforçamos para manter a compatibilidade com as versões anteriores do driver, mas apenas o driver com suporte mais recente é testado e certificado com as novas versões do SQL Server, à medida que o SQL Server é lançado.

|Versão do driver&nbsp;&#8594;<br />&#8595; Versão do banco de dados|5.8|5.6|5,3|5.2|4.3|4,0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Banco de Dados SQL do Azure        |Sim|Sim|Sim|Sim|Sim|   |   |
|Instância Gerenciada do Azure SQL|Sim|Sim|Sim|Sim|Sim|   |   |
|Azure Synapse Analytics   |Sim|Sim|Sim|Sim|Sim|   |   |
|SQL Server 2019           |Sim|   |   |   |   |   |   |
|Microsoft SQL Server 2017           |Sim|Sim|Sim|Sim|Sim|   |   |
|SQL Server 2016           |Sim|Sim|Sim|Sim|Sim|Sim|   |
|SQL Server 2014           |Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|SQL Server 2012           |Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|SQL Server 2008 R2        |   |Sim|Sim|Sim|Sim|Sim|Sim|
|SQL Server 2008           |   |   |   |   |   |Sim|Sim|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

Para obter informações sobre como usar o PHP com o Banco de Dados SQL do Microsoft Azure, confira [Como se conectar ao Banco de Dados SQL do Azure](connecting-to-microsoft-azure-sql-database.md).

## <a name="php-version-support"></a>Suporte à versão do PHP

As seguintes versões do PHP são compatíveis com a versão listada do Microsoft PHP Drivers:

|Versão do driver&nbsp;&#8594;<br />&#8595; Versão do PHP|5.8|5.6|5,3|5.2|4.3|4,0|3.2|
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

|Versão do driver&nbsp;&#8594;<br />&#8595; Sistema operacional|5.8|5.6|5,3|5.2|4.3|4,0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2019                 |Sim|Sim|   |   |   |   |   |
|Windows Server 2016                 |Sim|Sim|Sim|Sim|Sim|   |   |
|Windows Server 2012 R2              |Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|Windows Server 2012                 |Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|Windows Server 2008 R2 SP1          |   |   |   |   |   |Sim|Sim|
|Windows Server 2008 R2              |   |   |   |   |   |   |   |
|Windows Server 2008 SP2             |   |   |   |   |   |Sim|Sim|
|Windows 10                          |Sim|Sim|Sim|Sim|Sim|Sim|   |
|Windows 8.1                         |Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|Windows 8                           |   |   |   |   |Sim|Sim|Sim|
|Windows 7 SP1                       |   |   |   |   |   |Sim|Sim|
|Windows Vista SP2                   |   |   |   |   |   |Sim|Sim|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

As seguintes versões dos sistemas operacionais Linux e macOS (somente 64 bit) são compatíveis com a versão listada do Microsoft PHP Drivers:

|Versão do driver&nbsp;&#8594;<br />&#8595; Sistema operacional|5.8|5.6|5,3|5.2|4.3|4,0|3.2|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 20.04 (64 bits)               |Sim|   |   |   |   |   |   |
|Ubuntu 19.10 (64 bits)               |Sim|   |   |   |   |   |   |
|Ubuntu 18.10 (64 bits)               |   |Sim|   |   |   |   |   |
|Ubuntu 18.04 (64 bits)               |Sim|Sim|Sim|   |   |   |   |
|Ubuntu 17.10 (64 bits)               |   |   |Sim|Sim|   |   |   |
|Ubuntu 16.04 (64 bits)               |Sim|Sim|Sim|Sim|Sim|Sim|   |
|Ubuntu 15.10 (64 bits)               |   |   |   |   |Sim|   |   |
|Ubuntu 15.04 (64 bits)               |   |   |   |   |   |Sim|   |
|Debian 10 (64 bits)                  |Sim|   |   |   |   |   |   |
|Debian 9 (64 bits)                   |Sim|Sim|Sim|Sim|   |   |   |
|Debian 8 (64 bits)                   |Sim|Sim|Sim|Sim|Sim|   |   |
|Red Hat Enterprise Linux 8 (64 bits) |Sim|   |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 bits) |Sim|Sim|Sim|Sim|Sim|Sim|   |
|Suse Enterprise Linux 15 (64 bits)   |Sim|Sim|   |   |   |   |   |
|Suse Enterprise Linux 12 (64 bits)   |Sim|Sim|Sim|Sim|   |   |   |
|Alpine Linux 3.11 (64 bits)<sup>1</sup>|Sim|   |   |   |   |   |   |
|macOS Catalina (64 bits)             |Sim|   |   |   |   |   |   |
|macOS Mojave (64 bits)               |Sim|Sim|   |   |   |   |   |
|macOS High Sierra (64 bits)          |Sim|Sim|Sim|   |   |   |   |
|macOS Sierra (64 bits)               |   |Sim|Sim|Sim|Sim|   |   |
|macOS El Capitan (64 bits)           |   |   |Sim|Sim|Sim|   |   |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> O suporte ao Alpine Linux é experimental na versão 5.8.0. A versão 5.8.1 introduz o suporte de produção.

## <a name="see-also"></a>Consulte Também

[Notas de Versão](release-notes-php-sql-driver.md)

[Recursos de suporte](support-resources-for-the-php-sql-driver.md)

[Requisitos do sistema](system-requirements-for-the-php-sql-driver.md)
