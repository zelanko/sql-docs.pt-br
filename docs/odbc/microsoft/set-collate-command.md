---
title: Comando SET COLLATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a7701edd4c1902399f1d040ae9027365bdf04ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997746"
---
# <a name="set-collate-command"></a>Comando SET COLLATE
Especifica uma sequência de agrupamento para campos de caractere em subsequentes de indexação e operações de classificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>Argumentos  
 *cSequenceName*  
 Especifica uma sequência de agrupamento. As opções de sequência de agrupamento disponíveis são descritas na tabela a seguir.  
  
|Opções|Idioma|  
|-------------|--------------|  
|HOLANDÊS|Holandês|  
|GENERAL|Inglês, francês, alemão, espanhol moderno, português e outros idiomas da Europa Ocidental|  
|ALEMÃO|Ordem de catálogo telefônico alemão (DIN)|  
|ISLÂNDIA|Islandês|  
|MÁQUINA|Máquina (a sequência de agrupamento padrão para versões anteriores do FoxPro)|  
|NORDAN|Norueguês, dinamarquês|  
|ESPANHOL|Espanhol tradicional|  
|SWEFIN|Sueco, finlandês|  
|UNIQWT|Peso exclusivo|  
  
> [!NOTE]  
>  Quando você especifica a opção de espanhol *ch* é uma única letra que classifica entre *c* e *1!d*, e *ll* classifica entre  *l* e *m*.  
  
 Se você especificar uma opção de agrupamento de sequência como uma cadeia de caracteres literal, certifique-se de colocar a opção entre aspas:  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MÁQUINA é a opção de sequência de agrupamento padrão e se que os usuários do Xbase sequência estejam familiarizados com. Caracteres são classificadas como aparecem na página de código atual.  
  
 GERAL pode ser preferível para usuários dos EUA e Europa Ocidental. Caracteres são classificadas como aparecem na página de código atual. Nas versões do FoxPro anteriores a 2.5, os índices podem ter sido criados usando o **superior**() ou **inferior**funções () para converter os campos de caractere em um caso consistente. Nas versões do FoxPro posteriores a 2.5, em vez disso, você pode especificar a opção de sequência de agrupamento geral e omitir as **superior**conversão ().  
  
 Se você especificar uma opção de sequência de agrupamento que não seja o computador e se você criar um arquivo. idx, sempre é criado um. idx compact.  
  
 Use SET("COLLATE") para retornar a sequência de agrupamento atual.  
  
 Você pode especificar uma sequência de agrupamento para uma fonte de dados usando o [caixa de diálogo de instalação do Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) ou usando a palavra-chave Collate na sua cadeia de conexão com o [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md). Isso é idêntico ao emitir o seguinte comando:  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>Comentários  
 Definir AGRUPAMENTO permite às tabelas de ordem que contém os caracteres acentuados para qualquer um dos idiomas com suporte. Alterando a configuração de AGRUPAMENTO do conjunto não afeta a sequência de agrupamento de índices abertos anteriormente. Do Visual FoxPro mantém automaticamente os índices existentes, oferecendo a flexibilidade para criar muitos tipos diferentes de índices, mesmo para o mesmo campo.  
  
 Por exemplo, se um índice é criado com o conjunto de AGRUPAMENTO definido como geral e a configuração de AGRUPAMENTO do conjunto for alterada posteriormente para o espanhol, o índice retém a sequência de agrupamento geral.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo da instalação do Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
