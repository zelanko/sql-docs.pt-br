---
title: Manipulando erros no Visual C++ | Microsoft Docs
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
ms.openlocfilehash: fb9eb29a78c3ec5f47e3ff09641ba04ca01d204a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925125"
---
# <a name="handling-errors-in-visual-c"></a>Tratamento de erro em Visual C++
No COM, a maioria das operações retorna um código de retorno HRESULT que indica se uma função foi concluída com êxito. A diretiva #import gera código wrapper em cada método "RAW" ou propriedade e verifica o HRESULT retornado. Se o HRESULT indicar falha, o código do wrapper lançará um erro COM chamando _com_issue_errorex () com o código de retorno HRESULT como um argumento. Objetos de erro COM podem ser capturados em um bloco **try-catch** . (Para fins de eficiência, pegue uma referência a um objeto _com_error.)  
  
 Lembre-se de que são erros do ADO: eles resultam da falha da operação do ADO. Os erros retornados pelo provedor subjacente aparecem como objetos de **erro** na coleção de **erros** do objeto de **conexão** .  
  
 A diretiva #import cria apenas rotinas de tratamento de erros para métodos e propriedades declarados no ADO. dll. No entanto, você pode aproveitar esse mesmo mecanismo de tratamento de erros escrevendo sua própria macro de verificação de erros ou função embutida. Consulte o tópico Visual C++® Extensions para obter exemplos.
