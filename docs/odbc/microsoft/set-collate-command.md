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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997746"
---
# <a name="set-collate-command"></a>Comando SET COLLATE
Especifica uma sequência de agrupamento para campos de caracteres em operações subsequentes de indexação e classificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>Argumentos  
 *cSequenceName*  
 Especifica uma sequência de agrupamento. As opções de sequência de agrupamento disponíveis são descritas na tabela a seguir.  
  
|Opções|Linguagem|  
|-------------|--------------|  
|Holandês|Holandês|  
|GENERAL|Inglês, francês, alemão, espanhol moderno, Português e outros idiomas da Europa Ocidental|  
|Alemão|Pedido de catálogo telefônico alemão (DIN)|  
|Islândia|Islandês|  
|Tradução|Computador (a sequência de agrupamento padrão para versões anteriores do FoxPro)|  
|NORDAN|Norueguês, dinamarquês|  
|Espanhol|Espanhol tradicional|  
|SWEFIN|Sueco, finlandês|  
|UNIQWT|Peso exclusivo|  
  
> [!NOTE]  
>  Quando você especifica a opção espanhol, *ch* é uma única letra que classifica entre *c* e *d*e *ll* classifica entre *l* e *m*.  
  
 Se você especificar uma opção de sequência de agrupamento como uma cadeia de caracteres literal, certifique-se de colocar a opção entre aspas:  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 O computador é a opção de sequência de agrupamento padrão e é a seqüência Xbase que os usuários estão familiarizados. Os caracteres são ordenados conforme aparecem na página de código atual.  
  
 O geral pode ser preferível para usuários dos EUA e da Europa Ocidental. Os caracteres são ordenados conforme aparecem na página de código atual. Em versões do FoxPro anteriores a 2,5, os índices podem ter sido criados usando as funções **Upper**() ou **Lower**() para converter campos de caractere em um caso consistente. Em versões do FoxPro posteriores a 2,5, você pode especificar a opção de sequência de agrupamento geral e omitir a conversão **Upper**().  
  
 Se você especificar uma opção de sequência de agrupamento diferente de MACHINE e se você criar um arquivo. idx, um Compact. idx será sempre criado.  
  
 Use SET ("COLLATE") para retornar a sequência de agrupamento atual.  
  
 Você pode especificar uma sequência de agrupamento para uma fonte de dados usando a [caixa de diálogo configuração do ODBC do Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) ou usando a palavra-chave COLLATE em sua cadeia de conexão com [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md). Isso é idêntico a emitir o seguinte comando:  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>Comentários  
 DEFINIR agrupamento permite que você ordene tabelas que contêm caracteres acentuados para qualquer um dos idiomas com suporte. Alterar a configuração de SET COLLATE não afeta a sequência de agrupamento de índices abertos anteriormente. O Visual FoxPro mantém automaticamente os índices existentes, fornecendo a flexibilidade para criar vários tipos diferentes de índices, mesmo para o mesmo campo.  
  
 Por exemplo, se um índice for criado com SET COLLATE definido como geral e a configuração definir agrupamento for alterada posteriormente para espanhol, o índice manterá a sequência de agrupamento geral.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo da instalação do Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
