---
title: Descritores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d50ce0c2023e187d63d08aa862398d18dc188fd1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62744234"
---
# <a name="descriptors"></a>Descritores
Um identificador do descritor se refere a uma estrutura de dados que contém informações sobre colunas ou parâmetros dinâmicos.  
  
 Funções ODBC que operam em dados de parâmetro e coluna implicitamente definir e recuperar os campos de descritor. Por exemplo, quando **SQLBindCol** é chamado para associar dados da coluna, ele define os campos de descritor que descrevem completamente a associação. Quando **SQLColAttribute** é chamado para descrever dados da coluna, ele retorna os dados armazenados nos campos de descritor.  
  
 Um aplicativo chamando funções ODBC precisa não se preocupar em descritores. Nenhuma operação de banco de dados requer que o aplicativo obtenha acesso direto aos descritores. No entanto, para alguns aplicativos, ganhar acesso direto aos descritores simplifica muitas operações. Por exemplo, direcionar o acesso aos descritores fornece uma maneira de associar novamente os dados da coluna, que podem ser mais eficientes do que chamar **SQLBindCol** novamente.  
  
> [!NOTE]  
>  A representação física do descritor não está definida. Os aplicativos obtêm acesso direto para um descritor de apenas por meio da manipulação seus campos chamando funções ODBC com o identificador do descritor.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tipos de descritores](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [Campos de descritor](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [Alocando e liberando descritores](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [Obtendo e configurando campos de descritor](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
