---
title: CONJUNTO COLLATE comando | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- set collate command [ODBC]
ms.assetid: 00efbcd4-fea8-4061-86a5-82de413cb753
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dfd2225157c048840cd20bd140ed74ae31384b8a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="set-collate-command"></a>Comando do conjunto COLLATE
Especifica uma sequência de agrupamento para campos de caractere em operações de classificação e indexação subsequentes.  
  
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
|ALEMÃO|Ordem de alemão telefônico (DIN)|  
|ISLÂNDIA|Islandês|  
|MÁQUINA|Computador (o agrupamento padrão para versões anteriores do FoxPro)|  
|NORDAN|Norueguês, dinamarquês|  
|ESPANHOL|Espanhol tradicional|  
|SWEFIN|Sueco, finlandês|  
|UNIQWT|Peso exclusivo|  
  
> [!NOTE]  
>  Quando você especificar a opção espanhol, *ch* é uma única letra que classifica entre *c* e *d*, e *ll* classifica entre * l* e *m*.  
  
 Se você especificar uma opção de sequência de agrupamento como uma cadeia de caracteres literal, certifique-se de incluir a opção entre aspas:  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MÁQUINA é a opção de sequência de agrupamento padrão e é que os sequência Xbase usuários estão familiarizados com. Caracteres são ordenados que aparecem na página de código atual.  
  
 GERAL pode ser preferível para usuários dos EUA e Europa Ocidental. Caracteres são ordenados que aparecem na página de código atual. Em versões do FoxPro anteriores a 2.5, os índices podem ter sido criados usando o **superior**() ou **inferior**funções () para converter os campos de caractere em um caso consistente. Em versões posteriores a 2.5 no FoxPro, em vez disso, você pode especificar a opção de sequência de agrupamento geral e omitir o **superior**conversão ().  
  
 Se você especificar uma opção de sequência de agrupamento que não seja o computador e se você criar um arquivo. idx, sempre é criado um. idx compact.  
  
 Use SET("COLLATE") para retornar a sequência de agrupamento atual.  
  
 Você pode especificar uma sequência de agrupamento para uma fonte de dados usando o [caixa de diálogo de instalação do Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) ou usando a palavra-chave Collate em sua cadeia de conexão com [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md). Isso é idêntico ao emitir o seguinte comando:  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>Comentários  
 Definir COLLATE permite às tabelas de ordem que contém os caracteres acentuados para qualquer um dos idiomas com suporte. Alterando a configuração de AGRUPAMENTO de conjunto não afeta a sequência de agrupamento de índices abertos anteriormente. Do Visual FoxPro mantém automaticamente os índices existentes, fornece a flexibilidade para criar vários tipos diferentes de índices, mesmo para o mesmo campo.  
  
 Por exemplo, se um índice é criado com definir AGRUPAMENTO definido como geral e a configuração de AGRUPAMENTO definido for alterada posteriormente para espanhol, o índice retém a sequência de agrupamento geral.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo da instalação do Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)

