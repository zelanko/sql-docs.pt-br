---
title: Desconectar e reconectar o conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8a3f26ec756ac328c7b717f5f25b566d543d0ff
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>Desconectar e reconectar o conjunto de registros
Um dos recursos mais avançados encontrados no ADO é a capacidade de abrir um conjunto de registros do lado do cliente de uma fonte de dados e, em seguida, desconecte o conjunto de registros da fonte de dados. Depois que o conjunto de registros foi desconectado, a conexão à fonte de dados pode ser fechado, assim, liberar os recursos no servidor usado para mantê-lo. Você pode continuar exibir e editar os dados no conjunto de registros enquanto ela está desconectada e posteriormente se reconectar à fonte de dados e envie suas atualizações no modo de lote.  
  
 Para desconectar um conjunto de registros, abra-o com um local de cursor do adUseClient e, em seguida, defina a propriedade de ActiveConnection igual a nada. (C++ os usuários devem definir o ActiveConnection igual a NULL para desconectar.)  
  
 Usaremos um conjunto de registros desconectado posteriormente nesta seção quando discutiremos persistência de conjunto de registros para um cenário em que é preciso ter os dados em um conjunto de registros disponível para um aplicativo, enquanto o computador cliente não está conectado a uma rede de endereço.  
  
## <a name="see-also"></a>Consulte também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)
