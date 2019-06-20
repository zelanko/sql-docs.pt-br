---
title: Modificar procedimentos armazenados que usam propriedades de pesquisa de texto completo descontinuadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5204b27fb4745f8005a328dc62503f7db418387d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093846"
---
# <a name="modify-stored-procedures-that-use-discontinued-full-text-search-properties"></a>Modificar procedimentos armazenados que usam propriedades de Pesquisa de Texto Completo descontinuadas
  Para assegurar que seus procedimentos armazenados tenham o desempenho esperado, você deve editar procedimentos existentes e remover aquelas propriedades e configurações relacionadas a texto completo que foram removidas ou substituídas.  
  
## <a name="component"></a>Componente  
 Pesquisa de Texto Completo  
  
## <a name="description"></a>Descrição  
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
  
  
