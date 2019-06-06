---
title: Extensões do Visual C++ para ADO | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: ccd783bdb7bf266bfdc83c3a02520345d707ceea
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702626"
---
# <a name="visual-c-extensions-for-ado"></a>Extensões do Visual C++ para ADO
O método preferencial de programação ADO com o Visual C++ está usando o **#import** diretiva, conforme discutido na [programação do Microsoft Visual C++ ADO](../../../ado/guide/appendixes/visual-c-ado-programming.md). No entanto, as versões anteriores do ADO enviado com um método alternativo de programação usando o Visual C++: as extensões do Visual C++. Esta seção documenta a esse recurso para aqueles que deve manter o código de extensões do Visual C++, mas o novo código ADO deve ser escrito usando #**importação**.

 Um dos mais tediosa trabalhos Visual C++ programadores enfrentados durante a recuperação de dados com o ADO é conversão de dados retornados como um tipo de dados VARIANT em um tipo de dados do C++ e, em seguida, armazenar os dados convertidos em uma classe ou estrutura. Além de ser complicado, recuperar dados de C++ por meio de um tipo de dados VARIANTE afeta o desempenho.

 ADO fornece uma interface que oferece suporte à recuperação de dados em tipos de dados de C/C++ nativos sem passar por uma VARIANTE e também fornece as macros de pré-processador que simplificam o uso da interface. O resultado é uma ferramenta flexível que é mais fácil de usar e tem um desempenho ótimo.

 Um cenário comum de cliente do C/C++ é associar a um registro em uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para uma classe que contém os tipos do C/C++ nativos ou um struct do C/C++. Ao executar variantes, isso envolve escrever o código de conversão de VARIANTE em tipos nativos do C/C++. As extensões do Visual C++ para ADO são destinadas a tornar esse cenário muito mais fácil para o programador de Visual C++.

 Consulte os tópicos a seguir para saber mais sobre as extensões do Visual C++ para ADO.

-   [Usando extensões do Visual C++ para ADO](../../../ado/guide/appendixes/using-visual-c-extensions.md)

-   [Cabeçalho de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)

-   [O ADO com o exemplo de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md)

## <a name="see-also"></a>Consulte também
 [ADO para índice de sintaxe do Visual C++ para COM](../../../ado/reference/ado-api/ado-for-visual-c-syntax-index-for-com.md) [exemplo de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) [usando as extensões do Visual C++](../../../ado/guide/appendixes/using-visual-c-extensions.md) [cabeçalho de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)
