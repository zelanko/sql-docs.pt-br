---
title: Considerações de segurança para os drivers da Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- security considerations
ms.assetid: a8c1a570-9204-454f-b94c-ba34f54d487c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1fecf1add70a7b3bd96484cbd3634db2cfda01cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992893"
---
# <a name="security-considerations-for-the-microsoft-drivers-for-php-for-sql-server"></a>Considerações de segurança para os drivers da Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico descreve as considerações de segurança específicas para desenvolver, implantar e executar aplicativos que usam os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Para obter informações mais detalhadas sobre SQL Server segurança, consulte [visão geral da segurança do SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/overview-of-sql-server-security).  
  
## <a name="connect-using-windows-authentication"></a>Conectar usando a Autenticação do Windows  
A Autenticação do Windows deve ser usada para se conectar ao SQL Server sempre que possível, pelos seguintes motivos:  
  
-   **Nenhuma credencial é passada pela rede durante a autenticação.** Nomes de usuário e senhas não são inseridas na cadeia de conexão do banco de dados. Portanto, usuários mal-intencionados ou invasores não podem obter as credenciais monitorando a rede ou exibindo cadeias de conexão nos arquivos de configuração.  
  
-   **Os usuários estão sujeitos ao gerenciamento centralizado de contas.** Políticas de segurança, como períodos de validade da senha, comprimento mínimo da senha e bloqueio de conta após várias solicitações de logon inválidas são impostas.  
  
Para obter informações sobre como se conectar a um servidor com a Autenticação do Windows, consulte [How to: Connect using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Quando você se conecta usando a Autenticação do Windows, é recomendável configurar seu ambiente para que o SQL Server possa usar o protocolo de autenticação Kerberos. Para obter mais informações, consulte [Como certificar-se de que você está usando a Autenticação Kerberos ao criar uma conexão remota com uma instância do SQL Server 2005](https://support.microsoft.com/en-ca/help/909801/how-to-make-sure-that-you-are-using-kerberos-authentication-when-you-c) ou [Autenticação Kerberos e SQL Server](https://msdn.microsoft.com/library/cc280744.aspx).  
  
## <a name="use-encrypted-connections-when-transferring-sensitive-data"></a>Usar conexões criptografadas ao transferir dados confidenciais  
Devem-se usar conexões criptografadas sempre que dados confidenciais forem enviados para ou recuperados do SQL Server. Para obter informações sobre como habilitar conexões criptografadas, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados (SQL Server Configuration Manager)](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md). Para estabelecer uma conexão segura com os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], use o atributo de conexão Encrypt ao se conectar ao servidor. Para obter mais informações sobre atributos de conexão, consulte [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="use-parameterized-queries"></a>Usar consultas parametrizadas  
Use consultas parametrizadas para reduzir o risco de ataques de injeção de SQL. Para obter exemplos de como executar consultas parametrizadas, consulte [How to: Perform Parameterized Queries](../../connect/php/how-to-perform-parameterized-queries.md).  
  
Para obter mais informações sobre ataques de injeção de SQL e as considerações de segurança relacionadas, consulte [Injeção SQL](https://msdn.microsoft.com/library/ms161953.aspx).  
  
## <a name="do-not-accept-server-or-connection-string-information-from-end-users"></a>Não aceitar informações de cadeia de conexão de usuários finais ou de servidor  
Escreva os aplicativos de forma que os usuários finais não possam enviar informações da cadeia de conexão ou do servidor para o aplicativo. Manter controle restrito sobre informações de cadeia de caracteres de conexão e de servidor reduz a área de superfície para atividades mal-intencionadas.  
  
## <a name="turn-warningsaserrors-on-during-application-development"></a>Ativar WarningsAsErrors durante o desenvolvimento de aplicativos  
Desenvolva aplicativos com a configuração **WarningsAsErrors** definida como **true** para que os avisos emitidos pelo driver sejam tratados como erros. Isso permitirá que você trate os avisos antes de implantar seu aplicativo. Para obter mais informações, consulte [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).  
  
## <a name="secure-logs-for-deployed-application"></a>Proteger os logs do aplicativo implantado  
Para aplicativos implantados, verifique se os logs estão gravados em um local seguro ou se que o log está desativado. Isso ajuda a proteger contra a possibilidade de os usuários finais acessarem informações gravadas nos arquivos de log. Para obter mais informações, consulte [Logging Activity](../../connect/php/logging-activity.md).  
  
## <a name="see-also"></a>Consulte Também  
[Guia de programação para o Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
