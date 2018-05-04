---
title: Validando a entrada do usuário | Microsoft Docs
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
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bda7891ae7ec7c64053e0c586a05e54b4cc4634
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="validating-user-input"></a>Validando entradas de usuário
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando você construir um aplicativo que acessa dados, deverá presumir que toda a entrada do usuário é mal-intencionada até que se prove o contrário. Se você não fizer isso, deixará o aplicativo vulnerável a ataques. Um tipo de ataque que pode ocorrer é chamado injeção de SQL, onde código mal-intencionado é acrescentado a cadeias de caracteres que são passadas posteriormente a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para ser analisado e executado. Para evitar este tipo de ataque, use procedimentos armazenados com parâmetros onde for possível e sempre valide a entrada do usuário.  
  
 Validar a entrada do usuário no código do cliente é importante para que você não desperdice viagens de ida e volta ao servidor. É igualmente importante validar parâmetros para procedimentos armazenados no servidor a fim de capturar entrada que não é válida e que ignora a validação do lado do cliente.  
  
 Para obter mais informações sobre injeção de SQL e como evitá-la, consulte "Injeção de SQL" no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online. Para obter mais informações sobre como validar parâmetros de procedimento armazenado, consulte "procedimentos armazenados ([!INCLUDE[ssDE](../../includes/ssde_md.md)])" e tópicos subordinados nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="see-also"></a>Consulte também  
 [Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
