---
title: Requisitos do sistema (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 49cb24120d6c476e5b03c4a0cad2ddda511a9360
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76911183"
---
# <a name="system-requirements"></a>Requisitos do Sistema
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tópico lista os requisitos para usar o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS.


## <a name="microsoft-odbc-driver-13-131-and-17-for-sql-server"></a>Microsoft ODBC Driver 13, 13.1 e 17 for SQL Server

Os drivers Linux e macOS estão disponíveis somente para as versões de 64 bits dos sistemas operacionais a seguir:

|Sistema operacional|Versão do driver compatível|
|------------------------------------|--------------------------------|
|Apple OS X 10.11 (El Capitan)|13, 13.1, 17.4|
|Apple macOS 10.12 (Sierra)|13, 13.1, 17.4|
|Apple macOS 10.13 (High Sierra)|17+| 
|Apple macOS 10.14 (Mojave)|17+| 
|Apple macOS 10.15 (Catalina)|17.5+| 
|Alpine Linux 3.11|17.5+| 
|Debian Linux 8|13, 13.1, 17.4| 
|Debian Linux 9|17+|
|Debian Linux 10|17.4+|
|Oracle Linux 8|17.5+|
|RedHat Enterprise Linux 6|13, 13.1, 17+|
|RedHat Enterprise Linux 7|13, 13.1, 17+|
|RedHat Enterprise Linux 8|17.4+|
|SuSE Linux Enterprise Server 11|13, 13.1, 17+ <br /><br /> **OBSERVAÇÃO:** O Driver ODBC 17 é compatível somente com o SUSE Linux Enterprise Server 11 SP4|
|SuSE Linux Enterprise Server 12|13, 13.1, 17+|
|SuSE Linux Enterprise Server 15|17+|
|Ubuntu Linux 14.04|13, 13.1, 17.4|
|Ubuntu Linux 15.10|13, 13.1|
|Ubuntu Linux 16.04|13, 13.1, 17+|
|Ubuntu Linux 16.10|13, 13.1|
|Ubuntu Linux 17.04|17.4| 
|Ubuntu Linux 17.10|17.4|
|Ubuntu Linux 18.04|17+|
|Ubuntu Linux 18.10|17.4|
|Ubuntu Linux 19.04|17.3|
|Ubuntu Linux 19.10|17.5+| 

> [!NOTE]
> - Os sistemas operacionais com compatibilidade ativa mostram um "+" após a versão do driver, aqueles sem o sinal de mais mostram a última versão do driver compatível com o sistema operacional fornecido

Os pacotes de instalação para o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13, 13.1 e 17 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS resolvem as dependências do driver automaticamente quando instalados usando o sistema de gerenciamento de pacotes da sua distribuição, conforme descrito em [Instalando o Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 para SQL Server  
  
-   Gerenciador de Driver UnixODBC 2.3.0 64 bits, compilado para SQLLEN/SQLULEN 64 bits. Não há compatibilidade com versões posteriores do Gerenciador de Driver UnixODBC de 64 bits com o driver ODBC no Linux. Consulte [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) para obter mais informações.  
  
-   O driver ODBC para **Red Hat Enterprise Linux 5 (64 bits)** exige os seguintes pacotes e pode ser baixado aqui: [Microsoft ODBC Driver 11 para SQL Server – Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `e2fsprogs-libs`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   O driver ODBC para **Red Hat Enterprise Linux 6 (64 bits)** exige os seguintes pacotes e pode ser baixado aqui: [Microsoft ODBC Driver 11 para SQL Server – Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `libuuid`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   O driver ODBC para **SUSE Linux Enterprise 11 Service Pack 2 (64 bits)** exige os seguintes pacotes e pode ser baixado aqui: [Versão prévia do Microsoft ODBC Driver 11 para SQL Server – SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
    -   `glibc`  
    -   `libstdc++46`  
    -   `libgcc46`  
    -   `libuuid1`  
    -   `krb5`  
    -   `libopenssl0_9_8`  
  
## <a name="see-also"></a>Veja também
[Instalando o Gerenciador de Driver](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Problemas conhecidos nesta versão do driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[Notas sobre a versão](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
