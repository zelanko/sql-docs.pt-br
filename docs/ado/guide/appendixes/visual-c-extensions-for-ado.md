---
title: Extensões do Visual C++ para ADO | Microsoft Docs
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
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions for ADO
ms.assetid: 2952ece0-7217-4448-bb09-f6b64f43b7e2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca21e976783a10a738488762e382982e4fd8fd8a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747674"
---
# <a name="visual-c-extensions"></a>Extensões do Visual C++
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
