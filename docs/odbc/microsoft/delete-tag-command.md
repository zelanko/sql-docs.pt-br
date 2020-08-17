---
description: Comando DELETE TAG
title: Comando excluir marca | Microsoft Docs
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
ms.openlocfilehash: 16eeedd8d9995cf636791688179ba21002411aea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340882"
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
 *TagName1* DE *CDXFileName1*[, *TagName2*[of *CDXFileName2*]]...  
 Especifica uma marca a ser removida de um arquivo de índice composto. Você pode excluir várias marcas com uma marca DELETE, incluindo uma lista de nomes de marca separados por vírgulas. Se houver duas ou mais marcas com o mesmo nome nos arquivos de índice aberto, você poderá remover uma marca de um arquivo de índice específico incluindo *CDXFileName*.  
  
 TODOS [OF *CDXFileName*]  
 Remove cada marca de um arquivo de índice composto. Se a tabela atual tiver um arquivo de índice composto estrutural, todas as marcas serão removidas do arquivo de índice, o arquivo de índice será excluído do disco e o sinalizador no cabeçalho da tabela que indica a presença de um arquivo de índice composto estrutural associado será removido. Use ALL com OF *CDXFileName* para remover todas as marcas de um arquivo de índice composto aberto que não seja o arquivo de índice composto estrutural.  
  
## <a name="remarks"></a>Comentários  
 Os arquivos de índice compostos, criados com o índice, contêm marcas correspondentes às entradas de índice. A marca DELETE é usada para remover uma marca ou marcas de arquivos de índice composto abertos. Você pode excluir somente as marcas de arquivos de índice compostos abertos na área de trabalho atual. Se você remover todas as marcas de um arquivo de índice composto, o arquivo será excluído do disco.  
  
 O Visual FoxPro procura primeiro uma marca no arquivo de índice composto estrutural (se houver uma aberta). Se a marca não estiver no arquivo de índice composto estrutural, o Visual FoxPro procurará a marca nos outros arquivos de índice composto abertos.  
  
## <a name="see-also"></a>Consulte Também  
 [Comando INDEX](../../odbc/microsoft/index-command.md)
