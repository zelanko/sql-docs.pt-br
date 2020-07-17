---
title: Permitir opção de configuração de exportação do PolyBase | Microsoft Docs
description: Definir as opção de configuração de `allow polybase export` nas configurações do SQL Server
ms.custom: ''
ms.date: 07/10/2020
ms.prod: sql
ms.prod_service: ''
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c25a7e42b55561ed6337281497e847999d722292
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279642"
---
# <a name="set-allow-polybase-export-configuration-option"></a>Definir as opção de configuração de `allow polybase export`

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

A opção de configuração do servidor `allow polybase export` permite `INSERT` em uma tabela externa do Hadoop. 

Este recurso não oferece suporte à inserção em outras fontes de dados externas.

 Os possíveis valores são descritos na tabela seguinte: 

| Valor | Significado                                |
|-------|----------------------------------------|
| 0     | Desabilitado. Essa é a configuração padrão. |
| 1     | habilitado                                |


A configuração entra em vigor imediatamente.

## <a name="example"></a>Exemplo

O exemplo a seguir habilita essa configuração.

```sql
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
sp_configure 'allow polybase export', 0;
GO
RECONFIGURE;
GO
```

## <a name="next-steps"></a>Próximas etapas

 [Exportar dados](../../relational-databases/polybase/polybase-configure-hadoop.md#exporting-data)