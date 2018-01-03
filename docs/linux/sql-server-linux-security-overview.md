---
title: "Limitações de segurança para o SQL Server no Linux | Microsoft Docs"
description: "Este tópico descreve o SQL Server no Linux restrições."
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.workload: Inactive
ms.openlocfilehash: 989c34ff57fcc6ef0aa561c58043d1073772b63c
ms.sourcegitcommit: 6e016a4ffd28b09456008f40ff88aef3d911c7ba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Limitações de segurança para o SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Atualmente, o SQL Server no Linux tem as seguintes limitações:

* Uma política de senha padrão é fornecida. MUST_CHANGE é a única opção que você pode configurar.  
* Não há suporte para o gerenciamento extensível de chaves. 
* Não há suporte para usar as chaves armazenadas no cofre de chaves do Azure.
* SQL Server gera seu próprio certificado autoassinado para criptografia de conexões. SQL Server pode ser configurado para usar um usuário fornecido um certificado para TLS. 

Para obter mais informações sobre os recursos de segurança disponíveis no SQL Server, consulte o [Central de segurança do mecanismo de banco de dados do SQL Server e banco de dados do SQL Azure](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="next-steps"></a>Próximas etapas

Para tarefas comuns de segurança, consulte [começar com recursos de segurança do SQL Server no Linux](sql-server-linux-security-get-started.md).   
Para um script alterar o TCP número da porta, os diretórios do SQL Server e definir sinalizadores de rastreamento ou de agrupamento, consulte [configurar o SQL Server no Linux com mssql conf](sql-server-linux-configure-mssql-conf.md).
