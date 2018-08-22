---
title: Alterando senhas programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], password expiration
- SQL Server Native Client ODBC driver, passwords
- SQL Server Native Client OLE DB provider, passwords
- passwords [SQL Server], expiration
- SQLNCLI, password expiration
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- expired passwords [SQL Server Native Client]
- SQL Server Native Client, password expiration
- modifying passwords
ms.assetid: 624ad949-5fed-4ce5-b319-878549f9487b
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4de5badcb2b8c67d23b00fcb645c44fa8e1b1681
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393981"
---
# <a name="changing-passwords-programmatically"></a>Alterando senhas programaticamente
  Antes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], quando a senha de um usuário expirava, somente um administrador poderia redefini-la. Começando com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporta Native Client manipulando a expiração de senha programaticamente, por meio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client e por meio de alterações a **Logon do SQL Server** caixas de diálogo.  
  
> [!NOTE]  
>  Quando possível, solicite aos usuários que insiram suas credenciais em tempo de execução e que evitem armazená-las em um formato persistente. Caso precise persistir as credenciais, criptografe-as usando a [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532). Para obter mais informações sobre o uso de senhas, confira [Senhas fortes](../../security/strong-passwords.md).  
  
## <a name="sql-server-login-error-codes"></a>Códigos de erro de logon do SQL Server  
 Quando não é possível estabelecer uma conexão devido a problemas de autenticação, um dos seguintes códigos de erro do SQL Server estará disponível para o aplicativo, de forma a auxiliar no diagnóstico e na recuperação.  
  
|Código de erro do SQL Server|Mensagem de erro|  
|---------------------------|-------------------|  
|15113|Falha no logon do usuário '%.*ls'. Motivo: falha na validação da senha. A conta está bloqueada.|  
|18463|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. A senha não pode ser usada neste momento.|  
|18464|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. A senha não atende aos requisitos de política, pois é muito curta.|  
|18465|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. A senha não atende aos requisitos de política, pois é muito longa.|  
|18466|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. A senha não atende aos requisitos de política, pois não é complexa o bastante.|  
|18467|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. A senha não atende aos requisitos da DLL de filtragem de senha.|  
|18468|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. Ocorreu um erro inesperado durante a validação da senha.|  
|18487|Falha no logon do usuário '%.*ls'. Motivo: a senha da conta expirou.|  
|18488|Falha no logon do usuário '%.*ls'. Motivo: a senha da conta deve ser alterada.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client dá suporte à expiração de senha mesmo uma interface do usuário e programaticamente.  
  
### <a name="ole-db-user-interface-password-expiration"></a>Expiração de senha da interface do usuário OLE DB  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client dá suporte à expiração de senha por meio de alterações feitas para o **logon do SQL Server** caixas de diálogo. Se o valor de DBPROP_INIT_PROMPT for definido como DBPROMPT_NOPROMPT, a tentativa de conexão inicial irá falhar, caso a senha tenha expirado.  
  
 Se DBPROP_INIT_PROMPT tiver sido definido com outro valor, o usuário verá a caixa de diálogo **Logon do SQL Server**, independentemente de a senha ter expirado ou não. O usuário pode clicar no botão **Opções** e marcar **Alterar Senha** para alterar a senha.  
  
 Se o usuário clicar em OK e a senha tiver expirado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solicitará que o usuário insira e confirme uma nova senha usando a caixa de diálogo **Alterar Senha do SQL Server**.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>Contas bloqueadas e comportamento do prompt do OLE DB  
 As tentativas de conexão podem falhar devido ao bloqueio da conta. Se isso ocorrer após a exibição da caixa de diálogo **Logon do SQL Server**, a mensagem de erro do servidor será exibida para o usuário e a tentativa de conexão será anulada. Isso também poderá ocorrer após a exibição da caixa de diálogo **Alterar Senha do SQL Server** se o usuário inserir um valor incorreto para a senha antiga. Neste caso, a mesma mensagem de erro será exibida e a tentativa de conexão será anulada.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>Contas bloqueadas, expiração de senha e pool de conexão do OLE DB  
 Uma conta pode ser bloqueada ou sua senha pode expirar enquanto a conexão ainda está ativa em um pool de conexão. O servidor verifica senhas expiradas e contas bloqueadas em duas ocasiões. A primeiro ao criar uma conexão pela primeira vez. A segunda ocasião é ao redefinir a conexão, quando ela é tirada do pool.  
  
 Quando a tentativa de redefinição falha, a conexão é removida do pool e um erro é retornado.  
  
### <a name="ole-db-programmatic-password-expiration"></a>Expiração de senha programática do OLE DB  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client dá suporte à expiração de senha por meio da adição da propriedade SSPROP_AUTH_OLD_PASSWORD (tipo VT_BSTR) que foi adicionada ao conjunto de propriedades DBPROPSET_SQLSERVERDBINIT.  
  
 A propriedade "Password" existente referencia DBPROP_AUTH_PASSWORD e é usada para armazenar a nova senha.  
  
