---
title: "Limitações de segurança para o SQL Server no Linux | Microsoft Docs"
description: "Este tópico descreve o SQL Server no Linux restrições."
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 6823b8a9cd3f92781d0fd3518f50b8866ba12d48
ms.contentlocale: pt-br
ms.lasthandoff: 09/21/2017

---
# <a name="security-limitations-for-sql-server-on-linux"></a>Limitações de segurança para o SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Atualmente, o SQL Server no Linux tem as seguintes limitações:

* Uma política de senha padrão é fornecida. MUST_CHANGE é a única opção que você pode configurar.  
* Não há suporte para o gerenciamento extensível de chaves. 
* Não há suporte para usar as chaves armazenadas no cofre de chaves do Azure.
* SQL Server gera seu próprio certificado autoassinado para criptografia de conexões. Atualmente, o SQL Server não pode ser configurado para usar um usuário fornecido um certificado para SSL ou TLS. 

Para obter mais informações sobre os recursos de segurança disponíveis no SQL Server, consulte o [Central de segurança do mecanismo de banco de dados do SQL Server e banco de dados do SQL Azure](/sql-docs/docs/relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database).

## <a name="next-steps"></a>Próximas etapas

Para tarefas comuns de segurança, consulte [começar com recursos de segurança do SQL Server no Linux](sql-server-linux-security-get-started.md).   
Para um script alterar o TCP número da porta, os diretórios do SQL Server e definir sinalizadores de rastreamento ou de agrupamento, consulte [configurar o SQL Server no Linux com mssql conf](sql-server-linux-configure-mssql-conf.md).

