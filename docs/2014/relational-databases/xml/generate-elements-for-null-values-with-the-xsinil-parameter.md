---
title: Gerar elementos para valores NULL com o parâmetro XSINIL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 31b2654eeab73a83472da5b06d53557bf265dba6
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43890202"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>Gerar elementos para valores NULL com o parâmetro XSINIL
  A diretiva **ELEMENTS** constrói XML no qual cada valor de coluna é mapeado para um elemento no XML. Se o valor da coluna for NULL, nenhum elemento será adicionado. Especificando o parâmetro **XSINIL** opcional na diretiva ELEMENTS é possível solicitar que um elemento também seja criado para o valor NULL. Nesse caso, um elemento que tenha o atributo **xsi:nil** definido como TRUE é retornado para cada valor NULL da coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Usar modo RAW com FOR XML](use-raw-mode-with-for-xml.md)  
  
  
