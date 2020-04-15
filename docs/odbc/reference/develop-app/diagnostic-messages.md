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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be63e9d78960e40ac5e9ee016d2cfd868d99a922
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305827"
---
# <a name="diagnostic-messages"></a>Mensagens de diagnóstico
Uma mensagem de diagnóstico é devolvida com cada SQLSTATE. O mesmo SQLSTATE é frequentemente devolvido com uma série de mensagens diferentes. Por exemplo, SQLSTATE 42000 (erro de sintaxe ou violação de acesso) é devolvido para a maioria dos erros na sintaxe SQL. No entanto, é provável que cada erro de sintaxe seja descrito por uma mensagem diferente.  
  
 As mensagens de diagnóstico de amostra são listadas na coluna Erro na tabela de SQLSTATEs no apêndice A e em cada função. Embora os motoristas possam retornar essas mensagens, eles são mais propensos a retornar qualquer mensagem que seja passada a eles pela fonte de dados.  
  
 Os aplicativos geralmente exibem mensagens de diagnóstico para o usuário, juntamente com o SQLSTATE e o código de erro nativo. Isso ajuda o usuário e o pessoal de suporte a determinar a causa de quaisquer problemas. As informações do componente incorporadas na mensagem são particularmente úteis para fazer isso.  
  
 As mensagens de diagnóstico vêm de fontes de dados e componentes em uma conexão ODBC, como drivers, gateways e o Driver Manager. Normalmente, as fontes de dados não suportam diretamente o ODBC. Consequentemente, se um componente em uma conexão ODBC recebe uma mensagem de uma fonte de dados, ele deve identificar a fonte de dados como a fonte da mensagem. Ele também deve identificar-se como o componente que recebeu a mensagem.  
  
 Se a fonte de um erro ou aviso for um componente em si, a mensagem de diagnóstico deve explicar isso. Portanto, o texto das mensagens tem dois formatos diferentes. Para erros e avisos que não ocorrem em uma fonte de dados, a mensagem de diagnóstico deve usar este formato:  
  
 **[** *fornecedor-identificador* **][ODBC-component-identifier]** *ODBC-component-identifier* **]** *componente-fornecido-texto*  
  
 Para erros e avisos que ocorrem em uma fonte de dados, a mensagem de diagnóstico deve usar este formato:  
  
 **[** *identificador de fornecedor* **][** *identificador de componentes ODBC* **][identificador** de origem de **dados]** *data-source-supplied-text* *data-source-identifier*  
  
 A tabela a seguir mostra o significado de cada elemento.  
  
|Elemento|Significado|  
|-------------|-------------|  
|*identificador de fornecedor*|Identifica o fornecedor do componente no qual ocorreu o erro ou aviso ou que recebeu o erro ou aviso diretamente da fonte de dados.|  
|*Identificador de componentes ODBC*|Identifica o componente no qual ocorreu o erro ou aviso ou que recebeu o erro ou aviso diretamente da fonte de dados.|  
|*identificador de origem de dados*|Identifica a fonte de dados. Para drivers baseados em arquivos, este é tipicamente um formato de arquivo, como Xbase[1] Para drivers baseados em DBMS, este é o produto DBMS.|  
|*texto fornecido por componentes*|Gerado pelo componente ODBC.|  
|*data-source-fornecido-texto*|Gerado pela fonte de dados.|  
  
 [1] Neste caso, o motorista está agindo como o motorista e a fonte de dados.  
  
 Os suportes (**[ )** devem ser incluídos na mensagem e não indicam itens opcionais.
