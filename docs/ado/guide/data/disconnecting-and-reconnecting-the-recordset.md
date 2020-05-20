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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ef30165a05bc472bfe34cec4e7f669d545d7768
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761052"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>Desconectar e reconectar o conjunto de registros
Um dos recursos mais poderosos encontrados no ADO é a capacidade de abrir um conjunto de registros do lado do cliente de uma fonte de dados e, em seguida, desconectar o conjunto de registros da fonte de dados. Depois que o conjunto de registros tiver sido desconectado, a conexão com a fonte de dados poderá ser fechada, liberando assim os recursos no servidor usado para mantê-lo. Você pode continuar a exibir e editar os dados no conjunto de registros enquanto ele estiver desconectado e depois reconectar-se à fonte de dados e enviar suas atualizações no modo de lote.  
  
 Para desconectar um conjunto de registros, abra-o com um local de cursor de adUseClient e, em seguida, defina a propriedade ActiveConnection igual a Nothing. (Os usuários do C++ devem definir o ActiveConnection igual a NULL para desconectar.)  
  
 Usaremos um conjunto de registros desconectado posteriormente nesta seção quando discutimos a persistência do conjunto de registros para tratar de um cenário no qual precisamos ter os dados em um conjunto de registros disponível para um aplicativo enquanto o computador cliente não está conectado a uma rede.  
  
## <a name="see-also"></a>Consulte Também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)
