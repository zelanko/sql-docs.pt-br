---
title: Matriz de suporte de Drivers da Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: David-Engel
ms.author: v-daveng
manager: ''
ms.openlocfilehash: b8f1fad66e906b71ff5ea247ba4615e7be774f63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Drivers de PHP da Microsoft para a matriz de suporte do SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  Esta página contém a política de ciclo de vida de matriz e suporte de suporte para Drivers de PHP da Microsoft para SQL Server.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Matriz de ciclo de vida de suporte de Drivers PHP da Microsoft e a política
 A política de ciclo de vida de suporte da Microsoft (MSL) fornece informações transparentes e previsíveis sobre o ciclo de vida de suporte dos produtos da Microsoft. Versões de Drivers do PHP 5. x, 4. x e 3. x têm cinco anos de suporte base a partir da data de lançamento do driver. Suporte base é definido no [site de ciclo de vida do suporte Microsoft](https://support.microsoft.com/lifecycle).

 Opções de suporte personalizado e estendido não estão disponíveis para os Drivers de PHP da Microsoft.

 Os seguintes Drivers de PHP da Microsoft têm suporte até a data de término do suporte indicada.

|Nome do driver|Versão do pacote de driver|Fim do suporte básico|
|-|-|-|
|5.2 de Drivers de PHP da Microsoft para SQL Server|5.2|9 de fevereiro de 2023|
|4.3 de Drivers de PHP da Microsoft para SQL Server|4.3|6 de julho de 2022|
|Microsoft PHP Drivers 4.0 para SQL Server|4.0|11 de julho de 2021|
|3.2 de Drivers de PHP da Microsoft para SQL Server|3.2|9 de março de 2020|
|Drivers 3.1 do PHP da Microsoft para SQL Server|3.1|12 de dezembro de 2019|

 Não há suporte para os seguintes Drivers de PHP da Microsoft.

|Nome do driver|Versão do pacote de driver|Fim do suporte básico|
|-|-|-|
|PHP do Microsoft Drivers 3.0 para SQL Server|3.0|6 de março de 2017|
|Drivers de PHP da Microsoft 2.0 para SQL Server|2.0|10 de agosto de 2015|
|Drivers de PHP da Microsoft 1.0 para o SQL Server|1.0|28 de abril de 2014|

## <a name="sql-server-version-certified-compatibility"></a>Certificados de compatibilidade de versão do SQL Server
 A tabela a seguir lista as versões do SQL Server que foram testadas e certificadas como compatíveis com a versão do driver correspondente. Tentamos manter a compatibilidade com versões anteriores do driver, mas apenas o driver mais recente com suporte é testado e certificado com novas versões do SQL Server como o SQL Server é liberado.

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595;Versão do SQL Server|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Instância gerenciada do SQL Azure<br/> (Visualização privada estendida)|S|S| | | | | |
|Azure SQL Data Warehouse|S|S| | | | | |
|SQL Server 2017   |S|S| | | | | |
|SQL Server 2016   |S|S|S| | | | |
|SQL Server 2014   |S|S|S|S|S| | |
|SQL Server 2012   |S|S|S|S|S|S| |
|SQL Server 2008 R2|S|S|S|S|S|S|S|
|SQL Server 2008   | | |S|S|S|S|S|

## <a name="php-version-support"></a>Suporte de versão do PHP
 As seguintes versões do PHP têm suporte com a versão listada de Drivers de PHP da Microsoft:

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595;Versão do PHP|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|7.2|7.2.1+ no Windows<br/>7.2.0+ em outras plataformas| | | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|       |       |       |5.6.4 +  |        |        |        |
|5.5|       |       |       |5.5.16 + |5.5.16 + |        |        |
|5.4|       |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|       |       |       |        |        |5.3.0   |5.3.0   |
|5.2|       |       |       |        |        |        |5.2.4<br />5.2.13|

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte
 As seguintes versões de sistema operacional do Windows têm suporte com a versão listada de Drivers de PHP da Microsoft:

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595;Sistema Operacional|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Windows Server 2016                 |S  |S  |   |   |   |   |   |
|Windows Server 2012 R2              |S  |S  |S  |S  |S  |   |   |
|Windows Server 2012                 |S  |S  |S  |S  |S  |   |   |
|Windows Server 2008 R2 SP1          |   |   |S  |S  |S  |S  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |S  |
|Windows Server 2008 SP2             |   |   |S  |S  |S  |S  |   |
|Windows Server 2008                 |   |   |   |   |   |   |S  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |S  |
|Windows 10                          |S  |S  |S  |   |   |   |   |
|Windows 8.1                         |S  |S  |S  |S  |S  |   |   |
|Windows 8                           |   |S  |S  |S  |S  |   |   |
|Windows 7 SP1                       |   |   |S  |S  |S  |S  |   |
|Windows Vista SP2                   |   |   |S  |S  |S  |S  |S  |
|Windows XP SP3                      |   |   |   |   |   |   |S  |

 O Linux e Mac (somente 64 bits) de versões de sistema operacional a seguir têm suporte com a versão listada de Drivers de PHP da Microsoft:

|PHP para a versão do driver do SQL Server&#8594;<br />&#8595;Sistema Operacional|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Ubuntu 17.10 (64 bits)               |S  |   |   |   |   |   |   |
|Ubuntu 16.04 (64 bits)               |S  |S  |S  |   |   |   |   |
|Ubuntu 15.10 (64 bits)               |   |S  |   |   |   |   |   |
|Ubuntu 15.04 (64 bits)               |   |   |S  |   |   |   |   |
|Debian 9 (64 bits)                   |S  |   |   |   |   |   |   |
|Debian 8 (64 bits)                   |S  |S  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 bits) |S  |S  |S  |   |   |   |   |
|Linux SuSE Enterprise 12 (64 bits)   |S  |   |   |   |   |   |   |
|macOS Serra (64 bits)               |S  |S  |   |   |   |   |   |
|macOS El Capitan (64 bits)           |S  |S  |   |   |   |   |   |

## <a name="see-also"></a>Consulte também  
[Notas de versão](../../connect/php/release-notes-for-the-php-sql-driver.md)

[Recursos de suporte](../../connect/php/support-resources-for-the-php-sql-driver.md)

[Requisitos do sistema](../../connect/php/system-requirements-for-the-php-sql-driver.md)
