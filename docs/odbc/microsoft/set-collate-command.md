---
title: SET COMANDO COLLATE | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a9c1dfd59c00ad0ac0b7bd8b8f1cdfccc84d9b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300886"
---
# <a name="set-collate-command"></a>Comando SET COLLATE
Especifica uma seqüência de colagem para campos de caracteres em operações subseqüentes de indexação e classificação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET COLLATE TO cSequenceName  
```  
  
## <a name="arguments"></a>Argumentos  
 *cNome de seqüência*  
 Especifica uma seqüência de colagem. As opções de seqüência de colagem disponíveis são descritas na tabela a seguir.  
  
|Opções|Linguagem|  
|-------------|--------------|  
|Holandês|Holandês|  
|GENERAL|Inglês, francês, alemão, espanhol moderno, português e outras línguas da Europa Ocidental|  
|Alemão|Pedido de lista telefônica alemã (DIN)|  
|Islândia|Islandês|  
|Máquina|Máquina (a seqüência de colagem padrão para versões anteriores do FoxPro)|  
|NORDAN|Norueguês, dinamarquês|  
|Espanhol|Espanhol tradicional|  
|SWEFIN|Sueco, finlandês|  
|UNIQWT|Peso Único|  
  
> [!NOTE]  
>  Quando você especifica a opção ESPANHOL, *ch* é uma única letra que classifica entre *c* e *d*, e *ll* classifica entre *l* e *m*.  
  
 Se você especificar uma opção de seqüência de colagem como uma seqüência de caracteres literal, certifique-se de colocar a opção entre aspas:  
  
```  
SET COLLATE TO "SWEFIN"  
```  
  
 MACHINE é a opção de seqüência de colagem padrão e é a seqüência com a qual os usuários do Xbase estão familiarizados. Os caracteres são ordenados quando aparecem na página de código atual.  
  
 Geral pode ser preferível para usuários dos EUA e da Europa Ocidental. Os caracteres são ordenados quando aparecem na página de código atual. Nas versões FoxPro anteriores a 2,5, os índices podem ter sido criados usando as funções **UPPER**( ) ou **LOWER**( ) para converter campos de caracteres em um caso consistente. Nas versões FoxPro mais tarde que 2.5, você pode especificar a opção de seqüência de colagem GERAL e omiti-lo na conversão **UPPER**( ).  
  
 Se você especificar uma opção de seqüência de colagem diferente do MACHINE e se você criar um arquivo .idx, um compact .idx será sempre criado.  
  
 Use SET ("COLLATE") para retornar a seqüência de colagem atual.  
  
 Você pode especificar uma seqüência de colisão para uma fonte de dados usando a [caixa de diálogo de configuração Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) ou usando a palavra-chave Collate em sua seqüência de conexão com [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md). Isso é idêntico à emissão do seguinte comando:  
  
```  
SET COLLATE TO cSequenceName  
```  
  
## <a name="remarks"></a>Comentários  
 SET COLLATE permite que você peça tabelas contendo caracteres acentuados para qualquer um dos idiomas suportados. Alterar a configuração de SET COLLATE não afeta a seqüência de colisão de índices abertos anteriormente. O Visual FoxPro mantém automaticamente os índices existentes, proporcionando flexibilidade para criar muitos tipos diferentes de índices, mesmo para o mesmo campo.  
  
 Por exemplo, se um índice for criado com SET COLLATE definido como GERAL e a configuração SET COLLATE for posteriormente alterada para ESPANHOL, o índice retém a seqüência de colagem GERAL.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo da instalação do Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
