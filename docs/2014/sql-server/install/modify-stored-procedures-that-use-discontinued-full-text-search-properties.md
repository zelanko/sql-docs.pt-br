---
title: Modificar procedimentos armazenados que usem propriedades de pesquisa de texto completo descontinuadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 027fb2a7148dc0948c519836f30c8931d61f610b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012216"
---
# <a name="modify-stored-procedures-that-use-discontinued-full-text-search-properties"></a>Modificar procedimentos armazenados que usam propriedades de Pesquisa de Texto Completo descontinuadas
  Para assegurar que seus procedimentos armazenados tenham o desempenho esperado, você deve editar procedimentos existentes e remover aquelas propriedades e configurações relacionadas a texto completo que foram removidas ou substituídas.  
  
## <a name="component"></a>Componente  
 Pesquisa de Texto Completo  
  
## <a name="description"></a>Description  
 As seguintes propriedades e configurações relacionadas à Pesquisa de Texto Completo foram removidas.  
  
-   **DataTimeout**  
  
-   **ConnectTimeout**  
  
-   **Clean_up**  
  
-   **LogSize**  
  
 As seguintes propriedades e configurações relacionadas à Pesquisa de Texto Completo foram removidas ou substituídas:  
  
-   'Path' do Catálogo de Texto Completo. O Catálogo de Texto Completo será um objeto lógico sem um caminho de arquivo específico no sistema.  
  
-   Habilitar ou desabilitar SP_FULLTEXT_DATABASE não tem mais efeito, uma vez que os bancos de dados estão sempre habilitados para Pesquisa de Texto Completo e por padrão no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="corrective-action"></a>Ação corretiva  
 Modifique seus procedimentos armazenados para remover essas propriedades.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  