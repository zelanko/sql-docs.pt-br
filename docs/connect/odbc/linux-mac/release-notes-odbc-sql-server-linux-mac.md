---
title: Notas sobre a versão do ODBC Driver for SQL Server em Linux e macOS
description: Saiba quais são as novidades e mudanças em versões lançadas do Microsoft ODBC Driver for SQL Server.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-jizho2
ms.technology: connectivity
ms.topic: conceptual
author: v-chojas
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 79c86e34a759e65f858621932fea5772e51756e2
ms.sourcegitcommit: a4ee6957708089f7d0dda15668804e325b8a240c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87899526"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Notas de versão para o Microsoft ODBC Driver for SQL Server em Linux e macOS

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


## <a name="176-july-2020"></a>17.6, julho de 2020

| Novo item | Detalhes |
| :------- | :------ |
| Há suporte para novas distribuições. | Ubuntu 20.04 |
| Suporte para autenticação federada | Confira [Como usar o Azure Active Directory](../using-azure-active-directory.md). |
| Cache de metadados para instruções preparadas | Confira [Como usar o Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md). |
| Atributo de conexão SQL_COPT_SS_AUTOBEGINTXN para controlar se BEGIN TRANSACTION automático ocorre após ROLLBACK ou COMMIT | Confira [Atributos e palavras-chave da cadeia de conexão e DSN](../dsn-connection-string-attribute.md). |
| Correções de bugs. | [Correções de bugs](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="17522-april-2020-alpine-linux-only"></a>17.5.2.2, abril de 2020 (somente Alpine Linux)

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="1752-march-2020"></a>17.5.2, março de 2020

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte à autenticação com a Identidade Gerenciada para o Azure Key Vault | Confira [Uso do Always Encrypted com o driver ODBC](../using-always-encrypted-with-the-odbc-driver.md). |
| Compatibilidade com pontos de extremidade adicionais do Azure Key Vault | Confira [Uso do Always Encrypted com o driver ODBC](../using-always-encrypted-with-the-odbc-driver.md). |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="175-january-2020"></a>17.5, janeiro de 2020

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| O atributo de conexão SQL_COPT_SS_SPID para recuperar o SPID sem viagens de ida e volta ao servidor | Confira [Atributos e palavras-chave da cadeia de conexão e DSN](../dsn-connection-string-attribute.md). |
| Suporte para indicar a aceitação do EULA via `debconf` no Debian e Ubuntu | Confira [Instalação do Driver](./installing-the-microsoft-odbc-driver-for-sql-server.md). |
| Há suporte para novas distribuições. | &bull; &nbsp; &nbsp; Alpine Linux (3.10, 3.11)<br/>&bull; &nbsp; &nbsp; Oracle Linux 8<br/>&bull; &nbsp; &nbsp; Ubuntu 19.10<br/>&bull; &nbsp; &nbsp; macOS 10.15 |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="1742-october-2019"></a>17.4.2, outubro de 2019

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Compatibilidade com pontos de extremidade adicionais do Azure Key Vault | Confira [Uso do Always Encrypted com o driver ODBC](../using-always-encrypted-with-the-odbc-driver.md). |
| Compatibilidade com a configuração da versão de classificação de dados | Veja [Classificação de Dados](../data-classification.md#bkmk-version). |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

**Problema conhecido:**

Ao usar Always Encrypted com enclaves seguros e o Azure Key Vault, os comprimentos de caminho de chaves ímpares podem resultar em erros de verificação de assinatura CMK. Caso encontre esse problema, tente alterar o comprimento do caminho principal em um caractere ao renomear a chave AKV.

## <a name="174-august-2019"></a>17.4, agosto de 2019

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Always Encrypted com enclaves seguros. | Confira [Uso do Always Encrypted com o driver ODBC](../using-always-encrypted-with-the-odbc-driver.md). |
| Carregamento dinâmico do OpenSSL | Confira [Diretrizes de programação](programming-guidelines.md#bkmk-openssl). |
| Definições de Keep Alive de TCP configuráveis. | Confira [Conectar-se ao SQL Server](connection-string-keywords-and-data-source-names-dsns.md). |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="173-february-2019"></a>17.3, fevereiro de 2019

| Novo item | Detalhes |
| :------- | :------ |
| Há suporte para novas distribuições. | &bull; &nbsp; &nbsp; SUSE 15<br/>&bull; &nbsp; &nbsp; Ubuntu 18.10<br/>&bull; &nbsp; &nbsp; macOS 10.14 |
| Modo de autenticação de Identidade Gerenciada do Azure Active Directory (atribuída pelo usuário e pelo sistema). | Veja [Usando o Azure Active Directory com o Driver ODBC](../using-azure-active-directory.md). |
| Capacidade de transmitir parâmetros de entrada em relação a colunas Always Encrypted. | Para obter mais informações, confira [Limitações do driver ODBC ao usar Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted). |
| Transações distribuídas XA. | Veja [Usando Transações XA](../use-xa-with-dtc.md).<br/><br/>XA é o acrônimo de _eXtended Architecture_, que é um padrão para a execução de uma transação global que acessa mais de um sistema de armazenamento de dados do lado do servidor. |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2, julho de 2018

| Novo item | Detalhes |
| :------- | :------ |
| Há suporte para novas distribuições. | &bull; &nbsp; &nbsp; Ubuntu 18.04 |
| Classificação de Dados para o Banco de Dados SQL do Azure e SQL Server. | Veja [Classificação de Dados](../data-classification.md). |
| Suporte para codificação de servidor UTF-8. | &nbsp; |
| `SQLBrowseConnect` | &nbsp; |
| Dependência dinâmica de `libcurl`. | A partir desta versão, o pacote `libcurl` não é uma dependência explícita.<br/>O pacote `libcurl` para OpenSSL ou NSS é necessário ao usar a autenticação do Azure Key Vault ou do Azure Active Directory.<br/>Se você encontrar um erro em relação ao `libcurl`, verifique se ele está instalado. |
| Resiliência de Conexão Ociosa com palavras-chave ConnectRetryCount e ConnectRetryInterval na cadeia de conexão. | &bull; &nbsp; &nbsp; Use `SQL_COPT_SS_CONNECT_RETRY_COUNT` (somente leitura) para recuperar o número de tentativas de repetição de conexão.<br/><br/>&bull; &nbsp; &nbsp; Use `SQL_COPT_SS_CONNECT_RETRY_INTERVAL` (somente leitura) para recuperar a duração do intervalo de repetição de conexão.<br/><br/>Veja [Resiliência de conexão no Windows ODBC Driver](../windows/connection-resiliency-in-the-windows-odbc-driver.md). |
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

**Aprimoramentos de Desempenho**: melhoria de desempenho em mais de 10 vezes quando o driver converte para/de UTF-8/16.

**Recursos adicionados**:

Suporte a Always Encrypted para a API BCP

O novo atributo de cadeia de conexão UseFMTOnly faz driver usar metadados herdados em casos especiais que exigem tabelas temporárias.

Suporte para a Instância Gerenciada SQL do Azure. 
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

## <a name="131-for-ssnoversion-on-linux-and-macos-may-2017"></a>13.1, para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em Linux e macOS, maio de 2017

O Driver ODBC 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adiciona suporte para Always Encrypted e Azure Active Directory quando usado em conjunto com o Microsoft SQL Server 2016.

**Novas distribuições com suporte**: há suporte para OS X 10.11 e macOS 10.12 na primeira versão do Driver ODBC no macOS. Agora há suporte para Ubuntu 16.10, juntamente com o Red Hat 6, 7 e SUSE 12. Cada plataforma tem um pacote relevante para a plataforma (RPM ou DEB) para facilitar a instalação e a configuração. Para obter mais informações, confira as instruções de instalação do driver ODBC para [Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) e [macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md).

**Alterações no suporte para Gerenciador de Driver unixODBC 2.3.1**: o driver ODBC não depende mais de empacotamento personalizado para o Gerenciador de Driver unixODBC (exceto no Red Hat 6) e, em vez disso, depende do gerenciador de pacotes de distribuição para resolver a dependência do UnixODBC de repositórios de distribuição.

**Suporte à API BCP**: o driver ODBC para Linux e macOS agora dá suporte ao uso de [funções de API BCP (**bcp_init** etc.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="130-for-ssnoversion-on-linux"></a>13.0 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em Linux

Com o Microsoft ODBC Driver 13.0 for SQL Server, agora também há suporte para SQL Server 2014 e SQL Server 2016.  

**Novas distribuições com suporte**:

O Ubuntu agora tem suporte, juntamente com o Red Hat e o SUSE. Cada plataforma tem um pacote relevante para a plataforma (RPM ou DEB) para facilitar a instalação e a configuração.  Veja [Instalando o Driver](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para instruções de instalação.

**Suporte para Gerenciador de Driver unixODBC 2.3.1**: além de um gerenciador de driver mais novo, também há um pacote para instalar essa dependência que facilita a instalação e a configuração.  

**Resolução IP de Rede Transparente**: a Resolução IP de Rede Transparente é uma revisão do recurso existente de Failover de Várias Sub-Redes que afeta a sequência de conexão do driver no caso em que o primeiro IP resolvido do nome do host não responde e há vários IPs associados ao nome do host.

**Suporte a TLS 1.2**: o Microsoft ODBC Driver 13.0 para SQL Server em Linux agora dá suporte a TLS 1.2 quando são usadas comunicações seguras com o SQL Server.

## <a name="11-for-ssnoversion-on-linux"></a>11 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em Linux

O driver ODBC no SUSE Linux (visualização) oferece suporte para o SUSE Linux Enterprise 11 Service Pack 2 de 64 bits. Para obter mais informações, veja [Requisitos do sistema](../../../connect/odbc/linux-mac/system-requirements.md).  

O driver ODBC no Linux é compatível com [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para obter mais informações, veja [ODBC Driver no suporte do Linux para alta disponibilidade, recuperação de desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  

O driver ODBC no Linux é compatível com conexões com o Banco de Dados SQL do Azure.

A opção `-l` (tempo limite de logon) foi adicionada ao `bcp`. Para obter mais informações, veja [Como conectar-se com **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md).
