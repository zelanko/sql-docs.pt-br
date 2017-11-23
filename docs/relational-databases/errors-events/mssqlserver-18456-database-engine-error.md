---
title: MSSQLSERVER_18456 | Microsoft Docs
ms.custom: 
ms.date: 06/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 18456 (Database Engine error)
ms.assetid: c417631d-be1f-42e0-8844-9f92c77e11f7
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ae32f75a30f38c3f2c86370afbb49bbf6e6031b7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver18456"></a>MSSQLSERVER_18456
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do Evento|18456|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LOGON_FAILED|  
|Texto da mensagem|Falha no logon do usuário '%.*ls'.%.\*ls|  
  
## <a name="explanation"></a>Explicação  
Quando uma tentativa de conexão é rejeitada por causa de uma falha na autenticação que envolva uma senha ou um número de usuário incorreto, uma mensagem semelhante à seguinte é retornada ao cliente: "Falha no logon do usuário '<nome_do_usuário>'. (Microsoft SQL Server, Erro: 18456)".  
  
Informações adicionais voltadas ao cliente incluem o seguinte:  
  
“Falha no logon do usuário '<nome_do_usuário>'. (Provedor da Dados .Net SqlClient)"  
  
-----------------------------\-  
  
"Nome do servidor: <nome_do_computador>"  
  
“Número do erro: 18456”  
  
"Severidade: 14"  
  
“Estado: 1”  
  
“Número de linha: 65536”  
  
A mensagem seguinte também poderá ser retornada:  
  
"Msg 18456, nível 14, estado 1, servidor <nome_do_computador>, linha 1"  
  
Falha no logon do usuário '<nome_do_usuário>'."  
  
## <a name="additional-error-information"></a>Informações adicionais de erro  
Para aumentar a segurança, a mensagem de erro que é retornada ao cliente oculta deliberadamente a natureza do erro de autenticação. No entanto, no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um erro correspondente contém um estado de erro que mapeia até uma condição de falha na autenticação. Compare o estado de erro com a lista a seguir para determinar a razão da falha no logon.  
  
|Estado|Description|  
|---------|---------------|  
|1|Informações de erro não disponíveis. Esse estado geralmente significa que você não tem permissão para receber os detalhes do erro. Contate o administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter mais informações.|  
|2|A ID do usuário não é válida.|  
|5|A ID do usuário não é válida.|  
|6|Uma tentativa foi feita para usar um logon do Windows com Autenticação do SQL Server.|  
|7|O logon está desabilitado e a senha está incorreta.|  
|8|A senha está incorreta.|  
|9|A senha não é válida.|  
|11|O logon é válido, mas houve falha no acesso ao servidor. Uma causa possível deste erro é quando o usuário do Windows tem acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como membro do grupo de administradores locais, mas o Windows não está fornecendo credenciais de administrador. Para se conectar, inicie o programa de conexão usando a opção **Executar como administrador** e, depois, adicione o usuário do Windows ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um logon específico.|  
|12|O logon é válido, mas houve falha no acesso ao servidor.|  
|18|A senha deve ser alterada.|  
|38, 46|Não foi possível localizar o banco de dados solicitado pelo usuário.|
|102 – 111|Falha de AAD.|
|122 – 124|Falha devido a nome de usuário ou senha vazios.|
|126|O banco de dados solicitado pelo usuário não existe.|
|132 – 133|Falha de AAD.|
  
Outros estados de erro existem e significam um erro de processamento interno inesperado.  
  
**Outra possível causa incomum**  
  
A razão de erro **Falha em uma tentativa de logon com a Autenticação do SQL Server. O servidor está configurado apenas para a autenticação do Windows.** pode ser retornado nas situações a seguir.  
  
-   Quando o servidor é configurado para a autenticação de modo misto e uma conexão ODBC usa o protocolo TCP, e a conexão não especificar explicitamente que a conexão deve usar uma conexão confiável.  
  
-   Quando o servidor é configurado para a autenticação de modo misto, e uma conexão ODBC usa pipes nomeados, e as credenciais que o cliente usou para abrir o pipe nomeado são usadas para representar automaticamente o usuário, e a conexão não especificar explicitamente que ela deve usar uma conexão confiável.  
  
Para resolver esse problema, inclua **TRUSTED_CONNECTION = TRUE** na cadeia de conexão.  
  
## <a name="examples"></a>Exemplos  
Neste exemplo, o estado do erro de autenticação é 8. Isso indica que a senha está incorreta.  
  
|Data|Origem|Mensagem|  
|--------|----------|-----------|  
|2007-12-05 20:12:56.34|Logon|Erro: 18456, Severidade: 14, Estado: 8.|  
|2007-12-05 20:12:56.34|Logon|Falha no logon do usuário '<nome_do_usuário>'. [CLIENTE: <ip address>]|  
  
> [!NOTE]  
> Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado usando o modo de Autenticação do Windows e depois alterado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o modo de Autenticação do Windows, o logon **sa** é inicialmente desabilitado. Isso provoca o erro de estado 7: "Falha no logon do usuário 'sa'". Para habilitar o logon **sa**, consulte [Alterar modo de autenticação do servidor](~/database-engine/configure-windows/change-server-authentication-mode.md).  
  
## <a name="user-action"></a>Ação do usuário  
Se você estiver tentando se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado no Modo de Autenticação Mista.  
  
Se você estiver tentando se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existe e se você o escreveu corretamente.  
  
Se você estiver tentando se conectar usando a Autenticação do Windows, verifique se está devidamente conectado no domínio correto.  
  
Se o erro indicar estado 1, contate o administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Se você estiver tentando se conectar usando suas credenciais de administrador, inicie o aplicativo usando a opção **Executar como Administrador**. Quando conectado, adicione seu usuário do Windows como um logon individual.  
  
Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] oferecer suporte a bancos de dados independentes, confirme que o logon não foi excluído após a migração para um usuário de banco de dados independente.  
  
Durante a conexão local a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as conexões de serviços executados em **NT AUTHORITY\NETWORK SERVICE** deverão ser autenticadas com o uso do nome de domínio totalmente qualificado dos computadores. Para obter mais informações, consulte [Como usar a conta de serviço de rede para acessar recursos no ASP.NET](http://msdn.microsoft.com/library/ff647402.aspx)  
  
