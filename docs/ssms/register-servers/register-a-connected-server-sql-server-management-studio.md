---
description: Registrar-se a um servidor conectado (SQL Server Management Studio)
title: Registrar um servidor conectado
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], register connected servers
- connected server registrations [SQL Server]
ms.assetid: 77deb5f5-0f80-484f-8b8b-29afa67ec18f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 07/28/2016
ms.openlocfilehash: bcac629eef24a68f66d1e7043f5cedb5ff8923e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497370"
---
# <a name="register-a-connected-server-sql-server-management-studio"></a>Registrar-se a um servidor conectado (SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Este tópico descreve como registrar um servidor conectado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SSMS ( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ). Registrando o servidor, você pode salvar a informação de conexão para os servidores que você acessa frequentemente. Um servidor pode ser registrado antes de ser conectado, ou na hora da conexão no Pesquisador de Objetos.  Você pode exibir os servidores registrados no SSMS procurando **Exibir**\\**Servidores Registrados** no menu.
  
 **Neste tópico**  
  
-   **Para registrar um servidor, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-register-a-connected-server"></a>Para registrar um servidor conectado  
  
No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor ao qual você já está conectado e então clique em **Registrar**.
  
**Nome do servidor**  
Este campo usa como padrão o nome do servidor ao qual você está conectado.  Opcionalmente, você pode digitar um nome de servidor ou escolher um na lista suspensa.

**Autenticação**  
Dois modos de autenticação estão disponíveis quando se estabelece conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

-    **Autenticação do Windows**  
O modo de Autenticação do Windows permite que um usuário se conecte por meio de uma conta de usuário do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. 

-    **Autenticação do SQL Server**   
Quando um usuário se conecta com um nome de logon e senha especificados em uma conexão não confiável, o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] efetua a autenticação, verificando se foi definida uma conta de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se a senha especificada corresponde a uma senha registrada previamente. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tiver uma conta de logon definida, ocorrerá falha na autenticação e o usuário receberá uma mensagem de erro.

     > [!IMPORTANT]  
     > [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] Para obter mais informações, veja [Escolher um modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md).  

     -    **Nome de usuário**  
Mostra o nome de usuário atual com o que você está se conectando. Essa opção somente leitura só estará disponível se você tiver optado por conectar-se usando a Autenticação do Windows. Para alterar **Nomes de usuários**, faça logon no computador como um usuário diferente. 

     -    **Logon**  
Insira o logon com o qual se conectar. Esta opção só estará disponível se você tiver optado por conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

     -    **Senha**  
Digite a senha do logon. Esta opção poderá ser editada somente se você tiver optado por conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 

     -    **Lembrar senha**  
Selecione para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criptografe e armazene a senha que você acabou de digitar. Esta opção só será exibida se você tiver optado por conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

          > [!NOTE]  
          > Caso você tenha armazenado a senha e não queira mais fazê-lo, desmarque essa caixa de seleção e clique em **Salvar**.  

**Nome do servidor registrado**  
O nome que você deseja exibir em Servidores Registrados. Esse nome não precisa corresponder à caixa **Nome do servidor** .  
  
**Descrição do servidor registrado**  
Digite uma descrição opcional do servidor.  
  
**Test**  
Clique para testar a conexão com o servidor selecionado em **Nome do servidor**.  
  
**Salvar**  
Clique para salvar as configurações do servidor registrado. 

## <a name="see-also"></a>Consulte Também

[Criar um novo servidor registrado (SQL Server Management Studio)](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)
