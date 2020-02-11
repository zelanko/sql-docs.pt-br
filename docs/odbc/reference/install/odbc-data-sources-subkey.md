---
title: Subchave de fontes de dados ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d6d54d1fc7c7742bf94e91d7370f356e28b5624
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71207692"
---
# <a name="odbc-data-sources-subkey"></a>Subchave de fontes de dados ODBC

Os valores na `ODBC Data Sources` subchave listam as fontes de dados. O formato desses valores é mostrado na tabela a seguir.

| Nome | Tipo de dados | data |
| :--- | :-------- | :--- |
| *nome da fonte de dados* | REG_SZ | *Descrição do driver* |
| &nbsp; | &nbsp; | &nbsp; |

O valor *Data-Source-Name* é definido pelo programa de administração (que geralmente solicita o usuário) e a *Descrição do driver* é definida pelo desenvolvedor do driver (geralmente é o nome do DBMS associado ao driver).

Por exemplo, suponha que três fontes de dados tenham sido definidas: inventário, que usa SQL Server; Folha de pagamento, que usa o dBASE; e pessoal, que usa arquivos de texto formatados. Os valores na `ODBC Data Sources` subchave podem ser os seguintes:

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
