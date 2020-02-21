---
title: Autenticação no SQL Server
description: Descreve logons e a autenticação no SQL Server e fornece links para recursos adicionais.
ms.date: 09/26/2019
dev_langs:
- csharp
ms.assetid: 646ddbf5-dd4e-4285-8e4a-f565f666c5cc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 115b4810fbe890862dfb63e278a583b3e12dbf54
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75250893"
---
# <a name="authentication-in-sql-server"></a>Autenticação no SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O SQL Server dá suporte a dois modos de autenticação, autenticação do Windows e modo misto.  
  
- A autenticação do Windows é o padrão, e é geralmente conhecida como segurança integrada porque esse modelo de segurança do SQL Server está integrado com o Windows. Contas específicas de usuário e de grupo do Windows são confiáveis para fazer logon no SQL Server. Os usuários do Windows que já foram autenticados não precisam apresentar credenciais adicionais.  
  
- O modo misto oferece suporte à autenticação pelo Windows e pelo SQL Server. Os pares de nome de usuário e senha são mantidos dentro do SQL Server.  
  
> [!IMPORTANT]
> Recomendamos usar a autenticação do Windows sempre que possível. A autenticação do Windows usa uma série de mensagens criptografadas para autenticar usuários no SQL Server. Quando os logons do SQL Server são usados, os nomes e as senhas de logon criptografados do SQL Server são passados pela rede, o que os torna menos seguros.  
  
Com a autenticação do Windows, os usuários já estão conectados no Windows e não precisam fazer logon separadamente no SQL Server. O `SqlConnection.ConnectionString` a seguir especifica a autenticação do Windows sem exigir que os usuários informem um nome de usuário ou senha.  
  
```csharp
"Server=MSSQL1;Database=AdventureWorks;Integrated Security=true;  
```  
  
> [!NOTE]
> Os logons são diferentes dos usuários de banco de dados. Você precisa mapear logons ou grupos do Windows para usuários ou funções de banco de dados em uma operação separada. Em seguida, conceda permissões a usuários ou funções para acessar objetos de banco de dados.  
  
## <a name="authentication-scenarios"></a>Cenários de autenticação  
A autenticação do Windows é geralmente a melhor opção nas seguintes situações:  
  
- Há um controlador de domínio.  
  
- O aplicativo e o banco de dados estão no mesmo computador.  
  
- Você está usando uma instância do SQL Server Express ou LocalDB.  
  
Os logons do SQL Server geralmente são usados nas seguintes situações:  
  
- Se você tiver um grupo de trabalho.  
  
- Os usuários se conectam de diferentes domínios não confiáveis.  
  
- Aplicativos de Internet, como o ASP.NET.  
  
> [!NOTE]
> Especificar a autenticação do Windows não desabilita os logons do SQL Server. Use a instrução ALTER LOGIN DISABLE do Transact-SQL para desabilitar logons do SQL Server com privilégios elevados.  
  
## <a name="login-types"></a>Tipos de logon  
O SQL Server dá suporte a três tipos de logon:  
  
- Uma conta de usuário do Windows local ou uma conta de domínio confiável. O SQL Server depende do Windows para autenticar as contas de usuário do Windows.  
  
- Grupo do Windows. Permitir acesso a um grupo do Windows permite acesso a todos os logons de usuário do Windows que são membros do grupo.  
  
- Logon do SQL Server. O SQL Server armazena o nome de usuário e um hash da senha no banco de dados mestre, usando métodos de autenticação interna para verificar tentativas de logon.  
  
> [!NOTE]
> O SQL Server fornece os logons criados de certificados ou chaves assimétricas que são usados somente para assinatura de código. Eles não podem ser usados para a conexão com o SQL Server.  
  
## <a name="mixed-mode-authentication"></a>Autenticação de modo misto  
Se você deve usar a autenticação de modo misto, deverá criar os logons do SQL Server, que são armazenados no SQL Server. Em seguida, você terá que fornecer o nome de usuário e a senha do SQL Server em tempo de execução.  
  
> [!IMPORTANT]
> O SQL Server é instalado com um logon do SQL Server chamado `sa` (uma abreviação de "administrador do sistema"). Atribua uma senha forte ao logon do `sa` e não use o logon do `sa` em seu aplicativo. O logon do `sa` mapeia para a função de servidor fixa `sysadmin`, que tem credenciais administrativas irrevogáveis no servidor inteiro. Não haverá limites para o dano potencial se um invasor obtiver acesso como administrador do sistema. Todos os membros do grupo `BUILTIN\Administrators` do Windows (grupo do administrador local) são membros da função `sysadmin` por padrão, mas podem ser removidos dessa função.  
  
> [!IMPORTANT]
> Concatenar cadeias de conexão da entrada do usuário pode deixá-lo vulnerável a um ataque de injeção de cadeia de conexão. Use o <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> para criar cadeias de conexão sintaticamente válidas em tempo de execução. 
  
## <a name="external-resources"></a>Recursos externos  
Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Entidades](../../../relational-databases/security/authentication-access/principals-database-engine.md)|Descreve logons e outras entidades de segurança no SQL Server.|  
  
## <a name="next-steps"></a>Próximas etapas
- [Cenários de segurança de aplicativo no SQL Server](application-security-scenarios-sql-server.md)
