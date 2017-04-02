---
title: "Credenciais (Mecanismo de Banco de Dados) | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "entidades [SQL Server], credenciais"
  - "esquemas [SQL Server], credenciais"
  - "permissões [SQL Server], credenciais"
  - "grupos [SQL Server], credenciais"
  - "Permissão ALTER ANY CREDENTIAL"
  - "segurança [SQL Server], credenciais"
  - "autenticação [SQL Server], credenciais"
  - "usuários [SQL Server], credenciais"
  - "credenciais [SQL Server], sobre credenciais"
  - "credenciais [SQL Server]"
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Credenciais (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  Uma credencial é um registro que contém as informações de autenticação(credenciais) necessárias para conectar-se a um recurso fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Essas informações são usadas internamente pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A maioria das credenciais contém um nome e uma senha de usuário do Windows.  
  
 As informações armazenadas em uma credencial permite que um usuário quem se conectou com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por meio da Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] acesse os recursos fora da instância do servidor. Quando o recurso externo for o Windows, o usuário é autenticado como o usuário de Windows especificado na credencial. Uma única credencial pode ser mapeada para vários logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. No entanto, um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] só pode ser mapeado para uma credencial.  
  
 Para obter as credenciais que são armazenadas no banco de dados mestre e que podem ser usadas em toda a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], veja [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md). Para obter as credenciais usadas por um banco de dados específico e portátil com esse banco de dados, veja [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
 Credenciais de sistema são criadas automaticamente e associadas a pontos de extremidade específicos. Nomes para credenciais de sistema iniciam com dois sinais de hash (##).  
  
 Para obter mais informações sobre credenciais, veja as exibições de catálogo [sys.credentials](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) e [sys.database_credentials &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-credentials-transact-sql.md).  
  
## Conteúdo relacionado  
 [Criar uma credencial](../../../relational-databases/security/authentication-access/create-a-credential.md) [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md) [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
  
 [Protegendo o SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  