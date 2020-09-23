---
title: Notas sobre a versão do JDBC Driver
description: Este artigo lista as versões do Microsoft JDBC Driver for SQL Server. Para cada versão de lançamento, as alterações são nominadas e descritas.
ms.custom: ''
ms.date: 08/27/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba891b077e6144a97dfbfcb25597e00fc43b0b0d
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89062305"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver-for-sql-server"></a>Notas sobre a versão do Microsoft JDBC Driver para SQL Server

Este artigo lista as versões do _Microsoft JDBC Driver para SQL Server_. Para cada versão de lançamento, as alterações são nominadas e descritas.

## <a name="84"></a><a id="84"></a> 8.4

**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 8.4 para SQL Server (zip)](https://go.microsoft.com/fwlink/?linkid=2137600)**  
**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 8.4 para SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2137502)**  

Número de versão: 8.4.1  
Lançado: 27 de agosto de 2020

Se precisar baixar o driver em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver em um arquivo zip: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x40a)  
Para o driver em um arquivo tar.gz: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x40a)  

### <a name="compliance"></a>Conformidade

| Alteração de conformidade | Detalhes |
| :---------------- | :------ |
| Baixe as atualizações mais recentes do JDBC Driver 8.4. | &bull; &nbsp; [GitHub, 8.4.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v8.4.1)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| Totalmente em conformidade com a especificação 4.2 de API do JDBC. | Os jars no pacote 8.4 são denominados de acordo com a compatibilidade da versão do Java.<br/><br/>Por exemplo, o arquivo mssql-jdbc-8.4.1.jre14.jar do pacote 8.4 precisa ser usado com o Java 14. |
| Compatível com JDK (Java Development Kit) versão 14.0, 11.0 e 1.8. | O Microsoft JDBC Driver 8.4 para SQL Server agora é compatível com o JDK (Java Development Kit), versão 14.0, além do JDK 11.0 e 1.8. |
| &nbsp; | &nbsp; |

### <a name="releases"></a>Versões

Número de versão: 8.4.1  
Lançado: 27 de agosto de 2020  
Problemas corrigidos:  

- Correção de um problema com o `SQLServerConnectionPoolProxy` não ser compatível com `delayLoadingLobs`
- Correção de um problema potencial `NullPointerException` com `delayLoadingLobs`
- Corrigido um problema com a descriptografia de chaves de criptografia de coluna ao usar o repositório de certificados do Windows

Número de versão: 8.4.0  
Lançado: 31 de julho de 2020  

### <a name="support-for-jdk-14"></a>Suporte para JDK 14

O Microsoft JDBC Driver 8.4 para SQL Server agora é compatível com o JDK (Java Development Kit), versão 14.0, além do JDK 11.0 e 1.8.

### <a name="added-support-for-authentication-to-azure-key-vault-using-managed-identity"></a>Adicionado suporte para autenticação para Azure Key Vault usando a Identidade Gerenciada

| Adição de tipo de autenticação | Detalhes |
| :---------- | :------ |
| O Microsoft JDBC Driver 8.4 para SQL Server agora dá suporte à autenticação para Azure Key Vault usando a Identidade Gerenciada. | Confira [Como usar Always Encrypted com o JDBC Driver](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md). |
| &nbsp; | &nbsp; |

### <a name="extended-support-for-bulk-copy-for-azure-data-warehouse"></a>Suporte estendido para cópia em massa para o Data Warehouse do Azure

| Alterações de cópia em massa para o Data Warehouse do Azure | Detalhes |
| :------------------- | :------ |
| O Microsoft JDBC Driver 8.4 adiciona uma propriedade de conexão, `sendTemporalDataTypesAsStringForBulkCopy`. Essa propriedade booliana é TRUE por padrão. | Confira [Como usar cópia em massa com o JDBC Driver](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md). |
| &nbsp; | &nbsp; |

### <a name="added-support-for-azure-sql-dns-caching"></a>Adicionado suporte para armazenamento em cache de DNS do Azure SQL

| Cache DNS | Detalhes |
| :------------------- | :------ |
| O Microsoft JDBC Driver 8.4 para SQL Server agora dá suporte ao cache DNS em SQL Servers do Azure. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="added-backwards-compatibility-for-streaming-lob-objects"></a>Adicionada compatibilidade com versões anteriores para streaming de objetos LOB

| Streaming de LOB | Detalhes |
| :------------------- | :------ |
| O Microsoft JDBC Driver 8.4 para SQL Server adiciona uma propriedade de conexão, `delayLoadingLobs`. | Configurar `delayLoadingLobs` como FALSE fará com que todos os objetos LOB recuperados do ResultSet não sejam transmitidos. Isso significa que o driver carregará todo o objeto LOB na memória de uma vez, semelhante a como o driver funcionava antes da versão 6.4. |
| &nbsp; | &nbsp; |

### <a name="added-support-for-client-certificate-authentication-for-loopback-scenarios"></a>Adicionado suporte para autenticação de certificado do cliente para cenários de loopback

| Autenticação de certificado do cliente | Detalhes |
| :------------------- | :------ |
| O Microsoft JDBC Driver 8.4 para SQL Server adicionou um novo método de autenticação chamado autenticação de certificado de cliente para cenários de loopback. | Confira [Autenticação de certificado do cliente para cenários de loopback](../../connect/jdbc/client-certification-authentication-for-loopback-scenarios.md). |

