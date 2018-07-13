---
title: Criando um conjunto de linhas com IOpenRowset | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30ba5a4d1cbe326be567a3be18cd7a76371f7e49
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417935"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Criando um conjunto de linhas com IOpenRowset
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao provedor de OLE DB do Native Client a **IOpenRowset:: OPENROWSET** método com as seguintes restrições:  
  
-   Uma tabela base ou exibição deve ser especificada em um banco de dados de estrutura de ID (DBID) que o *pTableID* parâmetro aponta.  
  
-   O DBID *eKind* membro deve indicar DBKIND_NAME.  
  
-   O DBID *uName* membro deve especificar o nome de uma tabela base existente ou uma exibição como uma cadeia de caracteres Unicode.  
  
-   O *pIndexID* parâmetro do **OpenRowset** deve ser NULL.  
  
 O conjunto de resultados de **IOpenRowset:: OPENROWSET** contém um único conjunto de linhas. Conjuntos de resultados que contêm um único conjunto de linhas podem ser suportados por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores. O suporte de cursor permite ao desenvolvedor usar mecanismos de simultaneidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas](rowsets.md)  
  
  
