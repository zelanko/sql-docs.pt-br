---
title: Tipos definidos pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3873e2d05eab1fb7ce0ec26db73a78ce1c39b28e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="user-defined-types"></a>Tipos definidos pelo usuário
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Tipos definidos pelo usuário (UDTs) foram introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] para permitir que os desenvolvedores estender o sistema de tipo escalar do servidor armazenando objetos do common language runtime (CLR) em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. Os UDTs podem conter vários elementos e pode ter comportamentos, diferentemente dos tipos de dados de alias tradicionais, que consistem em um único [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de dados do sistema. Os UDTs eram anteriormente restritas a um tamanho máximo de 8 kilobytes. Em [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)], foi adicionado suporte para UDTs maiores que 64 kilobytes. A partir da versão 3.0, o JDBC Driver também oferece suporte a UDTs com mais de 64 kilobytes quando você especifica o formato UserDefined.  
  
 Não há alteração de comportamento para UDTs inferiores ou iguais a 8.000 bytes, mas são suportados UDTs maiores que informam seu tamanho como "ilimitado".  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
