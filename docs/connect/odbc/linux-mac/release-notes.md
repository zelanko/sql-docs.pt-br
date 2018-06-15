---
title: Notas - Microsoft ODBC Driver for SQL Server no Linux e macOS | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bddb826772d1c6ad7e33dce92b1e2615779b8931
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853291"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Notas de versão para o Microsoft ODBC Driver for SQL Server no Linux e macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>O que há de novo no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] o Driver ODBC 17.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Windows

**Recursos adicionados**:

Suporte para `SQL_COPT_SS_CEKCACHETTL` e `SQL_COPT_SS_TRUSTEDCMKPATHS` atributos de conexão (para obter mais informações, consulte [usando sempre criptografado com o Driver ODBC para SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` Permite controlando a hora em que o cache local das chaves de criptografia de coluna existe, bem como liberar a ele
- `SQL_COPT_SS_TRUSTEDCMKPATHS` Permite que o aplicativo restringir as operações de AE para usar somente a lista especificada de chaves mestras de coluna



Suporte para o carregamento de `.rll` de local padrão (para obter mais informações, consulte [seção do documento de instalação 'Carregamento de arquivo de recurso'](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading))

[Correções de bugs](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd-on-linux-and-macos"></a>O que há de novo no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 17 do Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em Linux e macOS

**Novo distribuições suportadas**: macOS Serra alta e Ubuntu 17.10 

**Melhorias de desempenho**: maior que 10 vezes melhoria no desempenho quando o driver converte para/de UTF-8/16.

**Recursos adicionados**:

Sempre criptografado suporte para a API BCP

Novo atributo de cadeia de caracteres de conexão UseFMTOnly faz com que o driver usar metadados herdados em casos especiais que exigem a tabelas temporárias.

Suporte para a instância gerenciada do SQL Azure (visualização privada estendida). 
> [!NOTE]
> Há algumas diferenças ao usar a instância gerenciada:
> -   Não há suporte para FILESTREAM 
> -   Acesso de sistema de arquivos local não tem suporte, mas necessário para coisas como tracefiles 
> -   Crie a UDT do local não há suporte para o caminho 
> -   Não há suporte para a autenticação integrada do Windows 
> -   Não há suporte para o DTC 
> -   conta 'sa' não está presente (a conta padrão é chamada 'cloudSA')
> -   Erro de token de TDS (0xAA) retorna o nome de servidor incorreto
> -   Não há suporte para caracteres especiais no nome do banco de dados 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] não tem suporte
> -   As mensagens de erro são sempre mostradas em inglês, independentemente do idioma configurações (mesmo que o Azure) 

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-linux-and-macos"></a>O que há de novo no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em Linux e macOS  

ODBC Driver 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] adiciona suporte para sempre criptografado e o Active Directory do Azure quando usado em conjunto com o Microsoft SQL Server 2016.

**Novo distribuições suportadas**: OS X 10.11 e macOS 10.12 têm suporte na primeira versão do Driver ODBC no macOS. Ubuntu 16.10 agora também tem suporte, juntamente com o Red Hat 6, 7 e o SUSE 12. Cada plataforma tem um pacote de plataforma relevante (RPM ou DEB) para facilitar a instalação e configuração.  Consulte [instalar o Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para instruções de instalação.

**unixODBC 2.3.1 do Gerenciador de Driver suporte alterações**: O ODBC driver não depende de empacotamento personalizado para o Gerenciador de driver unixODBC (exceto no RedHat 6) e se baseia em vez disso, no Gerenciador de pacote de distribuição para resolver a dependência de UnixODBC repositórios da distribuição.

**Suporte a API BCP**: driver ODBC do Linux e macOS agora dá suporte ao uso do [funções de API BCP (**bcp_init**, etc.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>O que há de novo no Microsoft ODBC Driver 13.0 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Linux  
Com o Microsoft ODBC Driver 13.0 para SQL Server, SQL Server 2014 e SQL Server 2016 agora também têm suporte.  

**Novo distribuições suportadas**:

O Ubuntu agora tem suporte, juntamente com o Red Hat e o SUSE. Cada plataforma tem um pacote de plataforma relevante (RPM ou DEB) para facilitar a instalação e configuração.  Consulte [instalar o Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para instruções de instalação.

**Suporte de 2.3.1 do Gerenciador de Driver unixODBC**: além de um Gerenciador de driver mais recente, também há um pacote para instalar essa dependência que facilita a instalação e configuração.  

**Resolução de IP de rede transparente**: resolução de IP de rede transparente é uma versão do recurso de Failover de várias sub-redes existente que afeta a sequência de conexão do driver no caso em que a primeira resolvido IP do nome do host não responder e há vários IPs associados com o nome do host.

**Suporte a TLS 1.2**: O Microsoft ODBC Driver 13.0 para SQL Server no Linux agora dá suporte a TLS 1.2 ao proteger as comunicações com o SQL Server são usadas.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>O que há de novo no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Linux  
O driver ODBC no SUSE Linux (visualização) oferece suporte para o SUSE Linux Enterprise 11 Service Pack 2 de 64 bits. Para obter mais informações, consulte [requisitos de sistema](../../../connect/odbc/linux-mac/system-requirements.md).  

O driver ODBC no Linux oferece suporte a [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para obter mais informações, consulte [Driver ODBC no Linux suporte para alta disponibilidade, recuperação de desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  

O driver ODBC no Linux oferece suporte para conexões com o Banco de Dados SQL do Microsoft Azure. Para obter mais informações, consulte [How to: Connect to Windows Azure SQL Database Using ODBC](http://msdn.microsoft.com/library/hh974312.aspx).  

O `-l` opção (tempo limite de logon) foi adicionada ao `bcp`. Para obter mais informações, consulte [conectando com **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md).
