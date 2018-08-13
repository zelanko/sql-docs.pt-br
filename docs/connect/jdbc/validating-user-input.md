---
title: Validação de entrada do usuário | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2320ed83c095d460aa233ac0227f37c15eca88b
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662308"
---
# <a name="validating-user-input"></a>Validando entradas de usuário

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando você construir um aplicativo que acessa dados, deverá presumir que toda a entrada do usuário é mal-intencionada até que se prove o contrário. Se você não fizer isso, deixará o aplicativo vulnerável a ataques. Um tipo de ataque que pode ocorrer é chamado injeção de SQL, em que código mal-intencionado é acrescentado a cadeias de caracteres posteriormente passadas a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a ser analisada e executada. Para evitar este tipo de ataque, use procedimentos armazenados com parâmetros onde for possível e sempre valide a entrada do usuário.

Validar a entrada do usuário no código do cliente é importante para que você não desperdice viagens de ida e volta ao servidor. É igualmente importante validar parâmetros para procedimentos armazenados no servidor a fim de capturar entrada que não é válida e que ignora a validação do lado do cliente.

Para obter mais informações sobre injeção de SQL e como evitá-la, veja "Injeção de SQL" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações sobre como validar parâmetros de procedimento armazenado, consulte "Procedimentos armazenados ([!INCLUDE[ssDE](../../includes/ssde_md.md)])" e tópicos subordinados nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].

## <a name="see-also"></a>Consulte Também

[Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)
