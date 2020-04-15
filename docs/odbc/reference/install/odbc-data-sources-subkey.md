---
title: Subchave de fontes de dados oDBC | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c5e97e643a78187b15e91833c832cd16ca435c7f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304048"
---
# <a name="odbc-data-sources-subkey"></a>Subchave de fontes de dados ODBC

Os valores `ODBC Data Sources` abaixo da sub-chave listam as fontes de dados. O formato desses valores é mostrado na tabela a seguir.

| Nome | Tipo de dados | Dados |
| :--- | :-------- | :--- |
| *nome-fonte de dados* | REG_SZ | *driver-descrição* |
| &nbsp; | &nbsp; | &nbsp; |

O valor *do nome de origem de dados* é definido pelo programa de administração (que geralmente solicita o usuário), e a descrição do *driver* é definida pelo desenvolvedor do driver (geralmente é o nome do DBMS associado ao driver).

Por exemplo, suponha que três fontes de dados tenham sido definidas: Inventário, que usa o SQL Server; Folha de pagamento, que usa dBASE; e Pessoal, que usa arquivos de texto formatados. Os valores `ODBC Data Sources` sob a sub-chave podem ser os seguintes:

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
