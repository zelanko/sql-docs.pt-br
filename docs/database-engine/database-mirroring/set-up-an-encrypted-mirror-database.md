---
title: "Configurar um banco de dados espelho criptografado | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "criptografia [SQL Server], espelhamento de banco de dados"
  - "criptografia [SQL Server], espelhamento de banco de dados"
  - "chave mestra do banco de dados [SQL Server], espelhamento de banco de dados"
  - "banco de dados espelho [SQL Server]"
  - "espelhamento de banco de dados [SQL Server], segurança"
ms.assetid: 7329a575-be29-46e0-abc6-1344db37920c
caps.latest.revision: 24
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 24
---
# Configurar um banco de dados espelho criptografado
  Para habilitar a descriptografia automática da chave mestra do banco de dados de um banco de dados espelho, forneça a senha usada para criptografar a chave mestra para a instância de servidor espelho. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores incluem mecanismos para transferir a senha. Use **sp_control_dbmasterkey_password** para criar uma credencial para a chave mestra de banco de dados antes de você iniciar o espelhamento de banco de dados. Você deve repetir este processo para todos os bancos de dados que serão espelhados. Para obter mais informações, veja [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md).  
  
> [!CAUTION]  
>  Não habilite a descriptografia de failover de um banco de dados que deve permanecer inacessível a **sa** e outros principais de servidor altamente privilegiados. É possível configurar um banco de dados de forma que sua hierarquia fundamental não possa ser descriptografada pela chave mestra de serviço. Essa opção tem suporte como defesa para bancos de dados que contêm informações que não deveria ser acessíveis a **sa** ou outros principais de servidor altamente privilegiados. Se você habilitar a descriptografia de failover desse banco de dados, removerá essa defesa, permitindo que **sa** e outros principais de servidor altamente privilegiados descriptografem o banco de dados.  
  
## Consulte também  
 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
  
  