---
description: Consultar colunas usando o Always Encrypted com enclaves seguros
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
ms.openlocfilehash: 8daabf320e0f736bcfabc5addb8508320b10bb8f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88482214"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>Consultar colunas usando o Always Encrypted com enclaves seguros
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

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

