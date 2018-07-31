---
title: Requisitos do sistema (Driver ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bab69d8a2ebf405e99cc9cff7e4cdadb94d79f98
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38047479"
---
# <a name="system-requirements"></a>Requisitos do sistema
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tópico lista os requisitos para usar o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Linux e no macOS.


## <a name="microsoft-odbc-driver-13-131-and-17-for-sql-server"></a>Microsoft ODBC Driver 13, 13.1 e 17 for SQL Server

Os drivers de Linux e macOS estão disponíveis somente para as versões de 64 bits dos sistemas operacionais a seguir:

|Sistema operacional|Versão do Driver com suporte|
|------------------------------------|--------------------------------|
|Apple OS X 10.11 (El Capitan)|13, 13.1, 17|
|Apple macOS 10.12 (Sierra)|13, 13.1, 17|
|Apple macOS 10.13 (High Sierra)|17| 
|Linux Debian 8|13, 13.1, 17|
|Linux Debian 9|17|
|RedHat Enterprise Linux 6|13, 13.1, 17|
|RedHat Enterprise Linux 7|13, 13.1, 17|
|SuSE Linux Enterprise Server 11|13, 13.1, 17 <br /><br /> **Observação:** ODBC Driver 17 SuSE Linux Enterprise Server 11 SP4 oferece suporte somente à|
|SuSE Linux Enterprise Server 12|13, 13.1, 17|
|Ubuntu Linux 14.04|13, 13.1, 17|
|Ubuntu Linux 15.10|13, 13.1|
|Ubuntu Linux 16.04|13, 13.1, 17|
|Ubuntu Linux 16.10|13, 13.1|
|Ubuntu Linux 17.10|17|

A instalação de pacotes para o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13, 13.1 e 17 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Linux e macOS resolver as dependências do driver automaticamente quando instalados usando o sistema de gerenciamento de pacotes da sua distribuição, conforme descrito em [ Instalando o Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 para SQL Server  
  
-   Gerenciador de Driver UnixODBC 2.3.0 64 bits, compilado para SQLLEN/SQLULEN 64 bits. Não há suporte para versões posteriores do Gerenciador de Driver UnixODBC de 64 bits com o driver ODBC no Linux. Consulte [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) para obter mais informações.  
  
-   O driver ODBC para **Red Hat Enterprise Linux 5 (64 bits)** requer os seguintes pacotes e pode ser baixado em [Microsoft ODBC Driver 11 for SQL Server – Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `e2fsprogs-libs`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   O driver ODBC para **Red Hat Enterprise Linux 6 (64 bits)** requer os seguintes pacotes e pode ser baixado em [Microsoft ODBC Driver 11 for SQL Server – Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `libuuid`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   O driver ODBC para **SUSE Linux Enterprise 11 Service Pack 2 (64 bits)** requer os seguintes pacotes e pode ser baixado em [Versão prévia do Microsoft ODBC Driver 11 for SQL Server – SUSE Linux](http://go.microsoft.com/fwlink/?LinkId=264916)  
    -   `glibc`  
    -   `libstdc++46`  
    -   `libgcc46`  
    -   `libuuid1`  
    -   `krb5`  
    -   `libopenssl0_9_8`  
  
## <a name="see-also"></a>Consulte Também
[Instalando o Gerenciador de Driver](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Problemas conhecidos nesta versão do driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[Notas de versão](../../../connect/odbc/linux-mac/release-notes.md)  
