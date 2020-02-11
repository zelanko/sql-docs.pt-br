---
title: Alterando senhas programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: def93c4860a7e1a29a4a721de3aa451f91fd1869
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73761501"
---
# <a name="changing-passwords-programmatically"></a>Alterando senhas programaticamente
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Antes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], quando a senha de um usuário expirava, somente um administrador poderia redefini-la. A partir [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , o Native Client dá suporte ao tratamento de expiração de senha programaticamente por meio do provedor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB de cliente nativo e do driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e por meio de alterações nas caixas de diálogo de logon do **SQL Server** .  
  
> [!NOTE]  
>  Quando possível, solicite aos usuários que insiram suas credenciais em tempo de execução e que evitem armazená-las em um formato persistente. Caso precise persistir as credenciais, criptografe-as usando a [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532). Para obter mais informações sobre o uso de senhas, confira [Senhas fortes](../../../relational-databases/security/strong-passwords.md).  
  
## <a name="sql-server-login-error-codes"></a>Códigos de erro de logon do SQL Server  
 Quando não é possível estabelecer uma conexão devido a problemas de autenticação, um dos seguintes códigos de erro do SQL Server estará disponível para o aplicativo, de forma a auxiliar no diagnóstico e na recuperação.  
  
|Código de erro do SQL Server|Mensagem de erro|  
|---------------------------|-------------------|  
|15113|Falha no logon do usuário '%.*ls'. Motivo: falha na validação da senha. A conta está bloqueada.|  
|18463|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. A senha não pode ser usada neste momento.|  
|18464|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. A senha não atende aos requisitos da política porque é muito curta.|  
|18465|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. A senha não atende aos requisitos de política, pois é muito longa.|  
|18466|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. A senha não atende aos requisitos da política porque não é complexa o suficiente.|  
|18467|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. A senha não atende aos requisitos da DLL de filtragem de senha.|  
|18468|Falha no logon do usuário '%.*ls'. Motivo: falha na alteração da senha. Ocorreu um erro inesperado durante a validação da senha.|  
|18487|Falha no logon do usuário '%.*ls'. Motivo: a senha da conta expirou.|  
|18488|Falha no logon do usuário '%.*ls'. Motivo: a senha da conta deve ser alterada.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte à expiração de senha por meio de uma interface do usuário e programatica  
  
### <a name="ole-db-user-interface-password-expiration"></a>Expiração de senha da interface do usuário OLE DB  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte à expiração de senha por meio de alterações feitas nas caixas de diálogo de **logon do SQL Server** . Se o valor de DBPROP_INIT_PROMPT for definido como DBPROMPT_NOPROMPT, a tentativa de conexão inicial irá falhar, caso a senha tenha expirado.  
  
 Se DBPROP_INIT_PROMPT tiver sido definido com outro valor, o usuário verá a caixa de diálogo **Logon do SQL Server**, independentemente de a senha ter expirado ou não. O usuário pode clicar no botão **Opções** e marcar **Alterar Senha** para alterar a senha.  
  
 Se o usuário clicar em OK e a senha tiver expirado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solicitará que o usuário insira e confirme uma nova senha usando a caixa de diálogo **Alterar Senha do SQL Server**.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>Contas bloqueadas e comportamento do prompt do OLE DB  
 As tentativas de conexão podem falhar devido ao bloqueio da conta. Se isso ocorrer após a exibição da caixa de diálogo **Logon do SQL Server**, a mensagem de erro do servidor será exibida para o usuário e a tentativa de conexão será anulada. Isso também poderá ocorrer após a exibição da caixa de diálogo **Alterar Senha do SQL Server** se o usuário inserir um valor incorreto para a senha antiga. Neste caso, a mesma mensagem de erro será exibida e a tentativa de conexão será anulada.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>Contas bloqueadas, expiração de senha e pool de conexão do OLE DB  
 Uma conta pode ser bloqueada ou sua senha pode expirar enquanto a conexão ainda está ativa em um pool de conexão. O servidor verifica senhas expiradas e contas bloqueadas em duas ocasiões. A primeiro ao criar uma conexão pela primeira vez. A segunda ocasião é ao redefinir a conexão, quando ela é tirada do pool.  
  
 Quando a tentativa de redefinição falha, a conexão é removida do pool e um erro é retornado.  
  
### <a name="ole-db-programmatic-password-expiration"></a>Expiração de senha programática do OLE DB  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte à expiração de senha por meio da adição da propriedade SSPROP_AUTH_OLD_PASSWORD (tipo VT_BSTR) que foi adicionada ao conjunto de propriedades DBPROPSET_SQLSERVERDBINIT.  
  
 A propriedade "Password" existente referencia DBPROP_AUTH_PASSWORD e é usada para armazenar a nova senha.  
  
> [!NOTE]  
>  Na cadeia de conexão, a propriedade "Old Password" define SSPROP_AUTH_OLD_PASSWORD, que é a senha atual (provavelmente expirada) que não está disponível por meio de uma propriedade de cadeia de caracteres do provedor.  
  
 O provedor não mantém o valor desta propriedade. Quando esta propriedade é definida, o provedor não usa o pool de conexão na primeira conexão, pois ocorrerá uma nova conexão. Se a alteração da senha tiver êxito, não será possível reutilizar a conexão atual, pois ela ainda conterá a senha antiga, que será inválida após a alteração da senha. Além disso, se o logon for bem-sucedido, o provedor limpará essa propriedade. As tentativas subsequentes de recuperar a senha antiga retornarão VT_EMPTY.  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD nunca deve ser mantido, pois ele é usado somente quando uma senha expirou.  
  
 Sempre que a propriedade "Old Password" é definida, o provedor supõe que está sendo feita uma tentativa de alterar a senha, a menos que a Autenticação do Windows também seja especificada; nesse caso, ela sempre terá precedência.  
  
 Se a Autenticação do Windows for usada, a especificação da senha antiga resultará em DB_E_ERRORSOCCURRED ou DB_S_ERRORSOCCURRED, dependendo de a senha antiga ter sido especificada como REQUIRED ou OPTIONAL, respectivamente, e o valor de status de DBPROPSTATUS_CONFLICTINGBADVALUE será retornado em *dwStatus*. Isto é detectado quando **IDBInitialize::Initialize** é chamado.  
  
 Se uma tentativa de alterar a senha falhar inesperadamente, o servidor retornará o código de erro 18468. Um erro OLEDB padrão é retornado da tentativa de conexão.  
  
 Para obter mais informações sobre o conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, consulte [Propriedades de inicialização e autorização](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte à expiração de senha por meio de uma interface do usuário e programatica  
  
### <a name="odbc-user-interface-password-expiration"></a>Expiração de senha da interface do usuário ODBC  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client dá suporte à expiração de senha por meio de alterações feitas nas caixas de diálogo de **SQL Server logon** .  
  
 Se [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) for chamado e o valor de **DriverCompletion** for definido como SQL_DRIVER_NOPROMPT, a tentativa de conexão inicial falhará se a senha tiver expirado. O valor SQLSTATE 28000 e o valor de código de erro nativo 18487 são retornados por chamadas subsequentes para **SqlError** ou **SQLGetDiagRec**.  
  
 Se **DriverCompletion** tiver sido definido como qualquer outro valor, o usuário verá a caixa de diálogo **SQL Server logon** , independentemente de a senha ter expirado ou não. O usuário pode clicar no botão **Opções** e marcar **Alterar Senha** para alterar a senha.  
  
 Se o usuário clicar em OK e a senha tiver expirado, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solicitará a inserção e a confirmação de uma nova senha usando a caixa de diálogo **alterar SQL Server senha** .  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>Contas bloqueadas e comportamento do prompt do ODBC  
 As tentativas de conexão podem falhar devido ao bloqueio da conta. Se isso ocorrer após a exibição da caixa de diálogo **Logon do SQL Server**, a mensagem de erro do servidor será exibida para o usuário e a tentativa de conexão será anulada. Isso também poderá ocorrer após a exibição da caixa de diálogo **Alterar Senha do SQL Server** se o usuário inserir um valor incorreto para a senha antiga. Neste caso, a mesma mensagem de erro será exibida e a tentativa de conexão será anulada.  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>Contas bloqueadas, expiração de senha e pool de conexão do ODBC  
 Uma conta pode ser bloqueada ou sua senha pode expirar enquanto a conexão ainda está ativa em um pool de conexão. O servidor verifica senhas expiradas e contas bloqueadas em duas ocasiões. A primeiro ao criar uma conexão pela primeira vez. A segunda ocasião é ao redefinir a conexão, quando ela é tirada do pool.  
  
 Quando a tentativa de redefinição falha, a conexão é removida do pool e um erro é retornado.  
  
### <a name="odbc-programmatic-password-expiration"></a>Expiração de senha programática do ODBC  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client dá suporte à expiração de senha por meio da adição do atributo SQL_COPT_SS_OLDPWD, que é definido antes da conexão com o servidor usando a função [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) .  
  
 O atributo SQL_COPT_SS_OLDPWD do identificador de conexão referencia a senha expirada. Não há nenhum atributo de cadeia de conexão para esse atributo, pois isto interferiria com o pool de conexão. Se o logon tiver êxito, o driver limpará esse atributo.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client retorna SQL_ERROR em quatro casos para esse recurso: expiração de senha, conflito de política de senha, bloqueio de conta e quando a propriedade de senha antiga é definida ao usar a autenticação do Windows. O driver retorna as mensagens de erro apropriadas ao usuário quando [SQLGetDiagField](../../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md) é invocado.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
