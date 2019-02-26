---
title: Notas de versão – Microsoft ODBC Driver for SQL Server em Linux e macOS | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 12f45cd1014a312eec7854685d8c7fe2e64b9714
ms.sourcegitcommit: b3d84abfa4e2922951430772c9f86dce450e4ed1
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56662750"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Notas de versão para o Microsoft ODBC Driver for SQL Server em Linux e macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS

**Novo distribuições suportadas**: 15 SuSE, Ubuntu 18.10, macOS 10.14

**Recursos adicionados**:

- Azure Active Directory Managed Service Identity (sistema e atribuída pelo usuário) modo de autenticação
- Parâmetro de entrada AE streaming
- XA DTC

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS

**Novo distribuições suportadas**: 18.04 Ubuntu

**Recursos adicionados**:

Classificação de dados para o banco de dados SQL e SQL Server, para obter mais informações consulte [classificação de dados](../data-classification.md)

Suporte à codificação do servidor de UTF-8

SQLBrowseConnect

Dependência dinâmica no `libcurl`:
- Começando com esta versão, o `libcurl` pacote não é uma dependência explícita. O `libcurl` do pacote para OpenSSL ou NSS é necessária ao usar a autenticação do Azure Key Vault ou Azure Active Directory. Se você encontrar um erro em relação ao `libcurl`, verifique se ele está instalado.

Idle resiliência de Conexão com ConnectRetryCount e ConnectRetryInterval palavras-chave na cadeia de caracteres de conexão (para obter mais informações, consulte [resiliência de Conexão no Driver ODBC do Windows](../windows/connection-resiliency-in-the-windows-odbc-driver.md)):
- Use `SQL_COPT_SS_CONNECT_RETRY_COUNT`(somente leitura) para recuperar o número de tentativas de repetição de conexão.
- Use `SQL_COPT_SS_CONNECT_RETRY_INTERVAL`(somente leitura) para recuperar a duração do intervalo de repetição de conexão.
- Conexão será repetida uma vez por padrão.


[Correções de bugs](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS

**Recursos adicionados**:

Suporte para `SQL_COPT_SS_CEKCACHETTL` e `SQL_COPT_SS_TRUSTEDCMKPATHS` atributos de conexão (para obter mais informações, consulte [usando o Always Encrypted com o Driver ODBC para SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` Permite controlar a hora em que existe no cache local de chaves de criptografia de coluna, bem como liberar a ele
- `SQL_COPT_SS_TRUSTEDCMKPATHS` Permite que o aplicativo restringir as operações de AE para usar somente a lista especificada de chaves mestras de coluna



Suporte para o carregamento de `.rll` do local padrão (para obter mais informações, consulte [seção do documento de instalação 'Carregamento de arquivo de recurso'](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading))

[Correções de bugs](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS

**Novo distribuições suportadas**: macOS High Sierra e Ubuntu 17.10 

**Melhorias de desempenho**: maior que 10 vezes melhoria no desempenho quando o driver converte / para UTF-8/16.

**Recursos adicionados**:

Always Encripted dá suporte para a API BCP

Novo atributo de cadeia de caracteres de conexão UseFMTOnly faz com que o driver usar metadados herdados em casos especiais que exigem a tabelas temporárias.

Suporte para a instância gerenciada do SQL do Azure (versão prévia privada estendida). 
> [!NOTE]
> Há várias diferenças ao usar a instância gerenciada:
> -   Não há suporte para FILESTREAM 
> -   Acesso de sistema de arquivos local não tem suporte, mas necessário para coisas como tracefiles 
> -   Criar o UDT de local não há suporte para o caminho 
> -   Não há suporte para a autenticação integrada do Windows 
> -   Não há suporte para DTC 
> -   conta 'sa' não está presente (a conta padrão é chamada 'cloudSA')
> -   Erro de token de TDS (0xAA) retorna o nome de servidor incorreto
> -   Não há suporte para caracteres especiais no nome do banco de dados 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] não tem suporte
> -   As mensagens de erro são sempre mostradas em inglês, independentemente da linguagem configurações (mesmo que o Azure) 

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS  

Driver ODBC 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adiciona suporte para Always Encrypted e o Azure Active Directory quando usado em conjunto com o Microsoft SQL Server 2016.

**Novo distribuições suportadas**: OS X 10.11 e macOS 10.12 têm suporte na primeira versão do Driver ODBC no macOS. Ubuntu 16.10 agora também dá suporte, juntamente com o Red Hat 6, 7 e SUSE 12. Cada plataforma tem um pacote de plataforma relevante (RPM ou DEB) para facilitar a instalação e configuração.  Ver [instalando o Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para instruções de instalação.

**unixODBC 2.3.1 do Gerenciador de Driver suporte alterações**: driver ODBC não depende de empacotamento personalizado para o Gerenciador de driver unixODBC (exceto no RedHat 6) e depende em vez disso, o Gerenciador de pacotes de distribuição para resolver a dependência de UnixODBC de repositórios de distribuição.

**Suporte a API BCP**: driver ODBC do Linux e macOS agora suporta o uso do [funções de API BCP (**bcp_init**, etc.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>O que há de novo no Microsoft ODBC Driver 13.0 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux  
Com o Microsoft ODBC Driver 13.0 for SQL Server, SQL Server 2014 e SQL Server 2016 agora também têm suporte.  

**Novo distribuições suportadas**:

O Ubuntu agora tem suporte, juntamente com o Red Hat e o SUSE. Cada plataforma tem um pacote de plataforma relevante (RPM ou DEB) para facilitar a instalação e configuração.  Ver [instalando o Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para instruções de instalação.

**unixODBC 2.3.1 do Gerenciador de Driver suporte**: além de um Gerenciador de driver mais recente, também há um pacote para instalar essa dependência que facilita a instalação e configuração.  

**Resolução de IP de rede transparente**: resolução de IP de rede transparente é uma revisão de recurso existente do Failover de várias sub-redes que afeta a sequência de conexão do driver no caso em que a primeira resolvido IP do nome do host não responder e há vários IPs associados com o nome do host.

**Suporte a TLS 1.2**: O Microsoft ODBC Driver 13.0 for SQL Server no Linux agora dá suporte a TLS 1.2 quando proteger as comunicações com o SQL Server são usadas.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux  
O driver ODBC no SUSE Linux (visualização) oferece suporte para o SUSE Linux Enterprise 11 Service Pack 2 de 64 bits. Para obter mais informações, consulte [System Requirements](../../../connect/odbc/linux-mac/system-requirements.md).  

O driver ODBC no Linux é compatível com [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para obter mais informações, consulte [Driver ODBC no suporte do Linux para alta disponibilidade, recuperação de desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  

O driver ODBC no Linux oferece suporte para conexões com o Banco de Dados SQL do Microsoft Azure. Para obter mais informações, consulte [How to: Connect to Windows Azure SQL Database Using ODBC](https://msdn.microsoft.com/library/hh974312.aspx).  

O `-l` opção (tempo limite de logon) foi adicionada ao `bcp`. Para obter mais informações, veja [Como conectar-se com **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md).
