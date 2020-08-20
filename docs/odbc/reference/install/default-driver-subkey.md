---
description: Subchave do driver padrão
title: Subchave do driver padrão | Microsoft Docs
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
ms.openlocfilehash: d78cc54253d002c54510fdc47f46f10de9281b65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494549"
---
# <a name="default-driver-subkey"></a>Subchave do driver padrão
A subchave padrão contém um único valor que descreve o driver usado pela fonte de dados padrão. O formato desse valor é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|**Driver**|REG_SZ|*Descrição do driver-padrão*|  
  
 O nome de *Descrição de driver-padrão* é o mesmo que o nome do valor na subchave drivers ODBC que descreve o driver.  
  
 Por exemplo, se a fonte de dados padrão usar o driver SQL Server, o valor na subchave padrão poderá ser:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  O driver padrão contido na subchave padrão pode se referir a um DSN de usuário padrão ou a um DSN de sistema padrão. Se um DSN de usuário padrão e um DSN de sistema padrão tiverem sido criados, o driver padrão será determinado pelo DSN que foi criado por último, portanto, pode não ser uma entrada válida para o DSN que foi criado primeiro.
