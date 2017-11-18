---
title: Recursos do Microsoft ODBC Driver for SQL Server no Windows | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3916b53dcccf77cea96b5d12ce61273569b33dc3
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Recursos do Microsoft ODBC Driver for SQL Server no Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 para SQL Server no Windows

O ODBC Driver 13.1 para SQL Server contém toda a funcionalidade da versão anterior (11) e adiciona suporte para autenticação de sempre criptografado e o Active Directory do Azure quando usado em conjunto com o Microsoft SQL Server 2016.  
  
Always Encrypted permite que os clientes criptografem os dados confidenciais em aplicativos de cliente e nunca revelem as chaves de criptografia para o SQL Server. Um driver Always Encrypted habilitado instalado no computador cliente realiza isso automaticamente criptografando e descriptografando dados confidenciais no aplicativo cliente do SQL Server. O driver criptografa as colunas de dados confidenciais antes de passar os dados para o SQL Server e reconfigura automaticamente as consultas para que a semântica do aplicativo seja preservada. Da mesma forma, o driver de modo transparente descriptografa os dados armazenados em colunas de banco de dados criptografado que estão contidas nos resultados da consulta. Para obter mais informações, consulte [usando sempre criptografado com o Driver ODBC](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md).
 
Active Directory do Azure permite que os usuários do DBA e programadores de aplicativos usar a autenticação do Active Directory do Azure como um mecanismo para se conectar ao banco de dados SQL do Microsoft Azure e o Microsoft SQL Server 2016 usando as identidades no Azure Active Directory (AD do Azure ). Para obter mais informações, consulte [usando o Active Directory do Azure com o Driver ODBC](../../../connect/odbc/using-azure-active-directory.md), e [se conectar ao banco de dados SQL ou SQL Data Warehouse por usando o Azure Active Directory Authentication](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/).   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft ODBC Driver 11 para SQL Server no Windows  

O ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] contém toda a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] driver ODBC Native Client fornecida no [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]. Para obter mais informações, consulte [Programação do SQL Server Native Client](http://msdn.microsoft.com/library/ms130892.aspx). O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] driver ODBC Native Client se baseia o driver ODBC fornecido com o sistema operacional Windows. Para obter mais informações, consulte [Windows Data Access Components SDK](http://msdn.microsoft.com/library/aa968814(VS.85).aspx)(SDL do Windows Data Access Components).  
  
Esta versão do ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] contém os seguintes recursos novos:  
  
### <a name="bcpexe-l-option-for-specifying-a-login-timeout"></a>BCP.exe – l opção para especificar um tempo limite de logon
 
A opção – l Especifica o número de segundos antes que um `bcp.exe` login [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] o tempo limite ao tentar conectar a um servidor. O tempo de limite de logon padrão é 15 segundos. O tempo limite de logon deve ser um número entre 0 e 65534. O `bcp.exe` irá gerar uma mensagem de erro se o valor fornecido não for numérico ou não estiver nesse intervalo. Um valor de 0 especifica um tempo limite infinito. Um tempo limite de logon de menor que (aproximadamente) 10 segundos não é confiável.  
  
### <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver  
O Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] dá suporte a [Pooling de Conexão com reconhecimento de Driver](http://msdn.microsoft.com/library/hh405031(VS.85).aspx). Para obter mais informações, consulte [Driver-Aware Connection Pooling in the ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).  
  
### <a name="asynchronous-execution-notification-method"></a>Execução assíncrona (método de notificação)  
O Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] dá suporte a [execução assíncrona (método de notificação)](http://msdn.microsoft.com/library/hh405038(VS.85).aspx). Para obter um exemplo de uso, consulte [execução assíncrona &#40; Método de notificação &#41; Exemplo](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md).  
  
### <a name="connection-resiliency"></a>Resiliência da conexão
Para garantir que os aplicativos permaneçam conectados a um Banco de Dados SQL do Microsoft Azure, o driver ODBC no Windows pode restaurar conexões ociosas. Para obter mais informações, consulte [Connection Resiliency in the Windows ODBC Driver](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).  
  
## <a name="behavior-changes"></a>Alterações de comportamento

Em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client, o `-y0` opção `sqlcmd.exe` causou a saída seja truncada em 1 MB se a largura da exibição for 0.
  
A partir do ODBC Driver 11 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], não há nenhum limite na quantidade de dados que podem ser recuperados em uma única coluna quando `–y0` for especificado. `sqlcmd.exe`Agora fluxos colunas tão grandes quanto 2 GB ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] máximo do tipo de dados).  
  
Outra diferença é que especificar ambos `-h` e `-y0` agora produz um erro relatando que as opções são incompatíveis. `-h`, que especifica o número de linhas a imprimir entre cabeçalhos de coluna e nunca foi compatível com `-y0`, foi ignorado, embora nenhum cabeçalho tenha sido impresso.
  
Observe que `-y0` pode causar problemas de desempenho no servidor e rede, dependendo do tamanho dos dados retornados.

## <a name="see-also"></a>Consulte também  
[Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  

