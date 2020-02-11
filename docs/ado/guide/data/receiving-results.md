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
ms.openlocfilehash: 2b861553e9a71ce56377f8d87bba0f9e26e929c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924520"
---
# <a name="receiving-results"></a>Receber resultados
No ADO, a maioria dos comandos resulta em algumas informações retornadas ao chamador. Para comandos que retornam o conjunto de linhas, os resultados são recebidos em um objeto **Recordset** , que provavelmente é o mais usado dos objetos ADO.  
  
 Há várias maneiras de receber dados em um objeto **Recordset** de uma fonte de dados, incluindo a chamada do seguinte:  
  
-   [Método Connection. Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Método Command. Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Método Recordset. Open](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection. NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection. StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 O recebimento de dados em um objeto de **conjunto de registros** conclui o processo de obtenção de dados, com a participação de um objeto de **conexão** e um objeto de **comando** , implicitamente ou explicitamente. Em um sistema de aplicativos cliente/servidor típico, todo o processo de obtenção de dados requer uma viagem de ida e volta pela rede para cada **conjunto de registros**preenchido.  
  
 Para receber mais de um conjunto de resultados significa que você precisaria fazer várias viagens de ida e volta pela rede, uma para cada conjunto de dados encapsulado em um objeto **Recordset** . Para redes lentas ou congestionadas, reduzir o número de viagens de ida e volta pode ajudar a melhorar o desempenho do aplicativo. Portanto, alguns provedores oferecem suporte para receber vários **conjuntos de registros**s em uma única viagem de ida e volta. Isso é discutido no seguinte tópico:  
  
-   [Receber vários conjuntos de registros](../../../ado/guide/data/receiving-multiple-recordsets.md)
