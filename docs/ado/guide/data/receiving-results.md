---
title: Receber resultados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3330d2989f5662693ff7aca720d2bf6e07e16e33
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="receiving-results"></a>Receber resultados
No ADO a maioria dos comandos resultar em algumas informações retornadas ao chamador. Para retornar o conjunto de linhas de comandos, os resultados são recebidos em uma **registros** objeto, que é provavelmente os objetos ADO mais usados.  
  
 Há várias maneiras para receber dados em um **registros** objeto de fonte de dados, incluindo a seguinte chamada:  
  
-   [Método Connection.Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Método Command.Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Método Recordset.Open](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 Recebendo dados em um **registros** objeto conclui o processo de obtenção de dados, com a participação de um **Conexão** objeto e um **comando** objeto, implicitamente ou explicitamente. Em um sistema de aplicativo típico de cliente/servidor, todo o processo de obtenção de dados requer uma viagem de ida e pela rede para cada preenchido **registros**.  
  
 Para receber a mais de um conjuntos de resultados significa que você precisa fazer várias processamentos pela rede, uma para cada conjunto de dados encapsulado em uma **registros** objeto. Para redes lentas ou congestionadas, reduzindo o número de viagens de ida e pode ajudar a melhorar o desempenho do aplicativo. Portanto, alguns provedores oferecem suporte para receber vários **registros**s em uma única viagem de ida. Isso é discutido no tópico a seguir:  
  
-   [Recebendo vários conjuntos de registros](../../../ado/guide/data/receiving-multiple-recordsets.md)
