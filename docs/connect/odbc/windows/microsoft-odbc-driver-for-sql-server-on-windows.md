---
title: Microsoft ODBC Driver para SQL Server no Windows | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e451d6813e85def9485d738f929ff38107bb0301
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server no Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Drivers de ODBC da Microsoft para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] são drivers ODBC independentes que fornecem uma interface de programação de aplicativo (API) implementando as interfaces ODBC padrão para a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].

O Microsoft ODBC Driver for SQL Server pode ser usado para criar novos aplicativos. Você também pode atualizar seus aplicativos mais antigos que usam um driver ODBC mais antigo. O Driver ODBC para SQL Server dá suporte a conexões com o banco de dados do SQL Azure, Azure SQL Data Warehouse, 2017 do SQL Server, SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008 e SQL Server 2005.  

## <a name="summary"></a>Resumo

| Versão       | Recursos com suporte      |
| ------------- |---------------| 
| Microsoft ODBC Driver 17 para SQL Server | <ul><li>Sempre criptografado suporte para a API BCP</li><li>Novo atributo de cadeia de caracteres de conexão UseFMTONLY faz com que o driver usar metadados herdados em casos especiais que exigem a tabelas temporárias</li>
| Microsoft ODBC Driver 13.1 para SQL Server     | <ul><li>Always Encrypted</li><li>Autenticação do AD do Azure</li><li>AG (Grupos de Disponibilidade) AlwaysOn</li></ul>   | 
| Microsoft ODBC Driver 13 para SQL Server      | <ul><li>Nome de domínio internacionalizado (IDN)</li></ul> |
| Microsoft ODBC Driver 11 para SQL Server | <ul><li>Pool de conexões com reconhecimento de driver</li><li>Resiliência da conexão</li><li>Execução assíncrona (método de sondagem)</li></ul> |    

## <a name="documentation"></a>Documentação  
Esta documentação para o Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] inclui:  
  
-   [Notas de Versão](../../../connect/odbc/windows/release-notes.md)  
-   [Recursos do Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [Requisitos do sistema, instalação e arquivos de driver](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [Pooling de conexão com reconhecimento de driver no driver ODBC para SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [Exemplo de execução assíncrona &#40;método de notificação&#41](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Resiliência de conexão no driver ODBC do Windows](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [Use sempre criptografado com o Driver ODBC](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [Usando o Azure Active Directory com o Driver ODBC](../../../connect/odbc/using-azure-active-directory.md) 
-   [Usando a resolução IP de rede transparente](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>Comunidade  
- [Blog da equipe do Microsoft ODBC Driver For SQL Server](http://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server Data Access Forum](http://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>Consulte também  
- [Sobre o SQL Server Native Client](https://msdn.microsoft.com/sqlserver/ff658532.aspx)   
- [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [Perguntas frequentes do SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937707.aspx)   
- [Referência do programador ODBC](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
