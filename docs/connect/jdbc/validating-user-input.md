---
title: Validando entrada do usuário | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8138b5fa17bb3cae6c1bdf079d3c562346156fd8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923922"
---
# <a name="validating-user-input"></a>Validando entrada do usuário

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando você construir um aplicativo que acessa dados, deverá presumir que toda a entrada do usuário é mal-intencionada até que se prove o contrário. Se você não fizer isso, deixará o aplicativo vulnerável a ataques. Um tipo de ataque que pode ocorrer é chamado injeção de SQL, em que código mal-intencionado é acrescentado a cadeias de caracteres posteriormente passadas a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser analisada e executada. Para evitar este tipo de ataque, use procedimentos armazenados com parâmetros onde for possível e sempre valide a entrada do usuário.

Validar a entrada do usuário no código do cliente é importante para que você não desperdice viagens de ida e volta ao servidor. É igualmente importante validar parâmetros para procedimentos armazenados no servidor a fim de capturar entrada que não é válida e que ignora a validação do lado do cliente.

Para obter mais informações sobre injeção de SQL e como evitá-la, veja "Injeção de SQL" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como validar parâmetros de procedimento armazenado, consulte "Procedimentos armazenados ([!INCLUDE[ssDE](../../includes/ssde_md.md)])" e tópicos subordinados nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="see-also"></a>Confira também

[Protegendo aplicativos do JDBC Driver](../../connect/jdbc/securing-jdbc-driver-applications.md)