## <a name="previous-releases"></a>Versões anteriores

## <a name="82"></a><a id="82"></a> 8.2

**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 8.2 para SQL Server (zip)](https://go.microsoft.com/fwlink/?linkid=2122433)**  
**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 8.2 para SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2122536)**  

Número de versão: Lançamento da versão 8.2.2: 24 de março de 2020

Se precisar baixar o driver em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver em um arquivo zip: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x40a)  
Para o driver em um arquivo tar.gz: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x40a)  

### <a name="compliance"></a>Conformidade

| Alteração de conformidade | Detalhes |
| :---------------- | :------ |
| Baixe as atualizações mais recentes do JDBC Driver 8.2. | &bull; &nbsp; [GitHub, 8.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v8.2.2)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| Totalmente em conformidade com a especificação 4.2 de API do JDBC. | Os jars no pacote 8.2 são denominados de acordo com a compatibilidade da versão do Java.<br/><br/>Por exemplo, o arquivo mssql-jdbc-8.2.2.jre11.jar do pacote 8.2 precisa ser usado com o Java 11. |
| Compatível com JDK (Java Development Kit) versão 13.0, 11.0 e 1.8. | O Microsoft JDBC Driver 8.2 para SQL Server agora é compatível com o JDK (Java Development Kit), versão 13.0, além do JDK 11.0 e 1.8. |
| &nbsp; | &nbsp; |

### <a name="releases"></a>Versões

Número de versão: 8.2.2  
Lançado: 24 de março de 2020  
Problemas corrigidos:  

- Adicionada uma opção para configurar a lista de pontos de extremidade confiáveis do Azure Key Vault

Número de versão: 8.2.1  
Lançado: 26 de fevereiro de 2020  
Problemas corrigidos:  

- Corrigido um problema potencial de `NullPointerException` ao recuperar dados como o tipo `java.time.LocalTime` ou `java.time.LocalDate` com `SQLServerResultSet.getObject()`

Número de versão: 8.2.0  
Lançado: 31 de janeiro de 2020  

### <a name="support-for-jdk-13"></a>Suporte para JDK 13

O Microsoft JDBC Driver 8.2 para SQL Server agora é compatível com o JDK (Java Development Kit), versão 13.0, além do JDK 11.0 e 1.8.

### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted com enclaves seguros

| Alteração do Always Encrypted | Detalhes |
| :--------- | :------ |
| O Microsoft JDBC Driver 8.2 para SQL Server agora dá suporte a Always Encrypted com enclaves seguros. Os detalhes podem ser encontrados aqui: Always Encrypted com enclaves seguros. |
| Mais detalhes e código de exemplo. | Veja [Always Encrypted com enclaves seguros](../../connect/jdbc/using-always-encrypted-with-secure-enclaves-with-the-jdbc-driver.md). |
| &nbsp; | &nbsp; |

### <a name="performance-improvement-when-retrieving-temporal-datatypes-from-sql-server-sup1sup"></a>Aprimoramento do desempenho ao recuperar tipos de dados temporais do SQL Server <sup>1</sup>

| Alteração dos tipos de dados temporais | Detalhes |
| :---------- | :------ |
| O Microsoft JDBC Driver 8.2 para SQL Server aprimorou o desempenho ao recuperar tipos de dados temporais do SQL Server. | Essa alteração elimina conversões de tipo de dados temporais desnecessárias acabando com o uso de java.util.Calendar sempre que possível. |
| Veja a seguir uma lista dos tipos de dados temporais que foram afetados por esse aprimoramento de desempenho; no formato tipo de dados do SQL Server seguido pelo respectivo mapeamento de Java. | date (java.sql.Date), datetime (java.sql.Timestamp), datetime2 (java.sql.Timestamp), smalldatetime (java.sql.Timestamp) e time (java.sql.Time). |
| &nbsp; | &nbsp; |

<sup>1</sup> Devido às diferenças na maneira como os fusos horários são tratados entre a API java.util.Calendar e java.time.LocalDateTime, os tipos de dados temporais com um objeto java.util.Calendar fornecido pelo usuário associado a ele ou tipos de dados microsoft.sql.DateTimeOffset não se beneficiam desse aprimoramento.

### <a name="deployment-of-mssql-jdbc_auth-version-archdll-previously-sqljdbc_authdll-to-maven-repository"></a>Implantação de mssql-jdbc_auth-\<version>-\<arch>.dll (anteriormente sqljdbc_auth.dll) no Repositório Maven

| Alteração de sqljdbc_auth.dll | Detalhes |
| :------------------- | :------ |
| Do Microsoft JDBC Driver 8.2 para SQL Server em diante, o driver depende de mssql-jdbc_auth-\<version>-\<arch>.dll em vez de sqljdbc_auth.dll para usar o recurso de Autenticação do Azure Active Directory. | &nbsp; |
| A DLL também foi carregada para o repositório Maven para facilitar o acesso. | Confira [esta página](https://search.maven.org/artifact/com.microsoft.sqlserver/mssql-jdbc_auth). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

| Problemas conhecidos | Detalhes |
| :----------- | :------ |
| Ao usar o Always Encrypted com enclaves seguros com o Java 8. | Os usuários devem incluir o Provedor BouncyCastle como uma dependência OU mapear/carregar um provedor de segurança que dá suporte ao algoritmo de assinatura RSASSA-PSS. |
| &nbsp; | &nbsp; |

## <a name="a-id74-741"></a><a id="74"> 7.4.1

**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 7.4.1 para SQL Server (exe com extração automática)](https://go.microsoft.com/fwlink/?linkid=2122712)**  
**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 7.4.1 para SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2122613)**  

