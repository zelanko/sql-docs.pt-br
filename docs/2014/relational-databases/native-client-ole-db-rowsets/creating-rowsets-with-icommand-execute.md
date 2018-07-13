---
title: 'Criando conjuntos de linhas com ICommand:: execute | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
- Execute method
ms.assetid: 9b530b7d-8165-49d4-a978-5ced17c6705e
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 28bfeafa028ce88b0d8132d0fdd2e29eab85b246
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420765"
---
# <a name="creating-rowsets-with-icommandexecute"></a>Criando conjuntos de linhas com ICommand::Execute
  Para conjuntos de linhas criados usando o **ICommand:: execute** método, as propriedades que você deseja no conjunto de linhas resultante pode restringir o texto do comando. Isto é especialmente crítico para consumidores que dão suporte a texto de comando dinâmico.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é possível usar o provedor OLE DB do Native Client [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores para dar suporte os resultados de vários conjuntos de linhas gerados por muitos comandos. Se um consumidor solicitar um conjunto de linhas que exigir suporte de cursor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ocorrerá um erro se o texto do comando gerar mais de um só conjunto de linhas como seu resultado. Para obter mais informações, consulte [resultados de vários conjuntos de linhas de geração de comandos](../native-client-ole-db-commands/commands-generating-multiple-rowset-results.md).  
  
 Rolável [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor OLE DB do Native Client são suportados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indica limitações sobre cursores que são sensíveis às alterações feitas por outros usuários do banco de dados. Especificamente, as linhas em alguns cursores não podem ser ordenadas e a tentativa de criar um conjunto de linhas usando um comando que contenha uma cláusula SQL ORDER BY pode falhar. Para obter mais informações, consulte [conjuntos de linhas e cursores do SQL Server](rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas](rowsets.md)  
  
  
