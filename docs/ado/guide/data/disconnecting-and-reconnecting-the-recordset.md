---
title: Desconectando e reconectando o conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a263903ab4f51d583b6533b6802fabd6c888f479
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700791"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>Desconectar e reconectar o conjunto de registros
Um dos recursos mais avançados encontrados no ADO é a capacidade de abrir um conjunto de registros do lado do cliente de uma fonte de dados e, em seguida, desconecte o conjunto de registros da fonte de dados. Depois que o conjunto de registros desconectado, a conexão à fonte de dados pode ser fechado, assim, liberar os recursos no servidor usado para mantê-lo. Você pode continuar a exibir e editar os dados no conjunto de registros enquanto ele estiver desconectado e se reconectar mais tarde para a fonte de dados e enviar suas atualizações no modo de lote.  
  
 Para desconectar um conjunto de registros, abri-lo com o local cursor adUseClient e, em seguida, defina a propriedade ActiveConnection igual a Nothing. (C++ os usuários devem definir o ActiveConnection igual a NULL para desconectar.)  
  
 Usaremos um conjunto de registros desconectado mais tarde nesta seção quando abordarmos a persistência de conjunto de registros para um cenário em que é necessário ter os dados em um conjunto de registros disponível para um aplicativo enquanto o computador cliente não estiver conectado a uma rede de endereço.  
  
## <a name="see-also"></a>Consulte também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)