Número de versão: 7.4.1  
Lançado: 2 de agosto de 2019

Se precisar baixar o driver em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver em um arquivo exe com extração automática: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x40a)  
Para o driver em um arquivo tar.gz: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x40a)  

### <a name="compliance"></a>Conformidade

| Alteração de conformidade | Detalhes |
| :---------------- | :------ |
| Baixe as atualizações mais recentes do JDBC Driver 7.4. | &bull; &nbsp; [GitHub, 7.4.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.4.1)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| Totalmente em conformidade com a especificação 4.2 de API do JDBC. | Os jars no pacote 7.4 são denominados de acordo com a compatibilidade da versão do Java.<br/><br/>Por exemplo, o arquivo mssql-jdbc-7.4.1.jre11.jar do pacote 7.4 precisa ser usado com o Java 11. |
| Compatível com JDK (Java Development Kit) versão 12.0, 11.0 e 1.8. | O Microsoft JDBC Driver 7.4 para SQL Server é agora compatível com o JDK (Java Development Kit), versão 12.0, além do JDK 11.0 e 1.8. |
| &nbsp; | &nbsp; |

### <a name="releases"></a>Versões

Número de versão: 7.4.1  
Lançado: 2 de agosto de 2019  
Problemas corrigidos:  

- Novas implementações de API `equals()` e `hashCode()` revertidas de `SQLServerDataTable` e `SQLServerDataColumn`, pois a alteração da API interrompeu a compatibilidade com versões anteriores

Número de versão: 7.4.0  
Lançado: 31 de julho de 2019  

### <a name="support-for-jdk-12"></a>Suporte para JDK 12

O Microsoft JDBC Driver 7.4 para SQL Server é agora compatível com o JDK (Java Development Kit), versão 12.0, além do JDK 11.0 e 1.8.

### <a name="introduces-ntlm-authentication"></a>Introduz a autenticação NTLM

| Alteração de NTLM | Detalhes |
| :--------- | :------ |
| É compatível com a autenticação NTLM. | Esse modo de autenticação permite que clientes Windows e não Windows se autentiquem no SQL Server com usuários de domínio do Windows. |
| Confira mais detalhes e um aplicativo de exemplo para usar esse modo de autenticação. | Confira [Como se conectar usando a autenticação NTLM](using-ntlm-authentication-to-connect-to-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="introduces-querying-parametermetadata-via-_usefmtonly_"></a>Introduz a consulta ParameterMetaData por meio de _useFmtOnly_

| Alteração useFmtOnly | Detalhes |
| :---------- | :------ |
| Propriedade de conexão **useFmtOnly** adicionada. | Esse recurso permite que os usuários consultem opcionalmente o ParameterMetaData por meio da API herdada `SET FMTONLY ON`. Isso é útil para cenários em que o `sp_describe_undeclared_parameters` não é executado conforme o esperado. |
| Mais detalhes e limitações. | Confira [Como usar o useFmtOnly](using-usefmtonly.md) |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-key-vault-sdk-for-java_-version-121"></a>Foi atualizado o _SDK do Microsoft Azure Key Vault para Java_, versão 1.2.1

| Alteração no SDK do Key Vault | Detalhes |
| :------------------- | :------ |
| A dependência Maven no _SDK do Microsoft Azure Key Vault para Java_ foi atualizada para a versão 1.2.1. | &nbsp; |
| Remove o _SDK do Microsoft Azure para Key Vault WebKey_ como uma dependência Maven. | &nbsp; |
| Detalhes adicionais. | Confira [Dependências de recurso do Microsoft JDBC Driver para SQL Server](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

| Problemas conhecidos | Detalhes |
| :----------- | :------ |
| Ao usar a Autenticação NTLM. | No momento, não é possível habilitar a Proteção Estendida e as conexões criptografadas ao mesmo tempo. |
| Ao usar o useFmtOnly. | Há alguns problemas com o recurso, causados por deficiências na lógica de análise do SQL. Confira [Como usar useFmtOnly](using-usefmtonly.md) para obter mais detalhes e sugestões de solução alternativa. |
| &nbsp; | &nbsp; |

## <a name="a-id72-722"></a><a id="72"> 7.2.2

**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 7.2.2 para SQL Server (exe com extração automática)](https://go.microsoft.com/fwlink/?linkid=2122435)**  
**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 7.2.2 para SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2122434)**  

Número de versão: 7.2.2  
Lançado: 16 de abril de 2019

Se precisar baixar o driver em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver em um arquivo exe com extração automática: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x40a)  
Para o driver em um arquivo tar.gz: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x40a)  

### <a name="compliance"></a>Conformidade

