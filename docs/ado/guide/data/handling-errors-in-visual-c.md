---
title: Tratamento de erros no Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e33d28201e1a2e4f7df8ac330ac89b3f00194b14
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161625"
---
# <a name="handling-errors-in-visual-c"></a>Tratamento de erro em Visual C++
No COM, a maioria das operações retornam um código de retorno de HRESULT que indica se uma função foi concluída com êxito. A diretiva #import gera o código de wrapper em torno de cada propriedade ou método "bruto" e verifica o HRESULT retornado. Se o HRESULT indica falha, o código de wrapper gerará um erro de COM por chamada _com_issue_errorex() com o código de retorno de HRESULT como um argumento. Objetos de erro de COM podem ser capturados em uma **try-catch** bloco. (Por questões de eficiência, capture uma referência a um objeto com_error).  
  
 Lembre-se de que esses são erros ADO: eles resultam de falha de operação do ADO. Erros retornados pelo provedor subjacente aparecem como **erro** objetos na **Conexão** do objeto **erros** coleção.  
  
 A diretiva #import cria apenas as rotinas de tratamento de erros para métodos e propriedades declaradas no arquivo. dll ADO. No entanto, você pode aproveitar o mesmo mecanismo de tratamento de erros ao escrever sua própria verificação de erro macro ou uma função in-line. Consulte o tópico de extensões do Visual C++® para obter exemplos.
