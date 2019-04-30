---
title: Subchave do Driver padrão | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d78101fd564e18467e6833f480cec2409dc2c44b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198308"
---
# <a name="default-driver-subkey"></a>Subchave do driver padrão
A subchave padrão contém um único valor que descreve o driver usado pela fonte de dados padrão. O formato desse valor é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|**Driver**|REG_SZ|*default-driver-description*|  
  
 O *descrição do driver de padrão* nome é igual ao nome do valor sob a subchave de Drivers ODBC que descreve o driver.  
  
 Por exemplo, se a fonte de dados padrão usa o driver do SQL Server, o valor sob a subchave padrão pode ser:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  O driver padrão contido na subchave padrão pode se referir a um DSN de usuário padrão ou um DSN de sistema padrão. Se um DSN de usuário padrão e um sistema padrão DSN tiver sido criado, o driver padrão é determinado pelo DSN que foi criado pela última vez, portanto, não pode ser uma entrada válida para o DSN que foi criado pela primeira vez.