| Alteração de conformidade | Detalhes |
| :---------------- | :------ |
| Baixe as atualizações mais recentes do JDBC Driver 7.2. | &bull; &nbsp; [GitHub, 7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| Totalmente em conformidade com a especificação 4.2 de API do JDBC. | Os jars no pacote 7.2 são denominados de acordo com a compatibilidade da versão do Java.<br/><br/>Por exemplo, o arquivo mssql-jdbc-7.2.2.jre11.jar do pacote 7.2 deve ser usado com o Java 11. |
| Compatível com JDK (Java Development Kit) versão 11.0, além de JDK 1.8. | O Microsoft JDBC Driver 7.2 para SQL Server é agora compatível com o JDK (Java Development Kit), versão 11.0, além do JDK 1.8. |
| &nbsp; | &nbsp; |

### <a name="releases"></a>Versões

Número de versão: 7.2.2  
Lançado: 16 de abril de 2019  
Problemas corrigidos:  

- Corrigidos problemas em que ActivityIDs não eram limpas adequadamente

Número de versão: 7.2.1  
Lançado: 11 de fevereiro de 2019  
Problemas corrigidos:  

- Corrigidos problemas de análise com determinadas consultas parametrizadas

Número de versão: 7.2.0  
Lançado: 31 de janeiro de 2019  

### <a name="active-directory-_managed-identity_-msi-authentication"></a>Autenticação de _Identidade Gerenciada_ do Active Directory (MSI)

| Alteração da MSI | Detalhes |
| :--------- | :------ |
| Dá suporte ao modo de autenticação da Identidade Gerenciada (MSI) do Active Directory. | Esse modo de autenticação aplica-se aos Recursos do Azure com suporte para o recurso "Identidade" habilitado.<br/><br/>Ambos os tipos de Identidades Gerenciadas (MSI) têm suporte do driver para adquirir o **accessToken** a fim de estabelecer uma conexão segura. |
| Confira mais detalhes e um aplicativo de exemplo para usar esse modo de autenticação. | Confira [Como se conectar usando a autenticação do Azure Active Directory](connecting-using-azure-active-directory-authentication.md). |
| &nbsp; | &nbsp; |

### <a name="introduces-_open-service-gateway-initiative_-osgi-support"></a>Introduz o suporte à _Open Service Gateway Initiative_ (OSGi)

| Alteração na OSGi | Detalhes |
| :---------- | :------ |
| A implementação **DataSourceFactory** foi adicionada. | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| A implementação **Activator** foi adicionada. | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-_sqlservererror_-apis"></a>Introduz as APIs _SQLServerError_

| Alteração da API de erro | Detalhes |
| :--------------- | :------ |
| A API SQLServerError foi introduzida. | APIs getter para recuperar detalhes adicionais a respeito do erro gerado pelo servidor.<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| Detalhes adicionais. | Confira [Como tratar erros](handling-errors.md). |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-active-directory-authentication-library-adal4j-for-java_-version-163"></a>A versão 1.6.3 da _ADAL4J (Biblioteca de Autenticação do Microsoft Azure Active Directory) para Java_ foi atualizada

| Alteração da ADAL4J | Detalhes |
| :------------ | :------ |
| A dependência Maven no ADAL4J foi atualizada para a versão 1.6.3. | &nbsp; |
| Introduz o _Runtime do cliente Java para AutoRest_ como uma dependência Maven, versão 1.6.5. | &nbsp; |
| Detalhes adicionais. | Confira [Dependências de recurso do Microsoft JDBC Driver para SQL Server](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-key-vault-sdk-for-java_-version-120"></a>Foi atualizado o _SDK do Microsoft Azure Key Vault para Java_, versão 1.2.0

| Alteração no SDK do Key Vault | Detalhes |
| :------------------- | :------ |
| A dependência Maven no _SDK do Microsoft Azure Key Vault para Java_ foi atualizada para a versão 1.2.0. | &nbsp; |
| Introduz o _SDK do Microsoft Azure para Key Vault WebKey_ como uma dependência Maven, versão 1.2.0. | &nbsp; |
| Detalhes adicionais. | Confira [Dependências de recurso do Microsoft JDBC Driver para SQL Server](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos

| Problemas conhecidos | Detalhes |
| :----------- | :------ |
| Consultas parametrizadas, em determinados casos. | Uma atualização da versão 7.2.0, a v7.2.1, foi lançada em fevereiro de 2019 para resolver esse problema. |
| Limpeza de ActivityIds. | Uma atualização da versão 7.2.1, a v7.2.2, foi lançada em abril de 2019 para resolver esse problema. |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 7.0 para SQL Server (exe com extração automática)](https://go.microsoft.com/fwlink/?linkid=2122713)**  
**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 7.0 para SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2122614)**  

Número de versão: 7.0.0  
Lançado: 31 de julho de 2018

Se precisar baixar o driver em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver em um arquivo exe com extração automática: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x40a)  
Para o driver em um arquivo tar.gz: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x40a)  

O Microsoft JDBC Driver 7.0 para SQL Server está totalmente em conformidade com a especificação 4.2 da API do JDBC. Os jars no pacote 7.0 são denominados de acordo com a compatibilidade da versão do Java. Por exemplo, o arquivo mssql-jdbc-7.0.0.jre10.jar do pacote 7.0 deve ser usado com o Java 10.

### <a name="support-for-jdk-10"></a>Suporte para JDK 10

O Microsoft JDBC Driver 7.0 para SQL Server é agora compatível com o JDK (Java Development Kit), versão 10.0, além do JDK 1.8. Essa atualização também expõe o `Automatic-Module-Name` do driver como `com.microsoft.sqlserver.jdbc` por meio de seu arquivo de manifesto.

### <a name="support-for-spatial-datatypes"></a>Suporte para tipos de dados espaciais

