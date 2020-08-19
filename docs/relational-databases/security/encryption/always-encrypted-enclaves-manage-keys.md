---
description: Gerenciar chaves para Always Encrypted com enclaves seguros
title: Gerenciar chaves para Always Encrypted com enclaves seguros | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 8b70fba2edc9a3ba948afa653acbe79607b8eb51
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420310"
---
# <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>Gerenciar chaves para Always Encrypted com enclaves seguros
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

O [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) estende o gerenciamento de chaves para o [Always Encrypted](always-encrypted-database-engine.md) introduzindo chaves habilitadas para enclave: 

- **Chave mestra de coluna habilitada para enclave** – uma chave mestra de coluna que é criada com a propriedade `ENCLAVE_COMPUTATIONS` especificada no objeto de metadados de chave mestra de coluna no banco de dados. 
- **Chave de criptografia de coluna habilitada para enclave** – uma chave de criptografia de coluna que é criptografada com uma chave mestra de coluna habilitada para enclave. Somente as chaves de criptografia de coluna habilitadas para enclave podem ser usadas para computações dentro de um enclave seguro no servidor. 

As diretrizes e os processos gerais para [gerenciar chaves de Always Encrypted](overview-of-key-management-for-always-encrypted.md) se aplicam ao gerenciamento de chaves habilitadas para enclave. 

## <a name="managing-keys"></a>Como gerenciar chaves

Os artigos a seguir discutem os aspectos específicos do gerenciamento de chaves habilitadas para enclave.

- [Provisionar chaves habilitadas para enclave](always-encrypted-enclaves-provision-keys.md)
- [Girar chaves habilitadas para enclave](always-encrypted-enclaves-rotate-keys.md)

## <a name="next-steps"></a>Próximas etapas
- [Provisionar chaves habilitadas para enclave](always-encrypted-enclaves-provision-keys.md)

## <a name="see-also"></a>Consulte Também  
- [Visão geral do gerenciamento de chaves do Always Encrypted](overview-of-key-management-for-always-encrypted.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
