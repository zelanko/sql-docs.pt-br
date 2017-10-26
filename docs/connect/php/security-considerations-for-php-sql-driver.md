---
title: "Considerações de segurança para o Driver SQL de PHP | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security considerations
ms.assetid: a8c1a570-9204-454f-b94c-ba34f54d487c
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2a7423bcfcfd28073840ad7f8c9ee2e7424507bc
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="security-considerations-for-php-sql-driver"></a>Considerações de segurança para o driver SQL do PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico descreve as considerações de segurança específicas para desenvolver, implantar e executar aplicativos que usam os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Para obter mais informações sobre segurança do SQL Server, consulte [Data security and compliance](http://go.microsoft.com/fwlink/?LinkId=129225).  
  
## <a name="connect-using-windows-authentication"></a>Conectar usando a Autenticação do Windows  
A Autenticação do Windows deve ser usada para se conectar ao SQL Server sempre que possível, pelos seguintes motivos:  
  
-   **Nenhuma credencial é passada pela rede durante a autenticação.** Nomes de usuário e senhas não são inseridas na cadeia de conexão do banco de dados. Isso significa que usuários mal-intencionados ou invasores não podem obter as credenciais monitorando a rede ou exibindo cadeias de conexão nos arquivos de configuração.  
  
-   **Os usuários estão sujeitos ao gerenciamento centralizado de contas.** Políticas de segurança, como períodos de validade da senha, comprimento mínimo da senha e bloqueio de conta após várias solicitações de logon inválidas são impostas.  
  
Para obter informações sobre como se conectar a um servidor com a Autenticação do Windows, consulte [How to: Connect using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Quando você se conecta usando a Autenticação do Windows, é recomendável configurar seu ambiente para que o SQL Server possa usar o protocolo de autenticação Kerberos. Para obter mais informações, consulte [Como certificar-se de que você está usando a Autenticação Kerberos ao criar uma conexão remota com uma instância do SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=121862) ou [Autenticação Kerberos e SQL Server](http://go.microsoft.com/fwlink/?LinkId=129226).  
  
## <a name="use-encrypted-connections-when-transferring-sensitive-data"></a>Usar conexões criptografadas ao transferir dados confidenciais  
Devem-se usar conexões criptografadas sempre que dados confidenciais forem enviados para ou recuperados do SQL Server. Para obter informações sobre como habilitar conexões criptografadas, consulte [como habilitar conexões criptografadas ao mecanismo de banco de dados (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/?LinkId=121864). Para estabelecer uma conexão segura com os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], use o atributo de conexão Encrypt ao se conectar ao servidor. Para obter mais informações sobre atributos de conexão, consulte [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="use-parameterized-queries"></a>Usar consultas parametrizadas  
Use consultas parametrizadas para reduzir o risco de ataques de injeção de SQL. Para obter exemplos de como executar consultas parametrizadas, consulte [How to: Perform Parameterized Queries](../../connect/php/how-to-perform-parameterized-queries.md).  
  
Para obter mais informações sobre ataques de injeção de SQL e as considerações de segurança relacionadas, consulte [Injeção SQL](http://go.microsoft.com/fwlink/?LinkId=104224).  
  
## <a name="do-not-accept-server-or-connection-string-information-from-end-users"></a>Não aceitar informações de cadeia de conexão de usuários finais ou de servidor  
Escreva os aplicativos de forma que os usuários finais não possam enviar informações da cadeia de conexão ou do servidor para o aplicativo. Manter controle restrito sobre informações de cadeia de caracteres de conexão e de servidor reduz a área de superfície para atividades mal-intencionadas.  
  
## <a name="turn-warningsaserrors-on-during-application-development"></a>Ativar WarningsAsErrors durante o desenvolvimento de aplicativos  
Desenvolva aplicativos com a configuração **WarningsAsErrors** definida como **true** para que os avisos emitidos pelo driver sejam tratados como erros. Isso permitirá que você trate os avisos antes de implantar seu aplicativo. Para obter mais informações, consulte [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).  
  
## <a name="secure-logs-for-deployed-application"></a>Proteger os logs do aplicativo implantado  
Para aplicativos implantados, verifique se os logs estão gravados em um local seguro ou se que o log está desativado. Isso ajuda a proteger contra a possibilidade de os usuários finais acessarem informações gravadas nos arquivos de log. Para obter mais informações, consulte [Logging Activity](../../connect/php/logging-activity.md).  
  
## <a name="see-also"></a>Consulte também  
[Guia de programação para o driver SQL de PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
  

