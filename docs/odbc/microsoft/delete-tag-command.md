---
title: Comando DELETE TAG | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97ca5abca7e70f5dffdae9bf14ce64429fd203d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303537"
---
# <a name="delete-tag-command"></a>Comando DELETE TAG
Remove uma tag ou tags de um arquivo de índice composto (.cdx).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>Argumentos  
 *TagName1* DE *CDXFileName1*[, *TagName2*[OF *CDXFileName2*]] ...  
 Especifica uma tag para remover de um arquivo de índice composto. Você pode excluir várias tags com uma TAG EXCLUIR, incluindo uma lista de nomes de tags separados por commas. Se existam duas ou mais tags com o mesmo nome nos arquivos de índice aberto, você poderá remover uma tag de um arquivo de índice específico, incluindo *CDXFileName*.  
  
 TUDO [DE *CDXFileName]*  
 Remove todas as etiquetas de um arquivo de índice composto. Se a tabela atual tiver um arquivo de índice composto estrutural, todas as tags serão removidas do arquivo de índice, o arquivo de índice será excluído do disco e o sinalizador no cabeçalho da tabela indicando a presença de um arquivo de índice composto estrutural associado é removido. Use ALL com *cdxfilename* para remover todas as tags de um arquivo de índice composto aberto que não seja o arquivo de índice composto estrutural.  
  
## <a name="remarks"></a>Comentários  
 Os arquivos de índice composto, criados com INDEX, contêm tags correspondentes às entradas de índice. DELETE TAG é usado para remover uma tag ou tags de arquivos de índice composto aberto. Você pode excluir apenas tags de arquivos de índice composto abertos na área de trabalho atual. Se você remover todas as tags de um arquivo de índice composto, o arquivo será excluído do disco.  
  
 Visual FoxPro procura primeiro uma tag no arquivo de índice composto estrutural (se um estiver aberto). Se a tag não estiver no arquivo de índice composto estrutural, o Visual FoxPro procurará a tag nos outros arquivos de índice composto aberto.  
  
## <a name="see-also"></a>Consulte Também  
 [Comando INDEX](../../odbc/microsoft/index-command.md)
