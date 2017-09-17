---
title: Microsoft ODBC Driver para SQL Server | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9f2ae91b-06af-4c9a-9d24-062df7bc4662
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e867bb283434a6a7ae515823b370c73e4df4e131
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

![Um círculo seta download](../../ssdt/media/download.png)[para baixar o driver ODBC](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ODBC é a API de acesso primário dados nativos para aplicativos escritos em C e C++ para o SQL Server. Há um driver ODBC para a maioria das fontes de dados. Outros idiomas que usam o ODBC incluem COBOL, Perl, PHP e Python. ODBC é amplamente usado em cenários de integração de dados.

O driver ODBC é fornecido com ferramentas como [ **sqlcmd** ](https://msdn.microsoft.com/library/ms162773.aspx) e [ **bcp**](https://msdn.microsoft.com/library/ms162802.aspx). O **sqlcmd** utilitário permite que você execute instruções Transact-SQL, procedimentos do sistema e scripts SQL. O **bcp** copia dados entre uma instância do Microsoft SQL Server e um arquivo de dados em um formato que você escolher. Você pode usar **bcp** para importar novo número de linhas em tabelas do SQL Server ou para exportar dados de tabelas para arquivos de dados.  

## <a name="code-example-in-c"></a>Exemplo de código em C++

Temos um arquivo. zip pequeno que contém o código-fonte de um programa C++ que usa ODBC:

- [Exemplo de código C++, usando o ODBC](../../odbc/reference/sample-odbc-program.md)

## <a name="download"></a>Download

- ![Um círculo seta download](../../ssdt/media/download.png)[para baixar o driver ODBC](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

## <a name="documentation"></a>Documentação  

### <a name="linux-and-macos"></a>Linux e macOS

- [Instalação do Driver](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Conectando com **bcp**](../../connect/odbc/linux-mac/connecting-with-bcp.md)
- [Conectando com **sqlcmd**](../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)
- [Usando a autenticação integrada (Kerberos)](../../connect/odbc/linux-mac/using-integrated-authentication.md)
- [Palavras-chave de cadeia de caracteres de Conexão e nomes de fonte de dados](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)
- [Rastreamento de acesso a dados](../../connect/odbc/linux-mac/data-access-tracing-with-the-odbc-driver-on-linux.md)
- [Perguntas frequentes](../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)
- [Instalando o Gerenciador de Driver](../../connect/odbc/linux-mac/installing-the-driver-manager.md)
- [Problemas conhecidos](../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)
- [Diretrizes de programação](../../connect/odbc/linux-mac/programming-guidelines.md)
- [Notas de versão](../../connect/odbc/linux-mac/release-notes.md)
- [Suporte para alta disponibilidade e recuperação de desastres](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)

### <a name="windows"></a>Windows

- [Exemplo de execução assíncrona (método de notificação)](../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)
- [Resiliência de conexão no driver ODBC do Windows](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
- [Pool de conexões com reconhecimento de driver](../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)
- [Recursos e alterações de comportamento](../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)
- [Notas de versão](../../connect/odbc/windows/release-notes.md)
- [Requisitos do sistema, instalação e arquivos de driver](../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)

### <a name="features"></a>Recursos

- [Provedores de armazenamento de chaves personalizado](../../connect/odbc/custom-keystore-providers.md)
- [SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md) (os recursos disponíveis também se aplicam, sem OLEDB, o driver ODBC para SQL Server)
- [Usar sempre criptografado](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [Usando o Active Directory do Azure](../../connect/odbc/using-azure-active-directory.md)
- [Usando a resolução IP de rede transparente](../../connect/odbc/using-transparent-network-ip-resolution.md)

## <a name="community"></a>Comunidade  
- [Blog da equipe do Microsoft ODBC Driver For SQL Server](http://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server Data Access Forum](http://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  

