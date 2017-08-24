---
title: "Relatório de avaliação (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9e13eba0-e3cf-4205-974f-c00f982061de
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2b984492a5c41bf971170076a2ab03f9c1af48ec
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="assessment-report-db2tosql"></a>Relatório de avaliação (DB2ToSQL)
A janela do relatório de avaliação mostra os resultados da conversão de objetos de banco de dados para [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe, e também pode ajudar a estimar a complexidade e o custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecionados objetos para converter no Gerenciador de metadados de origem, clique com botão direito **esquemas** ou **sinônimos**e, em seguida, selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
  
|||  
|-|-|  
|Termo|Definição|  
|**Estatísticas de conversão**|Mostra as estatísticas de conversão por tipo de instrução. Esse painel fica visível quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.|  
|**Objetos por categorias**|Mostra o número de objetos por categoria. Esse painel fica visível apenas quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.|  
|**Estatísticas**|Mostra as estatísticas de conversão para o objeto selecionado. Esse painel é visível somente quando um objeto individual com o código for selecionado no painel esquerdo. Talvez você precise expandir **estatísticas**, que está imediatamente acima do **fonte** painel para exibir este painel.|  
|**Origem**|Mostra o código do DB2 para o objeto selecionado e realça o código que não foi convertido para [!INCLUDE[tsql](../../includes/tsql_md.md)]. Esse painel é visível somente quando um objeto individual com o código for selecionado no painel esquerdo.<br /><br />Clique no número de linha para definir ou limpar indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**Target (destino)**|Mostra a conversão do resultante [!INCLUDE[tsql](../../includes/tsql_md.md)] código para o objeto selecionado e mensagens de erro de código que não foi convertido. Esse painel é visível somente quando um objeto individual com o código for selecionado no painel esquerdo.<br /><br />Clique no número de linha para definir ou limpar indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**Painel mensagens**|Mostra os erros, avisos e mensagens informativas que foram geradas durante a criação do relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erros**, **avisos**, ou **informações**, expanda a categoria de mensagens e, em seguida, clique em uma mensagem.|  
  

