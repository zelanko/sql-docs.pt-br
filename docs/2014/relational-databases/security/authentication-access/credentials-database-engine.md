---
title: Credenciais (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: faa2b5be7cf6918b5d5232763a96ed4dbbc89e51
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055361"
---
# <a name="credentials-database-engine"></a>Credenciais (Mecanismo de Banco de Dados)
  Uma credencial é um registro que contém as informações de autenticação(credenciais) necessárias para conectar-se a um recurso fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Essas informações são usadas internamente pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A maioria das credenciais contém um nome e uma senha de usuário do Windows.  
  
 As informações armazenadas em uma credencial permite que um usuário quem se conectou com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por meio da Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] acesse os recursos fora da instância do servidor. Quando o recurso externo for o Windows, o usuário é autenticado como o usuário de Windows especificado na credencial. Uma única credencial pode ser mapeada para vários logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . No entanto, um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] só pode ser mapeado para uma credencial.  
  
 Credenciais de sistema são criadas automaticamente e associadas a pontos de extremidade específicos. Nomes para credenciais de sistema iniciam com dois sinais de hash (##).  
  
 Para obter mais informações sobre credenciais, consulte a exibição do catálogo [Sys. Credentials](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) .  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Criar uma](../authentication-access/create-a-credential.md) credencial criar credencial [&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
 [Protegendo o SQL Server](../securing-sql-server.md)  
  
  
