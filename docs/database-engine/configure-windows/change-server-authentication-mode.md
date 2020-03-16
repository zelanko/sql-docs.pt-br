---
title: Alterar o modo de autenticação do servidor | Microsoft Docs
ms.custom: ''
ms.date: 02/18/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a8ffafae40991d6134925481409b5898b06c20c4
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288560"
---
# <a name="change-server-authentication-mode"></a>Alterar o modo de autenticação do servidor

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Este tópico descreve como alterar o modo de autenticação de servidor no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Durante a instalação, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] é definido como **Modo de Autenticação do Windows** ou **Modo de Autenticação do SQL Server e do Windows**. Após a instalação, você pode alterar o modo de autenticação a qualquer momento.

Se **modo de Autenticação do Windows** for selecionado durante a instalação, o logon sa será desabilitado e uma senha será atribuída por meio da instalação. Se você alterar posteriormente o modo de autenticação para **Modo de Autenticação do SQL Server e do Windows**, o logon sa permanecerá desabilitado. Para usar o logon sa, use a instrução ALTER LOGIN para habilitar o logon de sa e atribuir uma nova senha. O logon sa só pode se conectar ao servidor usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

## <a name="before-you-begin"></a>Antes de começar

A conta sa é uma conta bem conhecida do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e geralmente é visada por usuários mal-intencionados. Não habilite a conta sa, a menos que seu aplicativo exija isso. É muito importante que você use uma senha segura para o logon de sa.

## <a name="change-authentication-mode-with-ssms"></a>Alterar o modo de autenticação com o SSMS

1. No Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique com o botão direito do mouse no servidor e clique em **Propriedades**.

2. Na página **Segurança** , em **Autenticação de Servidor**, selecione o novo modo de autenticação de servidor e clique em **OK**.

3. Na caixa de diálogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique em **OK** para confirmar o requisito para reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

4. No Object Explorer, clique com o botão direito do mouse no seu servidor, e em seguida, clique em **Reiniciar**. Se o agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver em execução, ele também deverá ser reiniciado.

## <a name="enable-sa-login"></a>Habilitar logon SA

Você pode habilitar o logon **sa** com o SSMS ou o T-SQL.

### <a name="use-ssms"></a>Usar SSMS

1. No Pesquisador de Objetos, expanda **Segurança**, expanda Logons, clique com o botão direito do mouse em **sa**e clique em **Propriedades**.

2. Na página **Geral**, talvez seja necessário criar e confirmar uma senha para o logon **sa**.

3. Na página **Status** , na seção **Logon** , clique em **Habilitado**e, em seguida, em **OK**.

### <a name="using-transact-sql"></a>Usando o Transact-SQL

O exemplo a seguir habilita o logon sa e define uma nova senha. Substitua `<enterStrongPasswordHere>` por uma senha forte antes de executá-lo.

```sql  
ALTER LOGIN sa ENABLE ;  
GO  
ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
GO  
```

## <a name="change-authentication-mode-t-sql"></a>Alterar o modo de autenticação (T-SQL)

O exemplo a seguir altera a Autenticação do Servidor do modo misto (Windows + SQL) para somente Windows.

> [!CAUTION]
> O exemplo a seguir usa um procedimento armazenado estendido para modificar o Registro do servidor. Poderão ocorrer problemas graves se você modificar o Registro incorretamente. Esses problemas podem exigir a reinstalação do sistema operacional. A Microsoft não pode garantir que esses problemas possam ser resolvidos. Modifique o Registro por conta própria.

```sql
USE [master]
GO
EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', 
     N'Software\Microsoft\MSSQLServer\MSSQLServer',
     N'LoginMode', REG_DWORD, 1
GO
```

## <a name="see-also"></a>Confira também

 [Senhas fortes](../../relational-databases/security/strong-passwords.md)   
 [Considerações de segurança para uma Instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md) [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md) [Conectar-se ao SQL Server quando os administradores do sistema estiverem bloqueados](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)