> [!NOTE]  
>  Na cadeia de conexão, a propriedade "Old Password" define SSPROP_AUTH_OLD_PASSWORD, que é a senha atual (provavelmente expirada) que não está disponível por meio de uma propriedade de cadeia de caracteres do provedor.  
  
 O provedor não mantém o valor desta propriedade. Quando esta propriedade é definida, o provedor não usa o pool de conexão na primeira conexão, pois ocorrerá uma nova conexão. Se a alteração da senha tiver êxito, não será possível reutilizar a conexão atual, pois ela ainda conterá a senha antiga, que será inválida após a alteração da senha. Além disso, se o logon for bem-sucedido, o provedor limpará essa propriedade. As tentativas subsequentes de recuperar a senha antiga retornarão VT_EMPTY.  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD nunca deve ser mantido, pois ele é usado somente quando uma senha expirou.  
  
 Sempre que a propriedade "Old Password" é definida, o provedor supõe que está sendo feita uma tentativa de alterar a senha, a menos que a Autenticação do Windows também seja especificada; nesse caso, ela sempre terá precedência.  
  
 Se a Autenticação do Windows for usada, a especificação da senha antiga resultará em DB_E_ERRORSOCCURRED ou DB_S_ERRORSOCCURRED, dependendo de a senha antiga ter sido especificada como REQUIRED ou OPTIONAL, respectivamente, e o valor de status de DBPROPSTATUS_CONFLICTINGBADVALUE será retornado em *dwStatus*. Isto é detectado quando **IDBInitialize::Initialize** é chamado.  
  
 Se uma tentativa de alterar a senha falhar inesperadamente, o servidor retornará o código de erro 18468. Um erro OLEDB padrão é retornado da tentativa de conexão.  
  
 Para obter mais informações sobre o conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, consulte [propriedades de inicialização e autorização](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client dá suporte à expiração de senha mesmo uma interface do usuário e programaticamente.  
  
### <a name="odbc-user-interface-password-expiration"></a>Expiração de senha da interface do usuário ODBC  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client dá suporte à expiração de senha por meio de alterações feitas para o **logon do SQL Server** caixas de diálogo.  
  
 Se [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md) é chamado e o valor de **DriverCompletion** é definido como SQL_DRIVER_NOPROMPT, a falha de tentativa de conexão inicial, se a senha expirou. O valor SQLSTATE 28000 e o valor do código de erro nativo 18487 são retornados por chamadas subsequentes a **SQLError** ou **SQLGetDiagRec**.  
  
 Se **DriverCompletion** foi definida para qualquer outro valor, o usuário vê o **logon do SQL Server** caixa de diálogo, independentemente da senha expirou ou não. O usuário pode clicar no botão **Opções** e marcar **Alterar Senha** para alterar a senha.  
  
 Se o usuário clica em Okey e a senha expirou [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] prompts para digitar e confirmar uma nova senha usando o **alterar a senha do SQL Server** caixa de diálogo.  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>Contas bloqueadas e comportamento do prompt do ODBC  
 As tentativas de conexão podem falhar devido ao bloqueio da conta. Se isso ocorrer após a exibição da caixa de diálogo **Logon do SQL Server**, a mensagem de erro do servidor será exibida para o usuário e a tentativa de conexão será anulada. Isso também poderá ocorrer após a exibição da caixa de diálogo **Alterar Senha do SQL Server** se o usuário inserir um valor incorreto para a senha antiga. Neste caso, a mesma mensagem de erro será exibida e a tentativa de conexão será anulada.  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>Contas bloqueadas, expiração de senha e pool de conexão do ODBC  
 Uma conta pode ser bloqueada ou sua senha pode expirar enquanto a conexão ainda está ativa em um pool de conexão. O servidor verifica senhas expiradas e contas bloqueadas em duas ocasiões. A primeiro ao criar uma conexão pela primeira vez. A segunda ocasião é ao redefinir a conexão, quando ela é tirada do pool.  
  
 Quando a tentativa de redefinição falha, a conexão é removida do pool e um erro é retornado.  
  
### <a name="odbc-programmatic-password-expiration"></a>Expiração de senha programática do ODBC  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client dá suporte à expiração de senha por meio da adição do atributo SQL_COPT_SS_OLDPWD, que é definido antes de se conectar ao servidor usando o [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) função.  
  
 O atributo SQL_COPT_SS_OLDPWD do identificador de conexão referencia a senha expirada. Não há nenhum atributo de cadeia de conexão para esse atributo, pois isto interferiria com o pool de conexão. Se o logon tiver êxito, o driver limpará esse atributo.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client retornará SQL_ERROR em quatro casos para esse recurso: expiração de senha, conflito de política de senha, bloqueio de conta, e quando a propriedade de senha antiga é definida ao usar a autenticação do Windows. O driver retorna as mensagens de erro apropriado para o usuário quando [SQLGetDiagField](../../native-client-odbc-api/sqlgetdiagfield.md) é invocado.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)  
  
  