O Microsoft JDBC Driver 7.0 para SQL Server agora oferece suporte a tipos de dados espaciais de Geografia e Geometria do SQL Server. Para saber mais sobre as APIs de tipo de dados espaciais e como usá-las, confira [Como usar tipos de dados espaciais](use-spatial-datatypes.md).

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>A implementação para JDBC 4.3 introduziu as APIs beginRequest() e endRequest() do java.sql.Connection.

O Microsoft JDBC Driver 7.0 para SQL Server agora implementa as APIs `beginRequest()` e `endRequest()` da classe `java.sql.Connection`. Essas APIs foram introduzidas com as especificações do JDBC 4.3 e JDK 9. Para saber mais sobre a implementação do driver dessas APIs, confira [Conformidade do JDBC 4.3 para o JDBC Driver](jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="support-for-sql-data-discovery-and-classification"></a>Suporte para classificação e descoberta de dados SQL

O Microsoft JDBC Driver 7.0 para o SQL Server dá suporte para a descoberta e classificação de dados SQL em qualquer banco de dados de destino que dê suporte a esse recurso. O driver agora expõe as APIs `SQLServerResultSet.getSensitivityClassification()` para extrair essas informações do `ResultSet` buscado.

Para saber mais sobre como usar esse recurso com o JDBC Driver, confira o exemplo em [Descoberta e classificação de dados SQL](data-discovery-classification-sample.md).

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>Foi adicionada a propriedade de conexão: useBulkCopyForBatchInsert

O Microsoft JDBC Driver 7.0 para SQL Server apresenta uma nova propriedade de conexão, `useBulkCopyForBatchInsert`. Essa propriedade tem suporte apenas para o SQL Data Warehouse do Microsoft Azure.

Essa propriedade fica desabilitada por padrão. É possível habilitá-la para aumentar o desempenho de aplicativos do usuário ao enviar uma grande quantidade de dados para o SQL Data Warehouse do Microsoft Azure. Habilitar essa propriedade altera o comportamento das operações de inserção de lotes, alternando para operações de cópia em massa com os dados fornecidos pelo usuário. Para saber mais sobre essa propriedade e suas limitações, confira como [usar a API de cópia em massa para a operação de inserção de lote](use-bulk-copy-api-batch-insert-operation.md).

### <a name="added-connection-property-cancelquerytimeout"></a>Foi adicionada a propriedade de conexão: cancelQueryTimeout

O Microsoft JDBC Driver 7.0 para SQL Server apresenta uma nova propriedade de conexão, `cancelQueryTimeout`, para cancelar `queryTimeout` em objetos `java.sql.Connection` e `java.sql.Statement`.

### <a name="added-azure-key-vault-provider-constructors"></a>Foram adicionados construtores do Azure Key Vault Provider

O Microsoft JDBC Driver 7.0 para SQL Server reintroduz um construtor removido anteriormente, para `SQLServerColumnEncryptionAzureKeyVaultProvider`. Ele permitia a autenticação por meio de um método personalizado, implementado sobre `SQLServerKeyVaultAuthenticationCallback` para buscar um token de acesso.

Os novos construtores têm a seguinte definição:

```java
/* This constructor is added to provide backward compatibility with 6.0
* version of the driver. It is marked deprecated for removal in the next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>A versão "ADAL4J (Biblioteca de Autenticação do Microsoft Azure Active Directory) para Java" foi atualizada: 1.6.0

A dependência Maven do Microsoft JDBC Driver 7.0 para SQL Server foi atualizada para a versão 1.6.0 na "Biblioteca de Autenticação do Active Directory (ADAL4J) do Microsoft Azure para Java”. Para saber mais, confira [Dependências de recurso do Microsoft JDBC Driver para SQL Server](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="64"></a>6.4

**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 6.4 para SQL Server (exe com extração automática)](https://go.microsoft.com/fwlink/?linkid=2122436)**  
**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 6.4 para SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2122537)**  

Número de versão: 6.4.0  
Lançado: 27 de fevereiro de 2018

Se precisar baixar o driver em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver em um arquivo exe com extração automática: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x40a)  
Para o driver em um arquivo tar.gz: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x40a)  

O Microsoft JDBC Driver 6.4 para SQL Server está totalmente em conformidade com as especificações 4.1 e 4.2 do JDBC. Os jars no pacote 6.4 são denominados de acordo com a compatibilidade da versão do Java. Por exemplo, o arquivo mssql-jdbc-6.4.0.jre8.jar do pacote 6.4 deve ser usado com o Java 8.

### <a name="support-for-jdk-9"></a>Suporte para JDK 9

O driver dá suporte à versão 9.0 do JDK, além do JDK 8.0 e 7.0.

### <a name="jdbc-43-compliance"></a>Conformidade com o JDBC 4.3

O driver é compatível com a especificação da API Java Database Connectivity 4.3, além da 4.1 e da 4.2. Os métodos da API do JDBC 4.3 foram adicionados, mas ainda não foram implementados. Para obter detalhes, confira [Conformidade do JDBC 4.3 com o JDBC Driver](jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="added-connection-property-sslprotocol"></a>Foi adicionada a propriedade de conexão: sslProtocol

Uma nova propriedade de conexão permite aos usuários especificar a palavra-chave do protocolo TLS. Os valores possíveis são: "TLS", "TLSv1", "TLSv1.1" e "TLSv1.2". Para obter detalhes, confira o [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol).

### <a name="deprecated-connection-property-fipsprovider"></a>Propriedade de conexão preterida: fipsProvider

A propriedade de conexão `fipsProvider` foi removida da lista de propriedades de conexão aceitas. Para obter detalhes, confira a [solicitação de pull no GitHub](https://github.com/Microsoft/mssql-jdbc/pull/460) relacionada.

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>Foram adicionadas propriedades de conexão para especificar um TrustManager personalizado

O driver agora dá suporte à especificação de um TrustManager personalizado com as propriedades de conexão `trustManagerClass` e `trustManagerConstructorArg` adicionadas. É possível especificar dinamicamente um conjunto de certificados que são confiáveis de acordo com a conexão, sem modificar as configurações globais do ambiente da máquina virtual Java (JVM).

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>Foi adicionado o suporte para datetime/smallDatetime nos parâmetros com valor de tabela

O driver agora dá suporte aos tipos de dados `datetime` e `smallDatetime` ao usar parâmetros com valor de tabela (TVPs).

### <a name="added-support-for-the-sql_variant-datatype"></a>Foi adicionado o suporte para o tipo de dados sql_variant

O JDBC Driver agora dá suporte aos tipos de dados `sql_variant` a serem usados com o SQL Server. Há também suporte para o tipo de dado `sql_variant` com recursos como TVPs e cópia em massa, com as seguintes limitações:

* **Para valores de data**:

  Ao usar um TVP para preencher uma tabela que contém valores `datetime`, `smalldatetime` ou `date`, armazenados em uma coluna `sql_variant`, a chamada dos método `getDateTime()`, `getSmallDateTime()` ou `getDate()` no conjunto de resultados não vai funcionar e vai gerar a seguinte exceção:

  `java java.lang.String cannot be cast to java.sql.Timestamp`

  Como solução alternativa, em vez disso, use o método `getString()` ou `getObject()`.

* **Usando um TVP com sql_variant para valores nulos**:
  
  Se estiver usando um TVP para preencher uma tabela e enviar um valor NULL ao tipo de coluna `sql_variant`, você vai se deparar com uma exceção. Atualmente não há suporte para a inserção de um valor NULL com o tipo de coluna `sql_variant` em um TVP.

### <a name="implemented-prepared-statement-metadata-caching"></a>Foi implementado o armazenamento em cache de metadados de instrução preparados

O JDBC Driver implementou o armazenamento em cache de metadados de instrução preparados para melhorar o desempenho. O driver agora dá suporte ao armazenamento em cache de metadados de instrução preparados no driver com as propriedades de conexão `disableStatementPooling` e `statementPoolingCacheSize`. Por padrão, esse recurso está desabilitado. Para saber mais, confira [Armazenamento em cache de metadados de instrução preparados para o JDBC Driver](prepared-statement-metadata-caching-for-the-jdbc-driver.md).

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmacos"></a>Foi adicionado o suporte à Autenticação Integrada do Azure AD no Linux/macOS

O JDBC Driver agora dá suporte à Autenticação Integrada do Azure AD (Azure Active Directory) em todos os sistemas operacionais compatíveis (Windows, Linux e macOS) com Kerberos. Como alternativa, nos sistemas de operacionais Windows, os usuários podem autenticar com mssql-jdbc_auth-\<version>-\<arch>.dll.

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>A versão "ADAL4J (Biblioteca de Autenticação do Microsoft Azure Active Directory) para Java" foi atualizada: 1.4.0

A dependência Maven do Microsoft JDBC Driver foi atualizada para a versão 1.4.0 na "Biblioteca de Autenticação do Active Directory (ADAL4J) do Microsoft Azure para Java”. Para saber mais, confira [Dependências de recurso do Microsoft JDBC Driver para SQL Server](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="62"></a>6.2

**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 6.2 para SQL Server (exe com extração automática)](https://go.microsoft.com/fwlink/?linkid=2122616)**  
**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 6.2 para SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2122615)**  

Número de versão: 6.2.2  
Lançado: 29 de setembro de 2017

Se precisar baixar o driver em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver em um arquivo exe com extração automática: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x40a)  
Para o driver em um arquivo tar.gz: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x40a)  

O Microsoft JDBC Driver 6.2 para SQL Server está totalmente em conformidade com as especificações 4.1 e 4.2 do JDBC. Os jars no pacote 6.2 são denominados de acordo com a compatibilidade da versão do Java. Por exemplo, recomendamos que o arquivo mssql-jdbc-6.2.2.jre8.jar do pacote 6.2 seja usado com o Java 8.

### <a name="releases"></a>Versões

Número de versão: 6.2.2  
Lançado: 3 de outubro de 2017  
Problemas corrigidos:  

- Atualizada a dependência do ADAL4J para a versão 1.2.0 e a dependência do Azure Key Vault para a versão 1.0.0

Número de versão: 6.2.1  
Lançado: 14 de julho de 2017  
Problemas corrigidos:  

- Corrigido um problema ao executar consultas sem parâmetros usando `preparedStatement`

Número de versão: 6.2.0  
Lançado: 30 de junho de 2017  

> [!NOTE]  
> Foi encontrado um problema com a melhoria do armazenamento em cache de metadados na RTW do JDBC 6.2, lançada em 29 de junho de 2017. A melhoria foi revertida e novos jars (versão 6.2.1) foram lançados em 17 de julho de 2017.
>
> Outra melhoria atualizou a versão da biblioteca dependente do Azure Key Vault para 1.0.0, e novos jars (versão 6.2.2) foram lançados em 19 de outubro de 2017.
>
> Baixe as atualizações mais recentes do JDBC Driver 6.2 pelos links acima, no [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) ou na [Central do Maven](https://search.maven.org/search?q=g:com.microsoft.sqlserver). Atualize seus projetos a fim de usar os jars da versão 6.2.2. Para saber mais, confira as notas sobre as versões [6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) e [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2).

### <a name="azure-ad-support-for-linux"></a>Suporte do Azure AD para Linux

Conecte seus aplicativos Linux ao banco de dados SQL do Azure usando a autenticação do Azure AD por meio de métodos de token de acesso, nome de usuário/senha.

### <a name="fips-enabled-jvms"></a>JVMs habilitadas para FiPS

O JDBC Driver agora pode ser usado em JVMs que são executados no modo de conformidade 140 da FIPS (Federal Information Processing Standard) para atender aos padrões federais de conformidade.

### <a name="kerberos-authentication-improvements"></a>Melhorias na autenticação Kerberos

O JDBC Driver agora tem suporte para:

* Método de senha/entidade de segurança para aplicativos em que a configuração Kerberos não pode ser modificada ou em que não é possível recuperar um novo token ou keytab. Esse método pode ser usado para realizar a autenticação em uma instância do SQL Server que permita apenas a autenticação Kerberos.
* Autenticação entre realms que usa a Autenticação Integrada Kerberos sem configurar de forma explícita o servidor SPN. O driver agora calcula automaticamente o realm, mesmo quando ele não é fornecido.
* Delegação Restrita de Kerberos ao aceitar credenciais de usuário representado como um objeto de credencial GSS por meio da fonte de dados. Essa credencial representada é usada para estabelecer uma conexão Kerberos.

### <a name="added-timeouts"></a>Foram adicionados tempos limite

O JDBC Driver agora dá suporte aos seguintes tempos limite configuráveis. É possível alterá-los com base nas necessidades do seu aplicativo.

* Tempo limite da consulta para controlar o número de segundos a aguardar antes que ocorra um tempo limite quando você está executando uma consulta.
* Tempo limite para soquete a fim de especificar o número de milissegundos a aguardar antes que ocorra um tempo limite na leitura ou aceitação de um soquete.

## <a name="61"></a>6.1

Número de versão: 6.1.0  
Lançado: 17 de novembro de 2016  

O Microsoft JDBC Driver 6.1 para SQL Server está totalmente em conformidade com as especificações 4.1 e 4.2 do JDBC. Esta é a versão inicial de software livre do JDBC Driver. O código-fonte pode ser encontrado na [Marca do GitHub v6.1.0](https://github.com/microsoft/mssql-jdbc/releases/tag/v6.1.0). Ela compila os arquivos mssql-jdbc-6.1.0.jre8.jar e mssql-jdbc-6.1.0.jre7.jar, que correspondem à compatibilidade de versão do Java.

## <a name="60"></a>6,0

**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 6.0 para SQL Server (exe com extração automática)](https://go.microsoft.com/fwlink/?linkid=2122617)**  
**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 6.0 para SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2122714)**  

Número de versão: 6.0.8112  
Lançado: 17 de janeiro de 2017

Se precisar baixar o driver em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver em um arquivo exe com extração automática: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x40a)  
Para o driver em um arquivo tar.gz: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x40a)  

O Microsoft JDBC Driver 6.0 para SQL Server está totalmente em conformidade com as especificações 4.1 e 4.2 do JDBC. Os jars no pacote 6.0 são denominados de acordo com a conformidade deles com a versão da API do JDBC. Por exemplo, o arquivo sqljdbc42.jar, do pacote 6.0, está em conformidade com a API 4.2 do JDBC. Da mesma forma, o arquivo sqljdbc41.jar está em conformidade com a API 4.1 do JDBC.

Para ter certeza que você tem o arquivo sqljdbc41.jar ou sqljdbc42.jar correto, execute as seguintes linhas de código. Se a saída for "versão do driver: 6.0.7507.100", você terá o pacote JDBC Driver 6.0.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

O driver dá suporte ao recurso Always Encrypted no SQL Server 2016. Esse recurso garante que os dados confidenciais nunca sejam vistos em texto não criptografado em uma instância do SQL Server. O Always Encrypted funciona pela criptografia transparente de dados no aplicativo, de forma que o SQL Server apenas manipulará os dados criptografados e os valores de texto não criptografado. Mesmo se a instância do SQL Server ou o computador host estiverem comprometidos, o invasor apenas poderá obter um texto cifrado de dados confidenciais. Para obter detalhes, veja [Uso de Always Encrypted com o driver JDBC em Linux](using-always-encrypted-with-the-jdbc-driver.md).

### <a name="internationalized-domain-names"></a>Nomes de domínio internacionalizados

O driver dá suporte a nomes de domínio internacionalizados (IDNs) para nomes de servidor. Para obter detalhes, confira as informações sobre o "uso de nomes de domínio internacionais" no artigo [Recursos internacionais do JDBC Driver](international-features-of-the-jdbc-driver.md).

### <a name="parameterized-queries"></a>Consultas parametrizadas

O driver agora é compatível com a recuperação de metadados de parâmetro com instruções preparadas para consultas complexas, como subconsultas e/ou junções. Observe que essa melhoria está disponível apenas no SQL Server 2012 e nas versões mais recentes.

### <a name="azure-active-directory"></a>Azure Active Directory

A Autenticação do Azure AD é um mecanismo de conexão com o Banco de Dados SQL v12 do Azure usando identidades no Azure AD. Use a autenticação do Azure AD para gerenciar de forma centralizada as identidades de usuários do banco de dados e como uma alternativa à autenticação do SQL Server.

É possível usar o JDBC Driver 6.0 para especificar as credenciais do Azure AD na cadeia de conexão do JDBC para se conectar ao Banco de Dados SQL do Azure. Para obter detalhes, consulte a propriedade de autenticação no artigo [Definindo as propriedades de conexão](setting-the-connection-properties.md).

### <a name="table-valued-parameters"></a>Parâmetros com valor de tabela

Os TVPs fornecem uma maneira fácil de realizar marshaling em várias linhas de dados de um aplicativo cliente do SQL Server sem exigir várias viagens de ida e volta ou uma lógica especial do lado do servidor para processar os dados. Você pode usar os TVPs para encapsular linhas de dados em um aplicativo cliente e enviar os dados para o servidor em um único comando parametrizado. As linhas de dados de entrada são armazenadas em uma variável de tabela, as quais você poderá operar usando o Transact-SQL. Para obter detalhes, confira as informações sobre o [uso de parâmetros com valor de tabela](using-table-valued-parameters.md).

### <a name="always-on-availability-groups"></a>Grupos de Disponibilidade AlwaysOn

O driver agora dá suporte a conexões transparentes para os Grupos de Disponibilidade AlwaysOn. O driver descobre rapidamente a topologia Always On atual da infraestrutura de servidor e conecta-se ao servidor ativo atual de maneira transparente.

## <a name="42"></a>4.2

**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 4.2 para SQL Server (exe com extração automática)](https://go.microsoft.com/fwlink/?linkid=2122538)**  
**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 4.2 para SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2122437)**  

Número de versão: 4.2.8112  
Lançado: 24 de agosto de 2015

Se precisar baixar o driver em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver em um arquivo exe com extração automática: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x40a)  
Para o driver em um arquivo tar.gz: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x40a)  

O Microsoft JDBC Driver 4.2 para SQL Server está totalmente em conformidade com as especificações 4.1 e 4.2 do JDBC. Os jars no pacote 4.2 são denominados de acordo com a conformidade deles com a versão da API do JDBC. Por exemplo, o arquivo sqljdbc42.jar do pacote 4.2 está em conformidade com a API 4.2 do JDBC. Da mesma forma, o arquivo sqljdbc41.jar está em conformidade com a API 4.1 do JDBC.

Para ter certeza que você tem o arquivo sqljdbc42.jar ou sqljdbc41.jar correto, execute as seguintes linhas de código. Se a saída for "versão do driver: 4.2.6420.100", você terá o pacote JDBC Driver 4.2.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>Suporte para JDK 8

O driver dá suporte à versão 8.0 do JDK, além do JDK 7.0, 6.0 e 5.0.

### <a name="jdbc-41-and-42-compliance"></a>Conformidade do JDBC 4.1 e 4.2

O driver é compatível com as especificações da API Java Database Connectivity 4.1 e 4.2, além da 4.0. Para obter detalhes, confira a [conformidade com o JDBC 4.1 para o JDBC Driver](jdbc-4-1-compliance-for-the-jdbc-driver.md) e a [conformidade com o JDBC 4.2 para o JDBC Driver](jdbc-4-2-compliance-for-the-jdbc-driver.md).

### <a name="bulk-copy"></a>Cópia em massa

Você pode usar o recurso de cópia em massa para copiar rapidamente grandes quantidades de dados em tabelas ou em exibições nos bancos de dados do SQL Server. Para obter detalhes, confira [Usando uma cópia em massa com o JDBC Driver](using-bulk-copy-with-the-jdbc-driver.md).

### <a name="xa-transaction-rollback-option"></a>Opção de reversão de transação XA

O driver tem novas opções de tempo limite para reversão automática existente de transações não preparadas. Para obter detalhes, veja como [compreender as transações XA](understanding-xa-transactions.md).

### <a name="new-kerberos-principal-connection-property"></a>Nova propriedade de conexão principal Kerberos

O driver usa uma nova propriedade de conexão para facilitar a flexibilidade com conexões Kerberos. Para obter detalhes, confira [Usando a autenticação integrada Kerberos para conectar-se ao SQL Server](using-kerberos-integrated-authentication-to-connect-to-sql-server.md).

## <a name="41"></a>4.1

Número de versão: 4.1.8112  
Lançado: 12 de dezembro de 2014

### <a name="support-for-jdk-7"></a>Suporte para JDK 7

O driver dá suporte à versão 7.0 do JDK, além do JDK 6.0 e 5.0.

## <a name="itanium-not-supported-for-jdbc-driver-applications"></a>O Itanium não tem suporte em aplicativos do JDBC Driver

Não há suporte para execução de aplicativos do Microsoft JDBC Driver para SQL Server em um computador Itanium.

## <a name="see-also"></a>Confira também

[Visão geral do JDBC Driver](overview-of-the-jdbc-driver.md)
