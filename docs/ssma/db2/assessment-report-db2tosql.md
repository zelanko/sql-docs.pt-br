---
title: Relatório de avaliação (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e13eba0-e3cf-4205-974f-c00f982061de
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7b95d5861b0041055b2936a5b1e601b60081124d
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394686"
---
# <a name="assessment-report-db2tosql"></a>Relatório de avaliação (DB2ToSQL)
A janela relatório de avaliação mostra os resultados da conversão de objetos de banco de dados em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe e também pode ajudá-lo a estimar a complexidade e o custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecione objetos a serem convertidos no Gerenciador de metadados de origem, clique com o botão direito do mouse em **esquemas** ou **sinônimos**e selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|-|-|  
|**Estatísticas de conversão**|Mostra as estatísticas de conversão por tipo de instrução. Esse painel fica visível quando um objeto de grupo, como um esquema, ou um objeto sem código é selecionado no painel esquerdo.|  
|**Objetos por categorias**|Mostra o número de objetos por categoria. Esse painel só é visível quando um objeto de grupo, como um esquema, ou um objeto sem código é selecionado no painel esquerdo.|  
|**Estatísticas**|Mostra as estatísticas de conversão para o objeto selecionado. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo. Talvez seja necessário expandir as **estatísticas**, que estão imediatamente acima do painel de **origem** , para exibir esse painel.|  
|**Origem**|Mostra o código DB2 para o objeto selecionado e realça o código que não foi convertido em [!INCLUDE[tsql](../../includes/tsql-md.md)] . Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo.<br /><br />Clique nos números de linha para definir ou limpar os indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**Target (destino)**|Mostra o código resultante da conversão [!INCLUDE[tsql](../../includes/tsql-md.md)] para o objeto selecionado e mensagens de erro para o código que não foi convertido. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo.<br /><br />Clique nos números de linha para definir ou limpar os indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**painel Mensagens**|Mostra os erros, avisos e mensagens informativas que foram geradas durante a criação do relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erros**, **avisos**ou **informações**, expanda a categoria de mensagens e clique em uma mensagem.|  
  
