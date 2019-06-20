---
title: Recebendo resultados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: edd070cc6f10829b597534d024d767de2a0c7e12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701714"
---
# <a name="receiving-results"></a>Receber resultados
No ADO a maioria dos comandos resultar em algumas informações retornadas ao chamador. Para retornar o conjunto de linhas de comandos, os resultados são recebidos em uma **Recordset** objeto, que é provavelmente o mais usado os objetos do ADO.  
  
 Há várias maneiras para receber dados em um **Recordset** objeto a partir de uma fonte de dados, incluindo a seguinte chamada:  
  
-   [Método Connection.Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Método Command.Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Método Recordset.Open](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 Receber dados em um **conjunto de registros** objeto conclui o processo de obtenção de dados, com a participação de uma **Conexão** objeto e uma **comando** objeto implicitamente ou explicitamente. Em um sistema de aplicativos de cliente/servidor típico todo o processo de obtenção de dados requer uma viagem de ida e volta pela rede para cada preenchido **conjunto de registros**.  
  
 Para receber mais de um conjuntos de resultados significa que você precisaria fazer várias idas e vindas na rede, um para cada conjunto de dados encapsulado em uma **Recordset** objeto. Para redes lentas ou congestionadas, reduzindo o número de viagens de ida e pode ajudar a melhorar o desempenho do aplicativo. Portanto, alguns provedores oferecem suporte para receber vários **Recordset**s em uma única viagem de ida. Isso é discutido no tópico a seguir:  
  
-   [Recebendo vários conjuntos de registros](../../../ado/guide/data/receiving-multiple-recordsets.md)
