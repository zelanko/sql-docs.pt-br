---
description: Receber resultados
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3317441322d0f1be94ee1c897946d83f6291143c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452988"
---
# <a name="receiving-results"></a>Receber resultados
No ADO, a maioria dos comandos resulta em algumas informações retornadas ao chamador. Para comandos que retornam o conjunto de linhas, os resultados são recebidos em um objeto **Recordset** , que provavelmente é o mais usado dos objetos ADO.  
  
 Há várias maneiras de receber dados em um objeto **Recordset** de uma fonte de dados, incluindo a chamada do seguinte:  
  
-   [Connection.Exemétodo graciosos](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command.Exemétodo graciosos](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Método Recordset. Open](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection. NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection. StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 O recebimento de dados em um objeto de **conjunto de registros** conclui o processo de obtenção de dados, com a participação de um objeto de **conexão** e um objeto de **comando** , implicitamente ou explicitamente. Em um sistema de aplicativos cliente/servidor típico, todo o processo de obtenção de dados requer uma viagem de ida e volta pela rede para cada **conjunto de registros**preenchido.  
  
 Para receber mais de um conjunto de resultados significa que você precisaria fazer várias viagens de ida e volta pela rede, uma para cada conjunto de dados encapsulado em um objeto **Recordset** . Para redes lentas ou congestionadas, reduzir o número de viagens de ida e volta pode ajudar a melhorar o desempenho do aplicativo. Portanto, alguns provedores oferecem suporte para receber vários **conjuntos de registros**s em uma única viagem de ida e volta. Isso é discutido no seguinte tópico:  
  
-   [Receber vários conjuntos de registros](../../../ado/guide/data/receiving-multiple-recordsets.md)
