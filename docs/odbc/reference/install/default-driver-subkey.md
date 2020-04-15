---
title: Subchave padrão do driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb134d670964e352d94c13474d8a72fa4bd494ba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301049"
---
# <a name="default-driver-subkey"></a>Subchave do driver padrão
A sub-tecla Default contém um único valor que descreve o driver usado pela fonte de dados padrão. O formato deste valor é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|**Driver**|REG_SZ|*padrão-driver-descrição*|  
  
 O nome *padrão-driver-descrição* é o mesmo que o nome do valor sob a sub-chave Drivers ODBC que descreve o driver.  
  
 Por exemplo, se a fonte de dados padrão usar o driver sql server, o valor sob a sub-chave Padrão pode ser:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  O driver padrão contido na subchave Padrão pode se referir a um DSN de usuário padrão ou a um DSN do sistema padrão. Se um DSN de usuário padrão e um DSN padrão tiverem sido criados, o driver padrão será determinado pelo DSN que foi criado por último, então pode não ser uma entrada válida para o DSN que foi criado primeiro.
