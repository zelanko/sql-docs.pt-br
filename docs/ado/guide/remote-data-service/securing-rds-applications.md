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
ms.openlocfilehash: d91b8f41c344d45bfde646d24819e73c0cd8f283
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922221"
---
# <a name="securing-rds-applications"></a>Proteger aplicativos RDS
Este tópico fornece informações de segurança para o RDS.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Problemas de segurança do Microsoft Internet Explorer  
 Com novos aprimoramentos de segurança adicionados ao Microsoft Internet Explorer, alguns objetos ADO e RDS são restritos à execução apenas em um ambiente de modo "seguro". Isso exige que você esteja ciente desses problemas, incluindo diferentes zonas, níveis de segurança, comportamento restritivo, operações não seguras e configurações de segurança personalizadas.  
  
## <a name="security-and-your-web-server"></a>Segurança e seu servidor Web  
 Se você usar o objeto [RDSServer. datafactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) no seu servidor Web da Internet, lembre-se de que isso cria um risco de segurança potencial. Os usuários externos que obtêm o nome da fonte de dados (DSN), a ID de usuário e as informações de senha válidos podem gravar páginas para enviar qualquer consulta para essa fonte de dados. Se você quiser acesso mais restrito a uma fonte de dados, uma opção é cancelar o registro e excluir o objeto **RDSServer. datafactory** (msadcf. dll) e, em vez disso, usar objetos comerciais personalizados com consultas embutidas em código.  
  
 Para obter mais informações sobre as implicações de segurança do uso do objeto RDSServer. datafactory, consulte o boletim de segurança da Microsoft MS99-025 no site segurança da Microsoft.  
  
## <a name="client-impersonation-and-security"></a>Representação e segurança do cliente  
 Se a propriedade de **autenticação de senha** para o servidor Web do IIS estiver definida como autenticação de desafio/resposta do Windows NT (para windows NT 4,0) ou para autenticação integrada do Windows (para Windows 2000), os objetos comerciais serão invocados sob o contexto de segurança do cliente. Esse é um novo recurso no RDS 1,5 que permite a representação do cliente sobre HTTP. Ao trabalhar nesse modo, o logon no servidor Web (IIS) não é anônimo, mas usa a ID de usuário e a senha em que o computador cliente está sendo executado. Se os DSNs ODBC estiverem configurados para usar a conexão confiável, o acesso aos bancos de dados, como SQL Server, também ocorrerá no contexto de segurança do cliente. Mas isso só funcionará se o banco de dados estiver no mesmo computador que o IIS; as credenciais do cliente não podem ser transportadas para outro computador.  
  
 Por exemplo, um cliente, John Doe, com userid = "JohnD" e password = "segredo", está conectado a um computador cliente. Ele executa um aplicativo baseado em navegador que precisa acessar o objeto **RDSServer. datafactory** para criar um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) executando uma consulta SQL no computador "meuservidor" que executa o IIS. Meuservidor, um sistema executando o Windows NT Server 4,0, está configurado para usar a autenticação de desafio/resposta do Windows NT, seu DSN ODBC tem a seleção "usar conexão confiável" selecionada e o servidor também contém a fonte de dados SQL Server. Quando uma solicitação é recebida no servidor Web, ela solicita ao cliente a ID de usuário e a senha. Assim, a solicitação é registrada em meuservidor como proveniente de "João"/"segredo" em vez de IUSER_MyServer (que é o padrão quando a autenticação de senha anônima está ativada). Da mesma forma, ao fazer logon no SQL Server, "João"/"segredo" é usado.  
  
 Consequentemente, o modo de autenticação de desafio/resposta do IIS do Windows NT permite que páginas HTML sejam criadas sem que o usuário seja explicitamente solicitado a fornecer as informações de ID de usuário e senha necessárias para fazer logon no banco de dados. Se a autenticação básica do IIS estiver sendo usada, isso também seria necessário.  
  
## <a name="password-authentication"></a>Autenticação de senha  
 O RDS pode se comunicar com um servidor Web IIS em execução em qualquer um dos três modos de autenticação de senha: autenticação anônima, básica ou de desafio/resposta NT (chamada de autenticação integrada do Windows no Windows 2000). Essas configurações definem como um servidor Web controla o acesso por meio dele, como exigir que um computador cliente tenha privilégios de acesso explícitos no servidor Web NT.


