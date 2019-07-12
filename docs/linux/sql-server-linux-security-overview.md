---
title: Limitações de segurança para SQL Server no Linux
description: Este artigo descreve o SQL Server no Linux restrições.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.openlocfilehash: 033390cb2776988179fc40b2f3a2d9e65b98a05a
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834721"
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Limitações de segurança para SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Atualmente, o SQL Server no Linux tem as seguintes limitações:

* Uma política de senha padrão é fornecida. MUST_CHANGE é a única opção que você pode configurar.  
* Não há suporte para o gerenciamento extensível de chaves. 
* Não há suporte para o uso de chaves armazenadas no cofre de chaves do Azure.
* SQL Server gera seu próprio certificado autoassinado para criptografar conexões. SQL Server pode ser configurado para usar um usuário fornecido o certificado para TLS. 

Para obter mais informações sobre os recursos de segurança disponíveis no SQL Server, consulte o [Central de segurança do mecanismo de banco de dados do SQL Server e banco de dados SQL](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="next-steps"></a>Próximas etapas

Para tarefas comuns de segurança, consulte [Introdução aos recursos de segurança do SQL Server no Linux](sql-server-linux-security-get-started.md). Para obter um script alterar o TCP número da porta, os diretórios do SQL Server e configurar o agrupamento ou sinalizadores de rastreamento, consulte [configurar o SQL Server no Linux com o mssql-conf](sql-server-linux-configure-mssql-conf.md).
