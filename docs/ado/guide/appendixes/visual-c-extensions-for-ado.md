---
title: Extensões de Visual C++ para ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions for ADO
ms.assetid: 2952ece0-7217-4448-bb09-f6b64f43b7e2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db11e86ab479ad0df4224d59c3408729fa9903ab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926370"
---
# <a name="visual-c-extensions-for-ado"></a>Extensões do Visual C++ para ADO
O método preferencial de programação do ADO com o Visual C++ é usar a diretiva **#import** , conforme discutido em [Microsoft Visual C++ Programação ADO](../../../ado/guide/appendixes/visual-c-ado-programming.md). No entanto, as versões anteriores do ADO vêm com um método alternativo de programação usando Visual C++: as extensões de Visual C++. Esta seção documenta esse recurso para aqueles que devem manter o código de extensões de Visual C++, mas o novo código ADO deve ser escrito usando #**Import**.

 Um dos trabalhos mais entediantes Visual C++ os programadores enfrentam ao recuperar dados com o ADO, convertendo os dados retornados como um tipo de dados VARIANT em um tipo de dados C++ e, em seguida, armazenando os dados convertidos em uma classe ou estrutura. Além de ser complicado, a recuperação de dados do C++ por meio de um tipo de dados VARIANT diminui o desempenho.

 O ADO fornece uma interface que dá suporte à recuperação de dados em tipos de dados C/C++ nativos sem passar por uma variante e também fornece macros de pré-processador que simplificam o uso da interface. O resultado é uma ferramenta flexível que é mais fácil de usar e tem um ótimo desempenho.

 Um cenário de cliente comum do C/C++ é associar um registro em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) a um struct c/c++ ou classe que contenha tipos c/c++ nativos. Ao passar por VARIAntes, isso envolve escrever código de conversão de VARIANT para tipos nativos C/C++. As extensões de Visual C++ para ADO são destinadas a tornar esse cenário muito mais fácil para o programador de Visual C++.

 Consulte os tópicos a seguir para saber mais sobre as extensões de Visual C++ para ADO.

-   [Usando extensões de Visual C++ para ADO](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Cabeçalho de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [Exemplo de extensões ADO with Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>Consulte Também
 [ADO para Visual C++ índice de sintaxe para o exemplo de extensões de](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) [usando Visual C++ Extensions](../../../ado/guide/appendixes/using-visual-c-extensions.md) [Visual C++ cabeçalho de extensões](../../../ado/guide/appendixes/visual-c-extensions-header.md)
