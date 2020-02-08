---
title: Consultar colunas usando o Always Encrypted com enclaves seguros | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d0a522d6deb01169189d6f5faaf7ba2f189d1522
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73595501"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>Consultar colunas usando o Always Encrypted com enclaves seguros
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Este artigo captura considerações gerais para executar consultas em colunas criptografadas usando um enclave seguro no lado do servidor para o [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md). 

Os seguintes tipos de consultas envolvem o uso de um enclave seguro:
- Consultas que disparam operações criptográficas in-loco usando chaves habilitadas para enclave – confira [Configurar criptografia de coluna in-loco com Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md).
- *Consultas avançadas* – comparações de intervalo ou operações de correspondência de padrões em colunas criptografadas usando criptografia aleatória e chaves habilitadas para enclave.
- Consultas que criam ou atualizam índices em colunas criptografadas usando criptografia aleatória e chaves habilitadas para enclave. Para obter mais informações, confira [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md).

> [!NOTE]
> Há suporte para consultas e índices avançados somente em colunas habilitadas para enclave (colunas criptografadas com chaves de criptografia de coluna habilitadas para enclave) que usam criptografia aleatória. A criptografia determinística não dá suporte a consultas nem índices avançados.

> [!NOTE]
> Operações avançadas em colunas de cadeia de caracteres criptografadas exigem que as colunas usem ordenações com ordem de classificação binary2 (ordenações BIN2). 


## <a name="next-steps"></a>Próximas etapas
- [Consultar colunas usando o Always Encrypted com enclaves seguros com o SSMS](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="see-also"></a>Consulte Também
- [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)

