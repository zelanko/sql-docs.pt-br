---
description: Descritores
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
ms.openlocfilehash: ae01f093ef1b67f1326f8aa7719b74100fcba462
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429328"
---
# <a name="descriptors"></a>Descritores
Um identificador de descritor refere-se a uma estrutura de dados que contém informações sobre colunas ou parâmetros dinâmicos.  
  
 Funções ODBC que operam em dados de parâmetros e de coluna implicitamente definem e recuperam campos de descritor. Por exemplo, quando **SQLBindCol** é chamado para associar dados de coluna, ele define os campos de descritor que descrevem completamente a associação. Quando **SQLColAttribute** é chamado para descrever os dados da coluna, ele retorna os dados armazenados nos campos do descritor.  
  
 Um aplicativo que chama funções ODBC não precisa se preocupar com descritores. Nenhuma operação de banco de dados requer que o aplicativo tenha acesso direto aos descritores. No entanto, para alguns aplicativos, obter acesso direto aos descritores simplifica muitas operações. Por exemplo, o acesso direto aos descritores fornece uma maneira de reassociar dados de coluna, o que pode ser mais eficiente do que chamar **SQLBindCol** novamente.  
  
> [!NOTE]  
>  A representação física do descritor não está definida. Os aplicativos recebem acesso direto a um descritor apenas manipulando seus campos chamando funções ODBC com o identificador do descritor.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tipos de descritores](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [Campos de descritor](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [Alocar e liberar descritores](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [Obter e configurar campos de descritor](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
