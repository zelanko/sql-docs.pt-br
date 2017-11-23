---
title: Requisitos do sistema | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
caps.latest.revision: "31"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8bf81a5a5be0f5d276946b6f722c1875922b2155
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="system-requirements"></a>Requisitos do sistema
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tópico lista os requisitos para usar o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] o Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em Linux e macOS.

## <a name="microsoft-odbc-driver-13-and-131-for-sql-server"></a>Microsoft ODBC Driver 13 e 13.1 para SQL Server

Os drivers de Linux e macOS estão disponíveis apenas para as versões de 64 bits dos sistemas operacionais a seguir:

- Apple macOS 10.12 (Serra)
- Apple OS X 10.11 (El Capitan)
- Debian Linux 8
- Enterprise RedHat Linux 6
- Enterprise RedHat Linux 7
- SuSE Linux Enterprise Server 11
- SuSE Linux Enterprise Server 12
- Ubuntu Linux 14.04
- Ubuntu Linux 15.10
- Ubuntu Linux 16.04
- Ubuntu Linux 16.10

A instalação de pacotes para o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 e 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em Linux e macOS resolver dependências do driver automaticamente quando instalados usando o sistema de gerenciamento de pacote de sua distribuição, conforme descrito em [Instalar o Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Microsoft ODBC Driver 11 para SQL Server  
  
-   Gerenciador de Driver UnixODBC 2.3.0 64 bits, compilado para SQLLEN/SQLULEN 64 bits. Não há suporte para versões posteriores do Gerenciador de Driver UnixODBC de 64 bits com o driver ODBC no Linux. Consulte [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) para obter mais informações.  
  
-   O driver ODBC para **Red Hat Enterprise Linux 5 (64 bits)** requer os seguintes pacotes e pode ser baixado em: [Microsoft ODBC Driver 11 para SQL Server - Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   glibc  
    -   libgcc  
    -   libstdc++  
    -   e2fsprogs-libs  
    -   krb5-libs  
    -   openssl  
  
-   O driver ODBC para **Red Hat Enterprise Linux 6 (64 bits)** requer os seguintes pacotes e pode ser baixado em: [Microsoft ODBC Driver 11 para SQL Server - Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   glibc  
    -   libgcc  
    -   libstdc++  
    -   libuuid  
    -   krb5-libs  
    -   openssl  
  
-   O driver ODBC para **SUSE Linux Enterprise 11 Service Pack 2 (64 bits)** requer os seguintes pacotes e pode ser baixado em: [visualização do Microsoft ODBC Driver 11 para SQL Server - SUSE Linux](http://go.microsoft.com/fwlink/?LinkId=264916)  
    -   glibc  
    -   libstdc++46  
    -   libgcc46  
    -   libuuid1  
    -   krb5  
    -   libopenssl0_9_8  
  
## <a name="see-also"></a>Consulte também
[Instalando o Gerenciador de Driver](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Problemas conhecidos nesta versão do driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[Notas de versão](../../../connect/odbc/linux-mac/release-notes.md)  
