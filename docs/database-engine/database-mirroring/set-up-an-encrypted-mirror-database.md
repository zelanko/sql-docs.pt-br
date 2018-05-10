---
title: Configurar um banco de dados espelho criptografado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: high-availability
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cryptography [SQL Server], database mirroring
- encryption [SQL Server], database mirroring
- database master key [SQL Server], database mirroring
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 7329a575-be29-46e0-abc6-1344db37920c
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 51bf32a3699aaf32606246fe038c3ecd39e1b9a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-an-encrypted-mirror-database"></a>Configurar um banco de dados espelho criptografado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para habilitar a descriptografia automática da chave mestra do banco de dados de um banco de dados espelho, forneça a senha usada para criptografar a chave mestra para a instância de servidor espelho. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores incluem mecanismos para transferir a senha. Use **sp_control_dbmasterkey_password** para criar uma credencial para a chave mestra de banco de dados antes de você iniciar o espelhamento de banco de dados. Você deve repetir este processo para todos os bancos de dados que serão espelhados. Para obter mais informações, veja [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md).  
  
> [!CAUTION]  
>  Não habilite a descriptografia de failover de um banco de dados que deve permanecer inacessível a **sa** e outros principais de servidor altamente privilegiados. É possível configurar um banco de dados de forma que sua hierarquia fundamental não possa ser descriptografada pela chave mestra de serviço. Essa opção tem suporte como defesa para bancos de dados que contêm informações que não deveria ser acessíveis a **sa** ou outros principais de servidor altamente privilegiados. Se você habilitar a descriptografia de failover desse banco de dados, removerá essa defesa, permitindo que **sa** e outros principais de servidor altamente privilegiados descriptografem o banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
  
  
