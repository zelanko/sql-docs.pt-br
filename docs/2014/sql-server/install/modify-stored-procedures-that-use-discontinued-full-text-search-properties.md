---
title: Modificar procedimentos armazenados que usam propriedades de pesquisa de texto completo descontinuadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d6d7467da572d5d0552d400e2c05505c1bc0aaa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091519"
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
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
