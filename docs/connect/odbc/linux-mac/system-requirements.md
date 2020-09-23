---
title: Requisitos do sistema (ODBC Driver for SQL Server)
description: Este artigo lista os requisitos do sistema do ODBC Driver para sistemas operacionais SQL Server em Linux e macOS.
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 74b7bf1680dd956dfca85917939ad24a3559d7de
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934455"
---
# <a name="system-requirements-linux-and-macos"></a>Requisitos do sistema (Linux e macOS)

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tópico lista os requisitos para usar o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS.

## <a name="sql-version-compatibility"></a>Compatibilidade com versões do SQL

A compatibilidade de versão do SQL dos drivers do Linux e do macOS é igual à [compatibilidade de versão do SQL dos drivers do Windows](../windows/system-requirements-installation-and-driver-files.md#sql-version-compatibility).

## <a name="operating-system-support"></a>Suporte do sistema operacional

As versões 17, 13.1 e 13 dos drivers Linux e macOS são compatíveis com a arquitetura x64 dos seguintes sistemas operacionais:

|Versão do driver&nbsp;&#8594;<br />&#8595; Sistema operacional     |17.6|17.5|17.4|17.3|17.2|17.1|17.0|13.1|13|
|-------------------------------|----|----|----|----|----|----|----|----|---|
|Apple OS X 10.11 (El Capitan)  |    |    |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|Apple macOS 10.12 (Sierra)     |    |    |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|Apple macOS 10.13 (High Sierra)|Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|Apple macOS 10.14 (Mojave)     |Sim |Sim |Sim |Sim |    |    |    |    |   |
|Apple macOS 10.15 (Catalina)   |Sim |Sim |    |    |    |    |    |    |   |
|Alpine Linux 3.11              |Sim |Sim |    |    |    |    |    |    |   |
|Debian Linux 8                 |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|Debian Linux 9                 |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|Debian Linux 10                |Sim |Sim |Sim |    |    |    |    |    |   |
|Oracle Linux 8                 |Sim |Sim |    |    |    |    |    |    |   |
|RedHat Enterprise Linux 6      |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|RedHat Enterprise Linux 7      |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|RedHat Enterprise Linux 8      |Sim |Sim |Sim |    |    |    |    |    |   |
|SUSE Linux Enterprise Server 11<sup>1</sup>|Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|SUSE Linux Enterprise Server 12|Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|SUSE Linux Enterprise Server 15|Sim |Sim |Sim |Sim |    |    |    |    |   |
|Ubuntu Linux 14.04             |    |    |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|Ubuntu Linux 16.04             |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim |Sim|
|Ubuntu Linux 18.04             |Sim |Sim |Sim |Sim |Sim |    |    |    |   |
|Ubuntu Linux 20.04             |Sim |    |    |    |    |    |    |    |   |

<sup>1</sup> O Driver ODBC 17 dá suporte apenas ao SUSE Linux Enterprise Server 11 SP4

Os pacotes de instalação para o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13, 13.1 e 17 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS resolvem as dependências do driver automaticamente quando instalados usando o sistema de gerenciamento de pacotes da sua distribuição, conforme descrito em [Instalar o Driver ODBC (Linux)](installing-the-microsoft-odbc-driver-for-sql-server.md) e [Instalar o Driver ODBC (macOS)](install-microsoft-odbc-driver-sql-server-macos.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 para SQL Server  
  
* Gerenciador de Driver UnixODBC 2.3.0 64 bits, compilado para SQLLEN/SQLULEN 64 bits. Não há suporte para versões posteriores do Gerenciador de Driver UnixODBC de 64 bits com o driver ODBC no Linux. Consulte [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) para obter mais informações.  
  
* O driver ODBC para **Red Hat Enterprise Linux 5 (64 bits)** requer os seguintes pacotes e pode ser baixado em [Microsoft ODBC Driver 11 for SQL Server – Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `e2fsprogs-libs`  
  * `krb5-libs`  
  * `openssl`  
  
* O driver ODBC para **Red Hat Enterprise Linux 6 (64 bits)** requer os seguintes pacotes e pode ser baixado em [Microsoft ODBC Driver 11 for SQL Server – Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `libuuid`  
  * `krb5-libs`  
  * `openssl`  
  
* O driver ODBC para **SUSE Linux Enterprise 11 Service Pack 2 (64 bits)** requer os seguintes pacotes e pode ser baixado em [Versão prévia do Microsoft ODBC Driver 11 for SQL Server – SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
  * `glibc`  
  * `libstdc++46`  
  * `libgcc46`  
  * `libuuid1`  
  * `krb5`  
  * `libopenssl0_9_8`  
  
## <a name="see-also"></a>Consulte Também

[Instalando o Gerenciador de Driver](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)  
[Problemas conhecidos nesta versão do driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  
[Notas de Versão](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
