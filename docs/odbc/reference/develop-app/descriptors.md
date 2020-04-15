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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca8299daae744fb9398ed6ffc99c838ce8edff48
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305897"
---
# <a name="descriptors"></a>Descritores
Uma alça de descritor refere-se a uma estrutura de dados que contém informações sobre colunas ou parâmetros dinâmicos.  
  
 Funções ODBC que operam em dados de coluna e parâmetro satisfaz e recuperam implicitamente campos descritores. Por exemplo, quando **o SQLBindCol** é chamado para vincular dados de coluna, ele define campos descritores que descrevem completamente a vinculação. Quando **o SQLColAttribute** é chamado para descrever dados da coluna, ele retorna dados armazenados em campos descritores.  
  
 Um aplicativo chamado funções ODBC não precisa se preocupar com descritores. Nenhuma operação de banco de dados requer que o aplicativo obtenha acesso direto aos descritores. No entanto, para alguns aplicativos, obter acesso direto a descritores agiliza muitas operações. Por exemplo, o acesso direto a descritores fornece uma maneira de revincular dados de coluna, o que pode ser mais eficiente do que chamar **o SQLBindCol** novamente.  
  
> [!NOTE]  
>  A representação física do descritor não está definida. Os aplicativos ganham acesso direto a um descritor apenas manipulando seus campos, chamando funções ODBC com a alça do descritor.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de descritores](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [Campos de descritor](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [Alocar e liberar descritores](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [Obter e configurar campos de descritor](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
