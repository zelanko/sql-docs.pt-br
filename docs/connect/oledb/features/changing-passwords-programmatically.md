---
title: Alterando senhas programaticamente | Microsoft Docs
description: Alterando senhas programaticamente usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], password expiration
- OLE DB Driver for SQL Server, passwords
- passwords [SQL Server], expiration
- MSOLEDBSQL, password expiration
- expiration [OLE DB Driver for SQL Server]
- passwords [SQL Server], modifying
- expired passwords [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, password expiration
- modifying passwords
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8ac5c5c127b67fb872a6b10ffc7bd32ec7458092
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="changing-passwords-programmatically"></a>Alterando senhas programaticamente
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Antes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], quando a senha de um usuário expirava, somente um administrador poderia redefini-la. Começando com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], OLE DB Driver para SQL Server dá suporte a tratamento de expiração de senha programaticamente através do Driver do OLE DB e as alterações para o **logon do SQL Server** caixas de diálogo.  
  
> [!NOTE]  
>  Quando possível, solicite aos usuários que insiram suas credenciais em tempo de execução e que evitem armazená-las em um formato persistente. Se for necessário manter suas credenciais, criptografe-as usando o [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532). Para obter mais informações sobre o uso de senhas, consulte [senhas fortes](../../../relational-databases/security/strong-passwords.md).  
  
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
  
## <a name="ole-db-driver-for-sql-server"></a>Driver do OLE DB para SQL Server  
 O Driver OLE DB para SQL Server dá suporte à expiração de senha que uma interface do usuário e programaticamente.  
  
### <a name="ole-db-user-interface-password-expiration"></a>Expiração de senha da interface do usuário OLE DB  
 O Driver OLE DB para SQL Server dá suporte à expiração de senha por meio de alterações feitas a **logon do SQL Server** caixas de diálogo. Se o valor de DBPROP_INIT_PROMPT for definido como DBPROMPT_NOPROMPT, a tentativa de conexão inicial irá falhar, caso a senha tenha expirado.  
  
 Se DBPROP_INIT_PROMPT tiver sido definida para qualquer outro valor, o usuário vê o **logon do SQL Server** caixa de diálogo, independentemente da senha tenha expirado ou não. O usuário pode clicar no **opções** botão e marque **alterar senha** para alterar a senha.  
  
 Se o usuário clica em Okey e a senha tiver expirado, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solicita que o usuário insira e confirme uma nova senha usando o **alterar senha do SQL Server** caixa de diálogo.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>Contas bloqueadas e comportamento do prompt do OLE DB  
 As tentativas de conexão podem falhar devido ao bloqueio da conta. Se isso ocorrer após a exibição do **logon do SQL Server** caixa de diálogo, a mensagem de erro de servidor é exibida para o usuário e a tentativa de conexão será anulada. Isso também pode ocorrer após a exibição do **alterar senha do SQL Server** caixa de diálogo se o usuário insere um valor incorreto para a senha antiga. Neste caso, a mesma mensagem de erro será exibida e a tentativa de conexão será anulada.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>Contas bloqueadas, expiração de senha e pool de conexão do OLE DB  
 Uma conta pode ser bloqueada ou sua senha pode expirar enquanto a conexão ainda está ativa em um pool de conexão. O servidor verifica senhas expiradas e contas bloqueadas em duas ocasiões. A primeiro ao criar uma conexão pela primeira vez. A segunda ocasião é ao redefinir a conexão, quando ela é tirada do pool.  
  
 Quando a tentativa de redefinição falha, a conexão é removida do pool e um erro é retornado.  
  
### <a name="ole-db-programmatic-password-expiration"></a>Expiração de senha programática do OLE DB  
 O Driver OLE DB para SQL Server dá suporte à expiração de senha por meio da adição da propriedade SSPROP_AUTH_OLD_PASSWORD (tipo VT_BSTR) que foi adicionada ao conjunto de propriedades DBPROPSET_SQLSERVERDBINIT.  
  
 A propriedade "Password" existente referencia DBPROP_AUTH_PASSWORD e é usada para armazenar a nova senha.  
  
> [!NOTE]  
>  Na cadeia de conexão, a propriedade "Old Password" define SSPROP_AUTH_OLD_PASSWORD, que é a senha atual (provavelmente expirada) que não está disponível por meio de uma propriedade de cadeia de caracteres do provedor.  
  
 O provedor não mantém o valor desta propriedade. Quando esta propriedade é definida, o provedor não usa o pool de conexão na primeira conexão, pois ocorrerá uma nova conexão. Se a alteração da senha tiver êxito, não será possível reutilizar a conexão atual, pois ela ainda conterá a senha antiga, que será inválida após a alteração da senha. Além disso, se o logon for bem-sucedido, o provedor limpará essa propriedade. As tentativas subsequentes de recuperar a senha antiga retornarão VT_EMPTY.  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD nunca deve ser mantido, pois ele é usado somente quando uma senha expirou.  
  
 Sempre que a propriedade "Old Password" é definida, o provedor supõe que está sendo feita uma tentativa de alterar a senha, a menos que a Autenticação do Windows também seja especificada; nesse caso, ela sempre terá precedência.  
  
 Se a autenticação do Windows for usada, especificar a senha antiga resulta em DB_E_ERRORSOCCURRED ou DB_S_ERRORSOCCURRED, dependendo se a senha antiga foi especificada como REQUIRED ou OPTIONAL respectivamente e o valor de status de dbpropstatus _ CONFLICTINGBADVALUE é retornado no *dwStatus*. Isso é detectado quando **IDBInitialize:: Initialize** é chamado.  
  
 Se uma tentativa de alterar a senha falhar inesperadamente, o servidor retornará o código de erro 18468. Um erro OLEDB padrão é retornado da tentativa de conexão.  
  
 Para obter mais informações sobre o conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, consulte [propriedades de inicialização e autorização](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  

  
## <a name="see-also"></a>Consulte também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
