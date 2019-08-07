---
title: Notas sobre a versão ODBC em Linux e macOS | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: MightyPen
ms.technology: connectivity
ms.topic: conceptual
author: v-makouz
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 5d2587a6150807841edc9773478f1b798ee60d84
ms.sourcegitcommit: c5e2aa3e4c3f7fd51140727277243cd05e249f78
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2019
ms.locfileid: "68742807"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-to-sql-server-on-linux-and-macos"></a>Notas sobre a versão para Microsoft ODBC Driver para SQL Server em Linux e macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artigo lista e descreve o que há de novo nas versões com controle de versão do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em Linux e macOS.

<!--
Going forward, please use the new 2-column markdown table for each new H2 version section.
And we are keeping the H2 titles much shorter, partly by removing redundant or obvious info.
We want to track the Month YYYY each new version H2 section is added, at the end of the H2 title.
This is the new standard format for Release Notes article content.

OLD     FILE NAME:    linux-mac/release-notes.md
NOW NEW FILE NAME:    linux-mac/release-notes-odbc-sql-server-linux-mac.md

Thank you.
GeneMi.  2019/04/03.
-->
## <a name="174-august-2019"></a>17,4, agosto de 2019

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Always Encrypted com enclaves seguros. | Confira [Uso do Always Encrypted com o driver ODBC](../using-always-encrypted-with-the-odbc-driver.md). |
| Carregamento dinâmico do OpenSSL | Confira [Diretrizes de programação](programming-guidelines.md#bkmk-openssl). |
| Configurações de Keep Alive de TCP configuráveis. | Confira [Conectar-se ao SQL Server](connection-string-keywords-and-data-source-names-dsns.md). |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="173-february-2019"></a>17.3, fevereiro de 2019

| Novo item | Detalhes |
| :------- | :------ |
| Há suporte para novas distribuições. | &bull; &nbsp; &nbsp; SuSE 15<br/>&bull; &nbsp; &nbsp; Ubuntu 18.10<br/>&bull; &nbsp; &nbsp; macOS 10.14 |
| Modo de autenticação de Identidade de Serviço Gerenciada do Azure Active Directory (atribuída pelo usuário e pelo sistema). | Veja [Usando o Azure Active Directory com o Driver ODBC](../using-azure-active-directory.md). |
| Capacidade de transmitir parâmetros de entrada em relação a colunas Always Encrypted. | Para obter mais informações, veja [Limitações do driver ODBC ao usar Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted). |
| Transações distribuídas XA. | Veja [Usando Transações XA](../use-xa-with-dtc.md).<br/><br/>XA é o acrônimo de _eXtended Architecture_, que é um padrão para a execução de uma transação global que acessa mais de um sistema de armazenamento de dados do lado do servidor. |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2, julho de 2018

| Novo item | Detalhes |
| :------- | :------ |
| Há suporte para novas distribuições. | &bull; &nbsp; &nbsp; Ubuntu 18.04 |
| Classificação de Dados para o Banco de Dados SQL do Azure e SQL Server. | Veja [Classificação de Dados](../data-classification.md). |
| Suporte para codificação de servidor UTF-8. | &nbsp; |
| `SQLBrowseConnect` | &nbsp; |
| Dependência dinâmica de `libcurl`. | Começando com esta versão, o pacote `libcurl` não é uma dependência explícita.<br/>O pacote `libcurl` para OpenSSL ou NSS é necessário ao usar a autenticação do Azure Key Vault ou do Azure Active Directory.<br/>Se você encontrar um erro em relação ao `libcurl`, verifique se ele está instalado. |
| Resiliência de Conexão Ociosa com palavras-chave ConnectRetryCount e ConnectRetryInterval na cadeia de conexão. | &bull; &nbsp; &nbsp; Use `SQL_COPT_SS_CONNECT_RETRY_COUNT`(somente leitura) para recuperar o número de tentativas de repetição de conexão.<br/><br/>&bull; &nbsp; &nbsp; Use `SQL_COPT_SS_CONNECT_RETRY_INTERVAL`(somente leitura) para recuperar a duração do intervalo de repetição de conexão.<br/><br/>Veja [Resiliência de conexão no Windows ODBC Driver](../windows/connection-resiliency-in-the-windows-odbc-driver.md). |
| Correções de bugs. | [Correções de bugs](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>17.1, março de 2018

| Novo item | Detalhes |
| :------- | :------ |
| Suporte para os atributos de conexão `SQL_COPT_SS_CEKCACHETTL` e `SQL_COPT_SS_TRUSTEDCMKPATHS`. | &bull; &nbsp; &nbsp; `SQL_COPT_SS_CEKCACHETTL` permite controlar a hora em que o cache local de Chaves de Criptografia de Coluna existe, bem como liberá-lo.<br/><br/>&bull; &nbsp; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS` permite que o aplicativo restrinja operações Always Encrypted para usar somente a lista especificada de Chaves Mestras de Coluna.<br/><br/>Veja [Como usar o recurso Always Encrypted com o ODBC Driver for SQL Server](../using-always-encrypted-with-the-odbc-driver.md). |
| Suporte para carregar `.rll` do local padrão. | Veja a [seção "Carregamento de Arquivo de Recurso" no documento de instalação](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading). |
| Correções de bugs. | [Correções de bugs](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="17"></a>17

**Novas distribuições compatíveis**: macOS High Sierra e Ubuntu 17.10 

**Melhorias de desempenho**: melhoria de desempenho de mais de 10 vezes quando o driver converte para/de UTF-8/16.

**Recursos adicionados**:

Suporte a Always Encrypted para a API BCP

O novo atributo de cadeia de conexão UseFMTOnly faz driver usar metadados herdados em casos especiais que exigem tabelas temporárias.

Suporte para a Instância Gerenciada do SQL do Azure (Versão Prévia Privada Estendida). 
> [!NOTE]
> Há várias diferenças ao usar a Instância Gerenciada:
> -   Não há suporte para FILESTREAM 
> -   Não há suporte para acesso ao sistema de arquivos local, mas ele é necessário para itens como tracefiles 
> -   Não há suporte para criar UDT do caminho local 
> -   Não há suporte para Autenticação Integrada do Windows 
> -   Não há suporte para DTC 
> -   a conta 'sa' não está presente (a conta padrão é chamada de 'cloudSA')
> -   TDS token ERROR (0xAA) retorna o nome do servidor incorreto
> -   Não há suporte para caracteres especiais no nome do banco de dados 
> -   Não há suporte para ALTER DATABASE [dbname1] MODIFY NAME = [dbname2]
> -   As mensagens de erro são sempre mostradas em inglês, independentemente das configurações de idioma (mesmas que as do Azure) 

## <a name="131-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos-may-2017"></a>13.1, para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em Linux e macOS, maio de 2017

O Driver ODBC 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adiciona suporte para Always Encrypted e Azure Active Directory quando usado em conjunto com o Microsoft SQL Server 2016.

**Novas distribuições compatíveis**: há suporte para OS X 10.11 e macOS 10.12 na primeira versão do Driver ODBC no macOS. Agora há suporte para Ubuntu 16.10, juntamente com o Red Hat 6, 7 e SUSE 12. Cada plataforma tem um pacote relevante para a plataforma (RPM ou DEB) para facilitar a instalação e a configuração.  Veja [Instalando o Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para instruções de instalação.

**Alterações de suporte do unixODBC Driver Manager 2.3.1**: driver o ODBC não depende mais de empacotamento personalizado para o gerenciador de driver unixODBC (exceto no Red Hat 6) e depende, em vez disso, do gerenciador de pacotes de distribuição para resolver a dependência do UnixODBC de repositórios de distribuição.

**Suporte à API BCP**: o driver ODBC para Linux e macOS agora é compatível com o uso de [funções de API BCP (**bcp_init** etc.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="130-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>13.0 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em Linux

Com o Microsoft ODBC Driver 13.0 for SQL Server, agora também há suporte para SQL Server 2014 e SQL Server 2016.  

**Novas distribuições com suporte**:

O Ubuntu agora tem suporte, juntamente com o Red Hat e o SUSE. Cada plataforma tem um pacote relevante para a plataforma (RPM ou DEB) para facilitar a instalação e a configuração.  Veja [Instalando o Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para instruções de instalação.

**Suporte para unixODBC Driver Manager 2.3.1**: além de um gerenciador de driver mais novos, também há um pacote para instalar essa dependência que facilita a instalação e a configuração.  

**Resolução de IP de Rede Transparente**: a Resolução de IP de Rede Transparente é uma revisão do recurso existente de Failover de Várias Sub-Redes que afeta a sequência de conexão do driver no caso em que o primeiro IP resolvido do nome do host não responde e há vários IPs associados ao nome do host.

**Suporte a TLS 1.2**: o Microsoft ODBC Driver 13.0 for SQL Server em Linux agora dá suporte a TLS 1.2 quando são usadas comunicações seguras com o SQL Server.

## <a name="11-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>11 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em Linux

O driver ODBC no SUSE Linux (visualização) oferece suporte para o SUSE Linux Enterprise 11 Service Pack 2 de 64 bits. Para obter mais informações, consulte [System Requirements](../../../connect/odbc/linux-mac/system-requirements.md).  

O driver ODBC no Linux é compatível com [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para obter mais informações, veja [ODBC Driver no suporte do Linux para alta disponibilidade, recuperação de desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  

O driver ODBC no Linux oferece suporte para conexões com o Banco de Dados SQL do Microsoft Azure. Para obter mais informações, consulte [How to: Connect to Windows Azure SQL Database Using ODBC](https://msdn.microsoft.com/library/hh974312.aspx).  

A opção `-l` (tempo limite de logon) foi adicionada ao `bcp`. Para obter mais informações, veja [Como conectar-se com **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md).
