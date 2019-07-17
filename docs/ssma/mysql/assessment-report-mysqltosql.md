---
title: Relatório de avaliação (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5525d989-024c-402d-9e84-faa4721cc5b9
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: fb6d01bf9c02d0a7b96adf8e46eb354cd426db4d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139187"
---
# <a name="assessment-report-mysqltosql"></a>Relatório de avaliação (MySQLToSQL)
A janela relatório de avaliação mostra os resultados da conversão de objetos de banco de dados para [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, e também pode ajudar a estimar a complexidade e custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecionar objetos a ser convertido no Gerenciador de metadados de código-fonte, clique com botão direito **esquemas**e, em seguida, selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Estatísticas de conversão**|Mostra as estatísticas de conversão pelo tipo de instrução. Esse painel fica visível quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.|  
|**Objetos por categorias**|Mostra o número de objetos por categoria. Esse painel fica visível apenas quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.|  
|**Estatísticas**|Mostra as estatísticas de conversão para o objeto selecionado. Esse painel é visível somente quando um objeto individual com o código é selecionado no painel esquerdo. Talvez você precise expandir **estatísticas**, que está imediatamente acima a **origem** painel para exibir esse painel.|  
|**Source**|Mostra o código do MySQL para o objeto selecionado e destaca o código que não foi convertido em [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esse painel é visível somente quando um objeto individual com o código é selecionado no painel esquerdo.<br /><br />Clique para definir ou limpar indicadores, os números de linha. Use os botões na parte superior do painel para navegar por meio do código.|  
|**Target (destino)**|Mostra a conversão do resultante [!INCLUDE[tsql](../../includes/tsql-md.md)] código para o objeto selecionado e mensagens de erro para o código que não foi convertido. Esse painel é visível somente quando um objeto individual com o código é selecionado no painel esquerdo.<br /><br />Clique para definir ou limpar indicadores, os números de linha. Use os botões na parte superior do painel para navegar por meio do código.|  
|**Painel mensagens**|Mostra os erros, avisos e mensagens informativas que foram geradas durante a criação do relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erros**, **avisos**, ou **informações**, expanda a categoria de mensagens e, em seguida, clique em uma mensagem.|  
  
