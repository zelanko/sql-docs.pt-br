---
title: Protegendo aplicativos RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d41a1150a2562779f233454ae32949310cde600e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191771"
---
# <a name="securing-rds-applications"></a>Proteger aplicativos RDS
Este tópico fornece informações de segurança para RDS.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Problemas de segurança do Microsoft Internet Explorer  
 Com novos aprimoramentos de segurança adicionados ao Microsoft Internet Explorer, alguns objetos do ADO e RDS são restritos à execução somente em um ambiente de modo de "segurança". Isso exige que você esteja ciente desses problemas, incluindo zonas diferentes, níveis de segurança, comportamento restritivo, operações não seguras e as configurações de segurança personalizadas.  
  
## <a name="security-and-your-web-server"></a>Segurança e seu servidor Web  
 Se você usar o [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) de objeto em seu servidor Web da Internet, lembre-se de que fazer isso cria um potencial risco de segurança. Os usuários externos que obtêm nome de fonte de dados válido (DSN), ID de usuário e informações de senha foi possível gravar páginas para enviar qualquer consulta à fonte de dados. Se você quiser acesso mais restrito a uma fonte de dados, uma opção é cancelar o registro e exclua os **RDSServer.DataFactory** (msadcf.dll) do objeto e, em vez disso, use objetos comerciais personalizados com consultas embutido em código.  
  
 Para obter mais informações sobre as implicações de usar o objeto RDSServer.DataFactory segurança, consulte o boletim de segurança da Microsoft MS99-025 no site da Web de segurança da Microsoft.  
  
## <a name="client-impersonation-and-security"></a>Segurança e a representação do cliente  
 Se o **autenticação de senha** propriedade para o servidor Web do IIS é definida como autenticação de desafio/resposta do Windows NT (para Windows NT 4.0) ou a autenticação do Windows integrada (para Windows 2000) e, em seguida, são objetos comerciais invocado no contexto de segurança do cliente. Isso é um novo recurso no RDS 1.5 que permite a representação do cliente por meio de HTTP. Ao trabalhar nesse modo, o logon para o servidor Web (IIS) não é anônimo, mas usa a ID de usuário e senha que o computador cliente está executando em. Se os DSNs do ODBC são configurados para usar Conexão confiável, também acontece acesso aos bancos de dados, como o SQL Server, sob o contexto de segurança do cliente. Mas isso só funcionará se o banco de dados está no mesmo computador que o IIS; as credenciais do cliente não poderão ser transmitidas para outro computador.  
  
 Por exemplo, um cliente, John Doe, com a ID de usuário = "JohnD" e a senha = "segredo" está conectado a um computador cliente. Ele executa um aplicativo baseado em navegador que precisa acessar o **RDSServer.DataFactory** objeto para criar um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) executando uma consulta SQL no computador "Meuservidor" executando o IIS. MyServer, um sistema que executa o Windows NT Server 4.0, é configurado para usar a autenticação de desafio/resposta do Windows NT, o DSN do ODBC tem "Usar confiável Conexão" selecionado e o servidor também contém a fonte de dados do SQL Server. Quando uma solicitação é recebida no servidor Web, ele solicita que o cliente para a ID de usuário e senha. Assim, a solicitação é registrada em MeuServidor como proveniente de "JohnD" / "Segredo", em vez de IUSER_MyServer (que é o padrão quando a autenticação de senha anônima está ativado). Da mesma forma, ao fazer logon no SQL Server, "JohnD" / "Segredo" é usado.  
  
 Consequentemente, o modo de autenticação do Windows NT de IIS desafio/resposta permite que as páginas HTML a ser criado sem que o usuário que está sendo solicitado explicitamente as informações de ID e a senha de usuário necessárias para fazer logon no banco de dados. Se a autenticação básica do IIS que estavam sendo usada, em seguida, isso também seria necessário.  
  
## <a name="password-authentication"></a>Autenticação de senha  
 RDS podem se comunicar com um servidor Web IIS em execução em qualquer um dos três modos de autenticação de senha: Autenticação de desafio/resposta do NT, básico ou anônimo (chamada de autenticação do Windows integrada no Windows 2000). Essas configurações definem como um servidor Web controla o acesso por meio dele, como exigir que um computador cliente tem privilégios de acesso explícitas no servidor Web do NT.


