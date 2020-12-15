---
title: Credenciais (Mecanismo de Banco de Dados) | Microsoft Docs
description: Saiba mais sobre as credenciais no SQL Server. Familiarize-se com as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server.
ms.custom: ''
ms.date: 06/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- principals [SQL Server], credentials
- schemas [SQL Server], credentials
- permissions [SQL Server], credentials
- groups [SQL Server], credentials
- ALTER ANY CREDENTIAL permission
- security [SQL Server], credentials
- authentication [SQL Server], credentials
- users [SQL Server], credentials
- credentials [SQL Server], about credentials
- credentials [SQL Server]
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9bc63a0a3bf2482ea84f1a2f80febb5865892a6d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97406072"
---
# <a name="credentials-database-engine"></a>Credenciais (Mecanismo de Banco de Dados)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Uma credencial é um registro que contém as informações de autenticação(credenciais) necessárias para conectar-se a um recurso fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Essas informações são usadas internamente pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A maioria das credenciais contém um nome e uma senha de usuário do Windows.  
  
 As informações armazenadas em uma credencial permite que um usuário quem se conectou com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por meio da Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] acesse os recursos fora da instância do servidor. Quando o recurso externo for o Windows, o usuário é autenticado como o usuário de Windows especificado na credencial. Uma única credencial pode ser mapeada para um único logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. E um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode ser mapeado para apenas uma credencial.  
  
 Para obter as credenciais que são armazenadas no banco de dados mestre e que podem ser usadas em toda a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], veja [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md). Para obter as credenciais usadas por um banco de dados específico e portátil com esse banco de dados, veja [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
 Credenciais de sistema são criadas automaticamente e associadas a pontos de extremidade específicos. Nomes para credenciais de sistema iniciam com dois sinais de hash (##).  
  
 Para obter mais informações sobre credenciais, consulte as exibições de catálogo [sys.credentials](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) e [sys.database_scoped_credentials](../../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Criar uma credencial](../../../relational-databases/security/authentication-access/create-a-credential.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
 [Protegendo o SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  
