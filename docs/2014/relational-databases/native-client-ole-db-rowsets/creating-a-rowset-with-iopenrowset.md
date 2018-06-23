---
title: Criando um conjunto de linhas com IOpenRowset | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7cdce7632aa726d2992a0383d19691569ed57c0a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122828"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Criando um conjunto de linhas com IOpenRowset
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao provedor do OLE DB Native Client a **IOpenRowset:: OPENROWSET** método com as seguintes restrições:  
  
-   Uma tabela base ou exibição deve ser especificada em um banco de dados ID (DBID) estrutura que o *pTableID* parâmetro aponta para.  
  
-   O DBID *eKind* membro deve indicar DBKIND_NAME.  
  
-   O DBID *uName* membro deve especificar o nome de uma tabela base existente ou uma exibição como uma cadeia de caracteres Unicode.  
  
-   O *pIndexID* parâmetro **OpenRowset** deve ser NULL.  
  
 O conjunto de resultados de **IOpenRowset:: OPENROWSET** contém um único conjunto de linhas. Conjuntos de resultados que contêm um único conjunto de linhas podem ter suporte de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores. O suporte de cursor permite ao desenvolvedor usar mecanismos de simultaneidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas](rowsets.md)  
  
  