---
title: Recursos do Microsoft ODBC Driver for SQL Server no Windows | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db5c3e2e8265e88d49025ffd65894623fc5c5f85
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202235"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Recursos do Microsoft ODBC Driver for SQL Server no Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for SQL Server no Windows

O Driver ODBC 13.1 para SQL Server contém toda a funcionalidade da versão anterior (11) e adiciona suporte para autenticação de Always Encrypted e o Azure Active Directory quando usado em conjunto com o Microsoft SQL Server 2016.  
  
Always Encrypted permite que os clientes criptografem os dados confidenciais em aplicativos de cliente e nunca revelem as chaves de criptografia para o SQL Server. Um driver Always Encrypted habilitado instalado no computador cliente realiza isso automaticamente criptografando e descriptografando dados confidenciais no aplicativo cliente do SQL Server. O driver criptografa as colunas de dados confidenciais antes de passar os dados para o SQL Server e reconfigura automaticamente as consultas para que a semântica do aplicativo seja preservada. Da mesma forma, o driver de modo transparente descriptografa os dados armazenados em colunas de banco de dados criptografado que estão contidas nos resultados da consulta. Para obter mais informações, veja [Como usar Always Encrypted com o driver ODBC do Windows](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md).
 
O Azure Active Directory permite que os usuários, DBAs e programadores de aplicativos usar a autenticação do Active Directory do Azure como um mecanismo para se conectar ao banco de dados SQL do Microsoft Azure e o Microsoft SQL Server 2016 usando identidades no Azure AD (Active Directory do Azure ). Para obter mais informações, consulte [usando o Azure Active Directory com o Driver ODBC](../../../connect/odbc/using-azure-active-directory.md), e [conectar-se ao banco de dados SQL ou SQL Data Warehouse por usando o Azure Active Directory autenticação](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft ODBC Driver 11 para SQL Server no Windows  

O ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contém toda a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client fornecida no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Para obter mais informações, consulte [Programação do SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md). O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client se baseia o driver ODBC fornecido com o sistema operacional Windows. Para obter mais informações, consulte [Windows Data Access Components SDK](https://msdn.microsoft.com/library/aa968814(VS.85).aspx)(SDL do Windows Data Access Components).  
  
Esta versão do ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contém os seguintes recursos novos:  
  
### <a name="bcpexe--l-option-for-specifying-a-login-timeout"></a>BCP.exe -l opção para especificar um tempo limite de logon
 
A opção -l especifica o número de segundos antes que um logon `bcp.exe` em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] expire quando você tentar se conectar a um servidor. O tempo de limite de logon padrão é 15 segundos. O tempo limite do logon deve ser um número entre 0 e 65534. O `bcp.exe` irá gerar uma mensagem de erro se o valor fornecido não for numérico ou não estiver nesse intervalo. Um valor de 0 especifica um tempo limite infinito. Um tempo limite de logon de menos de (aproximadamente) 10 segundos não é confiável.  
  
### <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver  
O Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte para [Pool de Conexões com Reconhecimento de Driver](https://msdn.microsoft.com/library/hh405031(VS.85).aspx). Para obter mais informações, consulte [Driver-Aware Connection Pooling in the ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).  
  
### <a name="asynchronous-execution-notification-method"></a>Execução assíncrona (método de notificação)  
O ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte para a [execução assíncrona (método de notificação)](https://msdn.microsoft.com/library/hh405038(VS.85).aspx). Para encontrar um exemplo de uso, veja [Amostra de execução assíncrona &#40;método de notificação&#41;](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md).  
  
### <a name="connection-resiliency"></a>Resiliência da conexão
Para garantir que os aplicativos permaneçam conectados a um Banco de Dados SQL do Microsoft Azure, o driver ODBC no Windows pode restaurar conexões ociosas. Para obter mais informações, consulte [Connection Resiliency in the Windows ODBC Driver](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).  
  
## <a name="behavior-changes"></a>Alterações de comportamento

Na [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, o `-y0` opção obter `sqlcmd.exe` causou a saída seja truncada em 1 MB se a largura da exibição era 0.
  
Começando com o ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], não há nenhum limite à quantidade de dados recuperados em uma única coluna quando `-y0` é especificado. O `sqlcmd.exe` agora transmite as colunas como fluxos de até 2 GB ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] máximo para o tipo de dados).  
  
Outra diferença é que especificar ambos `-h` e `-y0` agora produz um erro relatando que as opções são incompatíveis. `-h`, que especifica o número de linhas a imprimir entre cabeçalhos de coluna e nunca foi compatível com `-y0`, foi ignorado, embora nenhum cabeçalho tenha sido impresso.
  
Observe que `-y0` pode causar problemas de desempenho tanto no servidor quanto na rede, dependendo do tamanho dos dados retornados.

## <a name="see-also"></a>Consulte Também  
[Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
