---
description: Relatório de avaliação (MySQLToSQL)
title: Relatório de avaliação (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5525d989-024c-402d-9e84-faa4721cc5b9
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6db16aab94dccd4d347325af36c9957f19168059
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88320612"
---
# <a name="assessment-report-mysqltosql"></a>Relatório de avaliação (MySQLToSQL)
A janela relatório de avaliação mostra os resultados da conversão de objetos de banco de dados em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe e também pode ajudá-lo a estimar a complexidade e o custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecione objetos a serem convertidos no Gerenciador de metadados de origem, clique com o botão direito do mouse em **esquemas**e selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Estatísticas de conversão**|Mostra as estatísticas de conversão por tipo de instrução. Esse painel fica visível quando um objeto de grupo, como um esquema, ou um objeto sem código é selecionado no painel esquerdo.|  
|**Objetos por categorias**|Mostra o número de objetos por categoria. Esse painel só é visível quando um objeto de grupo, como um esquema, ou um objeto sem código é selecionado no painel esquerdo.|  
|**Estatísticas**|Mostra as estatísticas de conversão para o objeto selecionado. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo. Talvez seja necessário expandir as **estatísticas**, que estão imediatamente acima do painel de **origem** , para exibir esse painel.|  
|**Origem**|Mostra o código do MySQL para o objeto selecionado e realça o código que não foi convertido em [!INCLUDE[tsql](../../includes/tsql-md.md)] . Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo.<br /><br />Clique nos números de linha para definir ou limpar os indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**Target (destino)**|Mostra o código resultante da conversão [!INCLUDE[tsql](../../includes/tsql-md.md)] para o objeto selecionado e mensagens de erro para o código que não foi convertido. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo.<br /><br />Clique nos números de linha para definir ou limpar os indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**painel Mensagens**|Mostra os erros, avisos e mensagens informativas que foram geradas durante a criação do relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erros**, **avisos**ou **informações**, expanda a categoria de mensagens e clique em uma mensagem.|  
  
