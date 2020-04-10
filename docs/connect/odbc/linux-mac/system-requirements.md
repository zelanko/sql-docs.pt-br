---
title: Requisitos do sistema (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/18/2020
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
ms.openlocfilehash: 2459a9f57f3591db1107994d0b18770690f22724
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921175"
---
# <a name="system-requirements"></a>Requisitos do Sistema

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tópico lista os requisitos para usar o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS.

## <a name="sql-version-compatibility"></a>Compatibilidade com versões do SQL

A compatibilidade de versão do SQL dos drivers do Linux e do macOS é igual à [compatibilidade de versão do SQL dos drivers do Windows](../windows/system-requirements-installation-and-driver-files.md#sql-version-compatibility).

## <a name="operating-system-support"></a>Suporte do sistema operacional

As versões 17, 13,1 e 13 dos drivers Linux e macOS são compatíveis com as versões de 64 bits dos seguintes sistemas operacionais:

|Sistema operacional com suporte     |17.5|17.4|17.3|17.2|17.1|17.0|13.1|13|
|-------------------------------|----|----|----|----|----|----|----|--|
|Apple OS X 10.11 (El Capitan)  | |S|S|S|S|S|S|S|
|Apple macOS 10.12 (Sierra)     | |S|S|S|S|S|S|S|
|Apple macOS 10.13 (High Sierra)|S|S|S|S|S|S|S|S|
|Apple macOS 10.14 (Mojave)     |S|S|S| | | | | |
|Apple macOS 10.15 (Catalina)   |S| | | | | | | |
|Alpine Linux 3.11              |S| | | | | | | |
|Debian Linux 8                 | |S|S|S|S|S|S|S|
|Debian Linux 9                 |S|S|S|S|S|S|S|S|
|Debian Linux 10                |S|S| | | | | | |
|Oracle Linux 8                 |S| | | | | | | |
|RedHat Enterprise Linux 6      |S|S|S|S|S|S|S|S|
|RedHat Enterprise Linux 7      |S|S|S|S|S|S|S|S|
|RedHat Enterprise Linux 8      |S|S| | | | | | |
|SUSE Linux Enterprise Server 11<sup>1</sup>|S|S|S|S|S|S|S|S|
|SUSE Linux Enterprise Server 12|S|S|S|S|S|S|S|S|
|SUSE Linux Enterprise Server 15|S|S|S| | | | | |
|Ubuntu Linux 14.04             | |S|S|S|S|S|S|S|
|Ubuntu Linux 16.04             |S|S|S|S|S|S|S|S|
|Ubuntu Linux 18.04             |S|S|S|S| | | | |
|Ubuntu Linux 19.10             |S| | | | | | | |

<sup>1</sup> O Driver ODBC 17 dá suporte apenas ao SUSE Linux Enterprise Server 11 SP4

Os pacotes de instalação para o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13, 13.1 e 17 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS resolvem as dependências do driver automaticamente quando instalados usando o sistema de gerenciamento de pacotes da sua distribuição, conforme descrito em [Instalar o Driver ODBC (Linux)](installing-the-microsoft-odbc-driver-for-sql-server.md) e [Instalar o Driver ODBC (macOS)](install-microsoft-odbc-driver-sql-server-macos.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 para SQL Server  
  
* Gerenciador de Driver UnixODBC 2.3.0 64 bits, compilado para SQLLEN/SQLULEN 64 bits. Não há suporte para versões posteriores do Gerenciador de Driver UnixODBC de 64 bits com o driver ODBC no Linux. Consulte [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) para obter mais informações.  
  
* O driver ODBC para **Red Hat Enterprise Linux 5 (64 bits)** exige os seguintes pacotes e pode ser baixado aqui: [Microsoft ODBC Driver 11 para SQL Server – Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `e2fsprogs-libs`  
  * `krb5-libs`  
  * `openssl`  
  
* O driver ODBC para **Red Hat Enterprise Linux 6 (64 bits)** exige os seguintes pacotes e pode ser baixado aqui: [Microsoft ODBC Driver 11 para SQL Server – Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `libuuid`  
  * `krb5-libs`  
  * `openssl`  
  
* O driver ODBC para **SUSE Linux Enterprise 11 Service Pack 2 (64 bits)** exige os seguintes pacotes e pode ser baixado aqui: [Versão prévia do Microsoft ODBC Driver 11 para SQL Server – SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
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
