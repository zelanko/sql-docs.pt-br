---
title: "Tipos definidos pelo usuário | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed2b0bb8227a1b430bcd30b1d41460862c8db325
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="user-defined-types"></a>Tipos definidos pelo usuário
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Tipos definidos pelo usuário (UDTs) foram introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] para permitir que os desenvolvedores estender o sistema de tipo escalar do servidor armazenando objetos do common language runtime (CLR) em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. Os UDTs podem conter vários elementos e pode ter comportamentos, diferentemente dos tipos de dados de alias tradicionais, que consistem em um único [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados do sistema. Os UDTs eram anteriormente restritas a um tamanho máximo de 8 kilobytes. Em [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)], foi adicionado suporte para UDTs maiores que 64 kilobytes. A partir da versão 3.0, o JDBC Driver também oferece suporte a UDTs com mais de 64 kilobytes quando você especifica o formato UserDefined.  
  
 Não há alteração de comportamento para UDTs inferiores ou iguais a 8.000 bytes, mas são suportados UDTs maiores que informam seu tamanho como "ilimitado".  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

