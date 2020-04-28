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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68141084"
---
# <a name="connect-to-sql-server-db2tosql"></a>Conectar-se ao SQL Server (DB2ToSQL)
Use a caixa de diálogo **conectar a SQL Server** para se conectar à instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do que você deseja migrar para o. Para acessar a caixa de diálogo **conectar a SQL Server** , no menu **arquivo** , clique em **conectar-se a SQL Server**.  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
Insira ou selecione a instância do SQL Server à qual se conectar. Por padrão, a instância conectada ao mais recentemente é exibida.  
  
-   Se você estiver se conectando à instância padrão no computador local, poderá inserir **localhost** ou um ponto (**.**).  
  
-   Se você estiver se conectando à instância padrão em outro computador, insira o nome do computador.  
  
-   Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador, uma barra invertida e o nome da instância, como *meuservidor*\\*MyInstance*.  
  
**Porta do servidor**  
Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver configurada para aceitar conexões na porta padrão (1433), insira o número da porta. Caso contrário, deixe esse valor em branco.  
  
**Backup de banco de dados**  
Especifique o banco de dados para o qual os objetos e a migração são migrados. Essa opção não está disponível ao reconectar-se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ao.  
  
**Autenticação**  
Selecione o método de autenticação que é usado para se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]conectar ao. Para usar sua conta atual do Windows, selecione Autenticação do Windows. Para especificar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon e uma senha, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selecione autenticação.  
  
**Nome de usuário**  
Se você estiver usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação do, insira o logon para essa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]instância do. Se você estiver usando a autenticação do Windows, essa opção não estará disponível.  
  
**Senha**  
Se você estiver usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação do, insira a senha para o logon nessa instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. Se você estiver usando a autenticação do Windows, essa opção não estará disponível.  
  
**Criptografar conexão**  
Se você quiser se conectar com segurança ao SQL Server, faça uso da conexão criptografar marcando a caixa de seleção **criptografar conexão** .  
  
**Confiar no certificado do servidor**  
Se você quiser usar essa opção, marque a caixa de seleção **certificado de servidor confiável** .  
  
> [!NOTE]  
> Para habilitar o **certificado de servidor confiável**, "criptografar" deve ser definido como **true**.  
  
