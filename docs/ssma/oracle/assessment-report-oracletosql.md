---
title: Relatório de avaliação (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 168b7465-a6d6-4329-b46e-fc6c5a3f2d9d
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 446a0bb9782d1e5e1c4072d7ef121d408dad1aa1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="assessment-report-oracletosql"></a>Relatório de avaliação (OracleToSQL)
A janela do relatório de avaliação mostra os resultados da conversão de objetos de banco de dados para [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe, e também pode ajudar a estimar a complexidade e o custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecionados objetos para converter no Gerenciador de metadados de origem, clique com botão direito **esquemas** ou **sinônimos**e, em seguida, selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
  
|||  
|-|-|  
|Termo|Definição|  
|**Estatísticas de conversão**|Mostra as estatísticas de conversão por tipo de instrução. Esse painel fica visível quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.|  
|**Objetos por categorias**|Mostra o número de objetos por categoria. Esse painel fica visível apenas quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.|  
|**Estatísticas**|Mostra as estatísticas de conversão para o objeto selecionado. Esse painel é visível somente quando um objeto individual com o código for selecionado no painel esquerdo. Talvez você precise expandir **estatísticas**, que está imediatamente acima do **fonte** painel para exibir este painel.|  
|**Origem**|Mostra o código do Oracle para o objeto selecionado e realça o código que não foi convertido para [!INCLUDE[tsql](../../includes/tsql_md.md)]. Esse painel é visível somente quando um objeto individual com o código for selecionado no painel esquerdo.<br /><br />Clique no número de linha para definir ou limpar indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**Target (destino)**|Mostra a conversão do resultante [!INCLUDE[tsql](../../includes/tsql_md.md)] código para o objeto selecionado e mensagens de erro de código que não foi convertido. Esse painel é visível somente quando um objeto individual com o código for selecionado no painel esquerdo.<br /><br />Clique no número de linha para definir ou limpar indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**Painel mensagens**|Mostra os erros, avisos e mensagens informativas que foram geradas durante a criação do relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erros**, **avisos**, ou **informações**, expanda a categoria de mensagens e, em seguida, clique em uma mensagem.|  
  
