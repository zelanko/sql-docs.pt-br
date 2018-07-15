---
title: Configurar um banco de dados espelho criptografado | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 550531519953de312f04655f5e7cf58c80a07448
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279122"
---
# <a name="set-up-an-encrypted-mirror-database"></a>Configurar um banco de dados espelho criptografado

Para habilitar a descriptografia automática da chave mestra do banco de dados de um banco de dados espelho, forneça a senha usada para criptografar a chave mestra para a instância de servidor espelho. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores incluem mecanismos para transferir a senha. Use **sp_control_dbmasterkey_password** para criar uma credencial para a chave mestra de banco de dados antes de você iniciar o espelhamento de banco de dados. Você deve repetir este processo para todos os bancos de dados que serão espelhados. Para obter mais informações, veja [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql).
  
> [!CAUTION]  
>  Não habilite a descriptografia de failover de um banco de dados que deve permanecer inacessível a **sa** e outros principais de servidor altamente privilegiados. É possível configurar um banco de dados de forma que sua hierarquia fundamental não possa ser descriptografada pela chave mestra de serviço. Essa opção tem suporte como defesa para bancos de dados que contêm informações que não deveria ser acessíveis a **sa** ou outros principais de servidor altamente privilegiados. Se você habilitar a descriptografia de failover desse banco de dados, removerá essa defesa, permitindo que **sa** e outros principais de servidor altamente privilegiados descriptografem o banco de dados.  


<!-- Note: We cannot append '?view=sql-server-2016' to these, even tho in theory we might want to. -->

## <a name="see-also"></a>Consulte também

[sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql)

[CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)

[ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql)

[Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)

[Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)

