---
title: Componentes ODBC afetados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d9155fa1c9df5846f069e93a3db1b969e9219ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306470"
---
# <a name="affected-odbc-components"></a>Componentes ODBC afetados
A compatibilidade retrógrada descreve como aplicativos, o Driver Manager e os drivers são afetados pela introdução de uma nova versão do Driver Manager. Isso afeta aplicativos e driver quando ambos permanecem na versão antiga. Há, portanto, três tipos de retrocompatibilidade a considerar, como mostrado na tabela a seguir.  
  
|Type|Versão do DM|Versão do aplicativo|Versão do driver|  
|----------|-------------------|----------------------------|-----------------------|  
|Compatibilidade retrógrada do driver manager|*3.x*|*2. x*|*2. x*|  
|Retrocompatibilidade do driver[1]|*3.x*|*2. x*|*3.x*|  
|Compatibilidade retroativa do aplicativo|*3.x*|*3.x*|*2. x*|  
  
 [1] A retrocompatibilidade dos drivers é discutida principalmente no Apêndice G: Diretrizes do Driver para Compatibilidade Retrógrada.  
  
> [!NOTE]
>  Um aplicativo compatível com padrões - por exemplo, um aplicativo que tenha sido escrito de acordo com as normas Open Group ou ISO CLI - é garantido para trabalhar com um driver ODBC *3.x* através do ODBC *3.x* Driver Manager. Presume-se que a funcionalidade que o aplicativo está usando está disponível no driver. Também se supõe que o aplicativo compatível com padrões foi compilado com os arquivos de cabeçalho ODBC *3.x.*
