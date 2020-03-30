---
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
ms.openlocfilehash: d3968c5c8f04cba8581dfdd44ac847f7010de994
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73595621"
---
# <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>Gerenciar chaves para Always Encrypted com enclaves seguros
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

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
