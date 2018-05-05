---
title: Protegendo aplicativos RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60cb8cde92d116344a99aea1e55d391906096548
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="securing-rds-applications"></a>Protegendo aplicativos do RDS
Este tópico fornece informações de segurança para RDS.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Problemas de segurança do Microsoft Internet Explorer  
 Com novos aprimoramentos de segurança foram adicionados para o Microsoft Internet Explorer, alguns objetos ADO e RDS são restritos a execução apenas em um ambiente de modo de "segurança". Isso requer que você esteja ciente desses problemas, inclusive regiões diferentes, níveis de segurança, comportamento restritivo, operações unsafe e as configurações de segurança personalizadas.  
  
## <a name="security-and-your-web-server"></a>Segurança e o servidor Web  
 Se você usar o [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) de objeto em seu servidor Web de Internet, lembre-se de que fazer isso cria um risco à segurança. Os usuários externos que obter nome de fonte de dados válida (DSN), ID de usuário e informações de senha foi possível gravar páginas para enviar todas as consultas à fonte de dados. Se você quiser acesso mais restrito a uma fonte de dados, uma opção é cancelar o registro e exclua o **RDSServer.DataFactory** (msadcf.dll) do objeto e, em vez disso, use objetos comerciais personalizados com consultas embutido.  
  
 Para obter mais informações sobre as implicações de usar o objeto RDSServer.DataFactory segurança, consulte o boletim de segurança da Microsoft MS99-025 no site da Web de segurança da Microsoft.  
  
## <a name="client-impersonation-and-security"></a>Segurança e a representação do cliente  
 Se o **autenticação de senha** propriedade para o servidor Web do IIS é definida para a autenticação de desafio/resposta do Windows NT (para Windows NT 4.0) ou a autenticação integrada do Windows (para Windows 2000), são objetos de negócios invocado no contexto de segurança do cliente. Este é um novo recurso do RDS 1.5 que permite a representação do cliente por HTTP. Ao trabalhar nesse modo, o logon no servidor Web (IIS) não é anônimo, mas usa o ID de usuário e senha que o computador cliente estiver executando em. Se os DSNs de ODBC são configurados para usar Conexão confiável, também acontece acesso aos bancos de dados, como o SQL Server, no contexto de segurança do cliente. Mas isso só funcionará se o banco de dados no mesmo computador que o IIS; as credenciais do cliente não podem ser transferidas para outro computador.  
  
 Por exemplo, um cliente, John Doe com userid = "JohnD" e a senha = "segredo" está conectado a um computador cliente. Ele executa um aplicativo baseado em navegador que precisa acessar o **RDSServer.DataFactory** objeto para criar um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) executando uma consulta SQL no computador "MyServer" executando o IIS. MyServer, um sistema que executa o Windows NT Server 4.0, é configurado para usar a autenticação de desafio/resposta do Windows NT, o DSN ODBC tem "Usar confiável Conexão" selecionado e o servidor também contém a fonte de dados do SQL Server. Quando uma solicitação é recebida no servidor Web, ele solicita que o cliente para a ID de usuário e senha. Portanto, a solicitação é registrada em MeuServidor como provenientes de "JohnD" / "Segredo" em vez de IUSER_MyServer (que é o padrão quando a autenticação de senha anônima está ativado). Da mesma forma, ao fazer logon no SQL Server, "JohnD" / "Segredo" é usado.  
  
 Consequentemente, o modo de autenticação de desafio/resposta do Windows NT do IIS permite que as páginas HTML a ser criado sem que o usuário que está sendo solicitado explicitamente para as informações de ID e a senha de usuário necessárias para fazer logon no banco de dados. Se a autenticação básica do IIS que estavam sendo usada, em seguida, isso também seria necessário.  
  
## <a name="password-authentication"></a>Autenticação de senha  
 RDS pode se comunicar com um servidor Web IIS em execução em qualquer um dos três modos de autenticação de senha: anônima, básica, ou autenticação de desafio/resposta do NT (chamado de autenticação integrada do Windows no Windows 2000). Essas configurações definem como um servidor Web controla o acesso por meio dele, como exigir que um computador cliente tem privilégios de acesso explícito no servidor Web do NT.


