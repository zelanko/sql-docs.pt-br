---
title: Tratamento de erros no Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 68ce5fb8cc94b130de5171a45b65743e86eec3da
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271685"
---
# <a name="handling-errors-in-visual-c"></a>Tratamento de erros no Visual C++
Em COM, a maioria das operações retornam um código de retorno de HRESULT que indica se uma função foi concluída com êxito. A diretiva #import gera o código de wrapper em torno de cada propriedade ou método "bruto" e verifica o HRESULT retornado. Se o HRESULT indica falha, o código de wrapper gerará um erro de COM pela chamada _com_issue_errorex() com o código de retorno HRESULT como um argumento. Objetos de erro podem ser capturados em uma **de try-catch** bloco. (Para a mesma da eficiência, capturar uma referência a um objeto com_error).  
  
 Lembre-se de que esses são erros de ADO: eles são provenientes de falha de operação do ADO. Erros retornados pelo provedor subjacente aparecem como **erro** objetos no **Conexão** do objeto **erros** coleção.  
  
 A diretiva #import só cria rotinas de tratamento de erros para os métodos e propriedades declaradas no arquivo. dll ADO. No entanto, você pode aproveitar o mesmo mecanismo de tratamento de erros, escrevendo sua própria verificação de erros de macro ou função embutida. Consulte o tópico de extensões do Visual C++® para obter exemplos.
