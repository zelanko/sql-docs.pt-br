---
title: Conectar-se ao SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: bc14a072-8949-4ee0-a4b4-ada55fe8df5c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3d96be29aa74d3903e47f20ec6841b4a20135727
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141084"
---
# <a name="connect-to-sql-server-db2tosql"></a>Conectar-se ao SQL Server (DB2ToSQL)
Use o **conectar-se ao SQL Server** caixa de diálogo para se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você deseja migrar para o. Para acessar o **conectar-se ao SQL Server** caixa de diálogo do **arquivo** menu, clique em **conectar-se ao SQL Server**.  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
Insira ou selecione a instância do SQL Server para se conectar ao. Por padrão, a instância que você conectado mais recentemente é exibida.  
  
-   Se você estiver se conectando à instância padrão no computador local, você pode inserir **localhost** ou um ponto ( **.** ).  
  
-   Se você estiver se conectando à instância padrão em outro computador, digite o nome do computador.  
  
-   Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador, uma barra invertida e o nome da instância, como *meuservidor*\\*MyInstance*.  
  
**Porta do servidor**  
Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está configurado para aceitar conexões em que o padrão da porta (1433), insira o número da porta. Caso contrário, deixe esse valor em branco.  
  
**Backup de banco de dados**  
Especifique o banco de dados para migrar objetos e dados. Essa opção não está disponível quando se reconectar à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Autenticação**  
Selecione o método de autenticação que é usado para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para usar sua conta atual do Windows, selecione autenticação do Windows. Para especificar uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon e senha, selecione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.  
  
**Nome de usuário**  
Se você estiver usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, insira o logon para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você estiver usando autenticação do Windows, essa opção não está disponível.  
  
**Senha**  
Se você estiver usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, insira a senha para o logon naquela instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você estiver usando autenticação do Windows, essa opção não está disponível.  
  
**Criptografar conexão**  
Se você quiser se conectar com segurança para o SQL Server, fazer uso de conexão Encrypt, verificando o **criptografar conexão** caixa de seleção.  
  
**Confiar em Certificado do Servidor**  
Se você quiser usar essa opção, selecione a **confiar em certificado do servidor** caixa de seleção.  
  
> [!NOTE]  
> Para habilitar **confiar em certificado do servidor**, "Criptografar" deve ser definida como **verdadeiro**.  
  
