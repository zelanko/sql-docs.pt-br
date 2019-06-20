---
title: Gerar elementos para valores NULL com o parâmetro XSINIL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d056959f5e05d3de79fa81d33331390f4decb49a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205609"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>Gerar elementos para valores NULL com o parâmetro XSINIL
  A diretiva **ELEMENTS** constrói XML no qual cada valor de coluna é mapeado para um elemento no XML. Se o valor da coluna for NULL, nenhum elemento será adicionado. Especificando o parâmetro **XSINIL** opcional na diretiva ELEMENTS é possível solicitar que um elemento também seja criado para o valor NULL. Nesse caso, um elemento que tenha o atributo **xsi:nil** definido como TRUE é retornado para cada valor NULL da coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Usar modo RAW com FOR XML](use-raw-mode-with-for-xml.md)  
  
  
