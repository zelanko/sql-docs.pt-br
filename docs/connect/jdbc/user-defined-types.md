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
ms.topic: article
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd978234ed253fe88dbb8b7aaf9403351caabb8a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="user-defined-types"></a>Tipos definidos pelo usuário
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Os tipos definidos pelo usuário (UDTs) foram introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] para permitir que os desenvolvedores estendessem o sistema de tipo escalar do servidor armazenando objetos de CLR em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Os UDTs podem conter vários elementos e ter comportamentos, diferentemente dos tipos de dados de alias tradicionais, que consistem em um único tipo de dado do sistema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Os UDTs eram anteriormente restritas a um tamanho máximo de 8 kilobytes. No [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)], o suporte foi adicionado a UDTs maiores que 64 kilobytes. A partir da versão 3.0, o JDBC Driver também oferece suporte a UDTs com mais de 64 kilobytes quando você especifica o formato UserDefined.  
  
 Não há alteração de comportamento para UDTs inferiores ou iguais a 8.000 bytes, mas são suportados UDTs maiores que informam seu tamanho como "ilimitado".  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
