---
title: Mensagens de diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic messages messages
- error messages [ODBC], diagnostic messages
- diagnostic messages [ODBC]
ms.assetid: 98027871-9901-476e-a722-ee58b7723c1f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 39ebda5de5820cdfd7333ad1d0997593922e0a4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039896"
---
# <a name="diagnostic-messages"></a>Mensagens de diagnóstico
Uma mensagem de diagnóstico é retornada com cada SQLSTATE. O mesmo SQLSTATE é geralmente retornado com um número de mensagens diferentes. Por exemplo, o SQLSTATE 42000 (erro de sintaxe ou violação de acesso) é retornado para a maioria dos erros na sintaxe SQL. No entanto, cada erro de sintaxe provavelmente será descrito por uma mensagem diferente.  
  
 As mensagens de diagnóstico de exemplo são listadas na coluna erro na tabela de hiperestados no apêndice A e em cada função. Embora os drivers possam retornar essas mensagens, é mais provável que eles retornem qualquer mensagem passada para eles pela fonte de dados.  
  
 Os aplicativos geralmente exibem mensagens de diagnóstico para o usuário, juntamente com o SQLSTATE e o código de erro nativo. Isso ajuda o usuário e a equipe de suporte a determinar a causa de quaisquer problemas. As informações de componente inseridas na mensagem são particularmente úteis para fazer isso.  
  
 As mensagens de diagnóstico são provenientes de fontes de dados e componentes em uma conexão ODBC, como drivers, gateways e o Gerenciador de driver. Normalmente, as fontes de dados não dão suporte diretamente a ODBC. Consequentemente, se um componente em uma conexão ODBC receber uma mensagem de uma fonte de dados, ele deverá identificar a fonte de dados como a origem da mensagem. Ele também deve se identificar como o componente que recebeu a mensagem.  
  
 Se a origem de um erro ou aviso for um componente em si, a mensagem de diagnóstico deverá explicar isso. Portanto, o texto das mensagens tem dois formatos diferentes. Para erros e avisos que não ocorrem em uma fonte de dados, a mensagem de diagnóstico deve usar este formato:  
  
 **[** *fornecedor-identificador* **] [** *ODBC-componente-identificador* **]** *texto fornecido pelo componente*  
  
 Para erros e avisos que ocorrem em uma fonte de dados, a mensagem de diagnóstico deve usar este formato:  
  
 **[** *fornecedor-identificador* **] [** *ODBC-componente-identificador* **] [** *Data-fonte-identificador* **]** *dados-fonte-fornecido-texto*  
  
 A tabela a seguir mostra o significado de cada elemento.  
  
|Elemento|Significado|  
|-------------|-------------|  
|*identificador de fornecedor*|Identifica o fornecedor do componente no qual ocorreu o erro ou o aviso ou que recebeu o erro ou aviso diretamente da fonte de dados.|  
|*ODBC-identificador de componente*|Identifica o componente no qual ocorreu o erro ou o aviso ou que recebeu o erro ou aviso diretamente da fonte de dados.|  
|*identificador de fonte de dados*|Identifica a fonte de dados. Para drivers baseados em arquivo, normalmente é um formato de arquivo, como Xbase [1] para drivers baseados em DBMS, este é o produto DBMS.|  
|*texto fornecido pelo componente*|Gerado pelo componente ODBC.|  
|*fonte de dados-fornecida-texto*|Gerado pela fonte de dados.|  
  
 [1] nesse caso, o driver está agindo como o driver e a fonte de dados.  
  
 Os colchetes (**[]**) devem ser incluídos na mensagem e não indicam itens opcionais.
