---
title: Microsoft ODBC Driver for SQL Server no Windows | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31688509bb7c7592da29ef51535029e1251ffd44
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921104"
---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server no Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Os Microsoft ODBC Drivers para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são drivers ODBC independentes que fornecem uma API (interface de programação de aplicativo) implementando as interfaces ODBC padrão para a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

O Microsoft ODBC Driver for SQL Server pode ser usado para criar novos aplicativos. Você também pode atualizar seus aplicativos mais antigos que usam um driver ODBC mais antigo no momento. O ODBC Driver for SQL Server dá suporte a conexões para o Banco de Dados SQL do Azure, o SQL Data Warehouse do Azure, SQL Server 2017, SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008 e SQL Server 2005.  

## <a name="summary"></a>Resumo

| Versão       | Recursos com suporte      |
| ------------- |---------------| 
| Microsoft ODBC Driver 17 for SQL Server | <ul><li>Suporte a Always Encrypted para a API BCP</li><li>O novo atributo de cadeia de conexão UseFMTONLY faz com que o driver use metadados herdados em casos especiais que exigem tabelas temporárias</li>
| Microsoft ODBC Driver 13.1 for SQL Server     | <ul><li>Always Encrypted</li><li>Autenticação do Azure AD</li><li>AG (Grupos de Disponibilidade) AlwaysOn</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>Nome de domínio internacionalizado (IDN)</li></ul> |
| Microsoft ODBC Driver 11 para SQL Server | <ul><li>Pool de conexões com reconhecimento de driver</li><li>Resiliência da conexão</li><li>Execução assíncrona (Método de Sondagem)</li></ul> |    

## <a name="documentation"></a>Documentação  
Esta documentação para o Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] inclui:  
  
-   [Notas sobre a Versão para ODBC para SQL Server no Windows](../../../connect/odbc/windows/release-notes-odbc-sql-server-windows.md)  
-   [Recursos do Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [Requisitos do sistema, instalação e arquivos de driver](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [Pooling de conexão com reconhecimento de driver no driver ODBC para SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [Exemplo de execução assíncrona &#40;método de notificação&#41](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Resiliência de conexão no driver ODBC do Windows](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [Uso do Always Encrypted com o Driver ODBC](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [Usando o Azure Active Directory com o Driver ODBC](../../../connect/odbc/using-azure-active-directory.md) 
-   [Como usar a resolução IP de rede transparente](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>Comunidade  
- [Blog da equipe do Microsoft ODBC Driver For SQL Server](https://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server Data Access Forum](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>Consulte Também  
- [Sobre o SQL Server Native Client](https://msdn.microsoft.com/sqlserver/ff658532.aspx)   
- [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [Perguntas frequentes do SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937707.aspx)   
- [Referência do programador ODBC](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
