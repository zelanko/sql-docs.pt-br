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
author: v-makouz
ms.author: genemi
ms.openlocfilehash: 6e3f7929c17b161d3534474d3d9ad99e559714d2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69653802"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Recursos do Microsoft ODBC Driver for SQL Server no Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-174-for-sql-server-on-windows"></a>Microsoft ODBC Driver 17.4 for SQL Server no Windows

O ODBC Driver 17.4 inclui a capacidade de ajustar as configurações keep alive do TCP. Elas podem ser modificadas adicionando valores às chaves do Registro do driver ou da DSN. As chaves estão localizadas em `HKEY_LOCAL_MACHINE\Software\ODBC\` para fontes de dados do sistema e em `HKEY_CURRENT_USER\Software\ODBC\` para fontes de dados do usuário. Para o DSN, os valores precisam ser adicionados a `...\Software\ODBC\ODBC.INI\<DSN Name>`; para o driver, a `...\Software\ODBC\ODBCINST.INI\ODBC Driver 17 for SQL Server`.

Confira [Entradas do Registro para componentes ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md) para obter mais informações.

Os valores são `REG_SZ` e são os seguintes:

- `KeepAlive` controla a frequência com que o TCP tenta verificar se uma conexão ociosa ainda está intacta enviando um pacote keep alive. O padrão é 30 segundos.

- `KeepAliveInterval` determina o intervalo que separa cada retransmissão keep alive até que uma resposta seja recebida. O padrão é 1 segundo.



## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for SQL Server no Windows

O ODBC Driver 13.1 for SQL Server contém toda a funcionalidade da versão anterior (11) e adiciona suporte para Always Encrypted e a autenticação do Azure Active Directory quando usado em conjunto com o Microsoft SQL Server 2016.  
  
Always Encrypted permite que os clientes criptografem os dados confidenciais em aplicativos de cliente e nunca revelem as chaves de criptografia para o SQL Server. Um driver Always Encrypted habilitado instalado no computador cliente realiza isso automaticamente criptografando e descriptografando dados confidenciais no aplicativo cliente do SQL Server. O driver criptografa as colunas de dados confidenciais antes de passar os dados para o SQL Server e reconfigura automaticamente as consultas para que a semântica do aplicativo seja preservada. Da mesma forma, o driver de modo transparente descriptografa os dados armazenados em colunas de banco de dados criptografado que estão contidas nos resultados da consulta. Para obter mais informações, veja [Como usar Always Encrypted com o driver ODBC do Windows](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md).
 
O Azure Active Directory permite que usuários, DBAs e programadores de aplicativos usem a autenticação do Azure Active Directory como um mecanismo de conexão com o Banco de Dados SQL do Microsoft Azure e o Microsoft SQL Server 2016 usando identidades no Azure AD (Azure Active Directory). Para obter mais informações, confira [Como usar o Azure Active Directory com o ODBC Driver](../../../connect/odbc/using-azure-active-directory.md) e [Conexão ao Banco de Dados SQL ou ao SQL Data Warehouse usando a autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft ODBC Driver 11 para SQL Server no Windows  

O ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contém toda a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client fornecida no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Para obter mais informações, consulte [Programação do SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md). O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client se baseia o driver ODBC fornecido com o sistema operacional Windows. Para obter mais informações, consulte [Windows Data Access Components SDK](https://msdn.microsoft.com/library/aa968814(VS.85).aspx)(SDL do Windows Data Access Components).  
  
Esta versão do ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contém os seguintes recursos novos:  
  
### <a name="bcpexe--l-option-for-specifying-a-login-timeout"></a>Opção bcp.exe -l para especificar um tempo limite de logon
 
A opção -l especifica o número de segundos antes que um logon `bcp.exe` em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] expire quando você tentar se conectar a um servidor. O tempo limite de logon padrão é de 15 segundos. O tempo limite do logon deve ser um número entre 0 e 65534. O `bcp.exe` irá gerar uma mensagem de erro se o valor fornecido não for numérico ou não estiver nesse intervalo. Um valor de 0 especifica um tempo limite infinito. Um tempo limite de logon de menos de (aproximadamente) 10 segundos não é confiável.  
  
### <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver  
O Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte para [Pool de Conexões com Reconhecimento de Driver](https://msdn.microsoft.com/library/hh405031(VS.85).aspx). Para obter mais informações, consulte [Driver-Aware Connection Pooling in the ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).  
  
### <a name="asynchronous-execution-notification-method"></a>Execução assíncrona (método de notificação)  
O ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte para a [execução assíncrona (método de notificação)](https://msdn.microsoft.com/library/hh405038(VS.85).aspx). Para encontrar um exemplo de uso, veja [Amostra de execução assíncrona &#40;método de notificação&#41;](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md).  
  
### <a name="connection-resiliency"></a>Resiliência da conexão
Para garantir que os aplicativos permaneçam conectados a um Banco de Dados SQL do Microsoft Azure, o driver ODBC no Windows pode restaurar conexões ociosas. Para obter mais informações, consulte [Connection Resiliency in the Windows ODBC Driver](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).  
  
## <a name="behavior-changes"></a>Alterações de comportamento

No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, a opção `-y0` para `sqlcmd.exe` fazia com que a saída fosse truncada em 1 MB se a largura da tela fosse 0.
  
Começando com o ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], não há nenhum limite à quantidade de dados recuperados em uma única coluna quando `-y0` é especificado. O `sqlcmd.exe` agora transmite as colunas como fluxos de até 2 GB ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] máximo para o tipo de dados).  
  
Outra diferença é que agora, especificar `-h` e `-y0` simultaneamente produz um erro que informa que as opções são incompatíveis. `-h`, que especifica o número de linhas a imprimir entre cabeçalhos de coluna e nunca foi compatível com `-y0`, foi ignorado, embora nenhum cabeçalho tenha sido impresso.
  
Observe que `-y0` pode causar problemas de desempenho tanto no servidor quanto na rede, dependendo do tamanho dos dados retornados.

## <a name="see-also"></a>Consulte Também  
[Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
