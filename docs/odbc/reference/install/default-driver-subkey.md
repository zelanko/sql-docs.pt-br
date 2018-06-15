---
title: Padrão de Driver subchave | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default subkey [ODBC]
- registry entries for components [ODBC], default subkey
- subkeys [ODBC], default subkey
- drivers subkey [ODBC]
ms.assetid: 9e58b24f-ebfc-4286-a272-0843b4d6f2d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6563627087ce8516f74f478b35f0f6a896aa025b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915731"
---
# <a name="default-driver-subkey"></a>Subchave do Driver de padrão
A subchave padrão contém um único valor que descreve o driver usado pela fonte de dados padrão. O formato desse valor é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|**Driver**|REG_SZ|*Descrição do driver de padrão*|  
  
 O *descrição do driver de padrão* nome é o mesmo que o nome do valor na subchave Drivers ODBC que descreve o driver.  
  
 Por exemplo, se a fonte de dados padrão usa o driver do SQL Server, o valor na subchave padrão pode ser:  
  
```  
Driver : REG_SZ : SQL Server  
```  
  
> [!NOTE]  
>  O driver padrão contido na subchave padrão pode se referir a um DSN de usuário padrão ou um DSN de sistema padrão. Se um DSN de usuário padrão e um sistema padrão DSN tiver sido criado, o driver padrão é determinado pelo DSN que foi criado por último, por isso não é uma entrada válida para o DSN que foi criado pela primeira vez.
