---
description: Conectar-se ao SQL Server (SybaseToSQL)
title: Conectar-se ao SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 30179b25-409b-4e23-bc73-2f226657098f
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 115b5ca1eadac2e8042abcc6fae7add920889155
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372482"
---
# <a name="connect-to-sql-server-sybasetosql"></a>Conectar-se ao SQL Server (SybaseToSQL)
Use a caixa de diálogo **conectar a SQL Server** para se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você deseja migrar para o. Para acessar a caixa de diálogo **conectar a SQL Server** , no menu **arquivo** , clique em **conectar-se a SQL Server**.  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
Insira ou selecione a instância do SQL Server à qual se conectar. Por padrão, a instância conectada ao mais recentemente é exibida.  
  
-   Se você estiver se conectando à instância padrão no computador local, poderá inserir **localhost** ou um ponto (**.**).  
  
-   Se você estiver se conectando à instância padrão em outro computador, insira o nome do computador.  
  
-   Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador, uma barra invertida e o nome da instância, como *meuservidor* \\ *MyInstance*.  
  
**Porta do servidor**  
Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver configurada para aceitar conexões na porta padrão (1433), insira o número da porta. Caso contrário, deixe esse valor em branco.  
  
**Banco de dados**  
Especifique o banco de dados para o qual os objetos e a migração são migrados. Essa opção não está disponível ao reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Autenticação**  
Selecione o método de autenticação que é usado para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para usar sua conta atual do Windows, selecione Autenticação do Windows. Para especificar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon e uma senha, selecione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.  
  
**Nome de usuário**  
Se você estiver usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação do, insira o logon para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você estiver usando a autenticação do Windows, essa opção não estará disponível.  
  
**Senha**  
Se você estiver usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação do, insira a senha para o logon nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você estiver usando a autenticação do Windows, essa opção não estará disponível.  
  
**Criptografar conexão**  
Se você quiser se conectar com segurança ao SQL Server, faça uso da conexão criptografar marcando a caixa de seleção **criptografar conexão** .  
  
**Confiar em Certificado do Servidor**  
Se você quiser usar essa opção, marque a caixa de seleção **certificado de servidor confiável** .  
  
> [!NOTE]  
> Para habilitar o **certificado de servidor confiável**, "criptografar" deve ser definido como **true**.  
  
