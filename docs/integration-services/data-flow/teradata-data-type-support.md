---
title: Suporte ao tipo de dados do Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f83f028772a93dbd2104d9f449fcd7aa3b1be0d8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74543004"
---
# <a name="data-type-support"></a>Suporte do tipo de dados

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Os componentes do SSIS usam a API de transporte paralelo do Teradata (API TPT) para carregar e transferir dados de e para o banco de dados do Teradata, portanto, somente o tipo de dado compatível da API TPT pode ser usado no SSIS.

> [!NOTE]
>
> Os tipos de dados TIME, TIMESTAMP e INTERVAL no Teradata são tratados pela API TPT como cadeias de caracteres de tamanho fixo. Eles são tratados pelos componentes do SSIS para Teradata como uma cadeia de caracteres.

## <a name="data-type-mapping"></a>Mapeamento de tipo de dados

A tabela a seguir mostra os tipos de dados do banco de dados do Teradata e o mapeamento padrão para os tipos de dados do SSIS. Ela também mostra os tipos de dados não compatíveis do Teradata.

|Tipo de dados SQL|Tipo de dados SSIS|
|:-|:-|
|DECIMAL/NUMERIC|DT_NUMERIC|
|BYTEINT|DT_I1|
|SMALLINT|DT_I2|
|INTEGER|DT_I4|
|FLOAT/REAL/DOUBLE PRECISION|DT_R8|
|DATE|DT_DBDATE|
|TIME<br>TIME(n)|DT_STR|
|timestamp<br>TIMESTAMP (n)|DT_STR|
|TIME WITH TIMEZONE<br>TIME(n) WITH TIMEZONE|DT_STR|
|TIMESTAMP WITH TIMEZONE<br>TIMESTAMP(n) WITH TIMEZONE|DT_STR|
|INTERVAL YEAR<br>INTERVAL YEAR (n)|DT_STR|
|INTERVAL YEAR TO MONTH<br>INTERVAL YEAR (n) TO MONTH|DT_STR|
|INTERVAL MONTH<br>INTERVAL MONTH (n)|DT_STR|
|INTERVAL DAY<br>INTERVAL DAY (n)|DT_STR|
|INTERVAL DAY TO HOUR<br>INTERVAL DAY (n) TO HOUR|DT_STR|
|INTERVAL DAY TO MINUTE<br>INTERVAL DAY (n) TO MINUTE|DT_STR|
|INTERVAL DAY TO SECOND<br>INTERVAL DAY (n) TO SECOND<br>INTERVAL DAY TO SECOND (m)<br>INTERVAL DAY (n) TO SECOND (m)|DT_STR|
|INTERVAL HOUR<br>INTERVAL HOUR (n)|DT_STR|
|INTERVAL HOUR TO MINUTE<br>INTERVAL HOUR (n) TO MINUTE|DT_STR
|INTERVAL HOUR TO SECOND<br>INTERVAL HOUR (n) TO SECOND<br>INTERVAL HOUR TO SECOND (m)<br>INTERVAL HOUR (n) TO SECOND (m)|DT_STR|
|INTERVAL MINUTE<br>INTERVAL MINUTE (n)|DT_STR|
|INTERVAL MINUTE TO SECOND<br>INTERVAL MINUTE (n) TO SECOND<br>INTERVAL MINUTE TO SECOND (m)<br>INTERVAL MINUTE (n) TO SECOND (m)|DT_STR|
|INTERVAL SECOND<br>INTERVAL SECOND (n)<br>INTERVAL SECOND (n,m)|DT_STR|
|PERIOD(DATE)|DT_STR|
|PERIOD(TIME)|DT_STR|
|NUMBER|DT_STR|
|CHARACTER|DT_STR|
|VARCHAR|DT_STR (DT_WSTR para conjunto de caracteres Unicode)<br>**Observações**:<br> O comprimento máximo de VARCHAR compatível é de 32.000. <br> O comprimento máximo permitido de DT_STR é de 8.000 caracteres; de DT_WSTR, é de 4.000 caracteres. Os dados serão truncados se excederem.|
|LONG VARCHAR|Sem suporte|
|CLOB|Sem suporte|
|BYTE|DT_BYTES<br>**Observação**: O comprimento máximo permitido é de 8.000 bytes. Os dados serão truncados se excederem.|
|VARBYTE|DT_BYTES<br>**Observação**: O comprimento máximo permitido é de 8.000 bytes. Os dados serão truncados se excederem.|
|BLOB|Sem suporte|

## <a name="next-steps"></a>Próximas etapas

- Configurar o [gerenciador de conexões do Teradata](teradata-connection-manager.md)
- Configurar a [origem do Teradata](teradata-source.md)
- Configurar o [destino do Teradata](teradata-destination.md)
- Em caso de dúvidas, acesse a [Tech Community](https://aka.ms/AA6iwdw).
