---
title: Comando de marca de exclusão | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 576e7e10d9d6f5c7e8616f57bde2dfed05503eae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112068"
---
# <a name="delete-tag-command"></a>Comando DELETE TAG
Remove uma marca ou marcas de um arquivo de índice composto (. cdx).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>Argumentos  
 *TagName1*OF *CDXFileName1*[, *TagName2*[OF *CDXFileName2*]]...  
 Especifica uma marca a ser removido de um arquivo de índice composto. Você pode excluir várias marcas com uma marca de excluir, incluindo uma lista de nomes de marca separados por vírgulas. Se duas ou mais marcas com o mesmo nome existirem nos arquivos de índice aberto, você pode remover uma marca de um arquivo de índice específico incluindo OF *CDXFileName*.  
  
 Todos os [OF *CDXFileName*]  
 Remove cada marca de um arquivo de índice composto. Se a tabela atual tem um arquivo de índice composto estrutural, todas as marcas são removidas do arquivo de índice, o arquivo de índice é excluído do disco e o sinalizador no cabeçalho da tabela que indica a presença de um arquivo de índice composto de estrutural associado é removido. Use tudo isso com OF *CDXFileName* para remover todas as marcas de um arquivo de índice composto aberto que não seja o arquivo de índice composto estrutural.  
  
## <a name="remarks"></a>Comentários  
 Arquivos de índice composto, criados com o índice, contenham marcas correspondentes a entradas de índice. Excluir marca é usada para remover uma marca ou marcas de arquivos de índice composto aberto. Você pode excluir apenas as marcas de arquivos de índice composto abertos na área de trabalho atual. Se você remover todas as marcas de um arquivo de índice composto, o arquivo é excluído do disco.  
  
 Do Visual FoxPro procura primeiro uma marca no arquivo de índice composto estrutural (se estiver aberto). Se a marca não estiver no arquivo de índice composto estrutural, Visual FoxPro, em seguida, procura a marca em outros arquivos de índice composto aberto.  
  
## <a name="see-also"></a>Consulte também  
 [Comando INDEX](../../odbc/microsoft/index-command.md)
