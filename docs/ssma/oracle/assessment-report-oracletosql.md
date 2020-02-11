---
title: Relatório de avaliação (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 168b7465-a6d6-4329-b46e-fc6c5a3f2d9d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 75fdb97b5b7d763694289d762edc65b4536a86c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68264519"
---
# <a name="assessment-report-oracletosql"></a>Relatório de avaliação (OracleToSQL)
A janela relatório de avaliação mostra os resultados da conversão de objetos de banco [!INCLUDE[tsql](../../includes/tsql-md.md)] de dados em sintaxe e também pode ajudá-lo a estimar a complexidade e o custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecione objetos a serem convertidos no Gerenciador de metadados de origem, clique com o botão direito do mouse em **esquemas** ou **sinônimos**e selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
  
|||  
|-|-|  
|Termo|Definição|  
|**Estatísticas de conversão**|Mostra as estatísticas de conversão por tipo de instrução. Esse painel fica visível quando um objeto de grupo, como um esquema, ou um objeto sem código é selecionado no painel esquerdo.|  
|**Objetos por categorias**|Mostra o número de objetos por categoria. Esse painel só é visível quando um objeto de grupo, como um esquema, ou um objeto sem código é selecionado no painel esquerdo.|  
|**Estatísticas**|Mostra as estatísticas de conversão para o objeto selecionado. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo. Talvez seja necessário expandir as **estatísticas**, que estão imediatamente acima do painel de **origem** , para exibir esse painel.|  
|**Origem**|Mostra o código Oracle para o objeto selecionado e realça o código que não foi convertido em [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo.<br /><br />Clique nos números de linha para definir ou limpar os indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**Alvo**|Mostra o código resultante [!INCLUDE[tsql](../../includes/tsql-md.md)] da conversão para o objeto selecionado e mensagens de erro para o código que não foi convertido. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo.<br /><br />Clique nos números de linha para definir ou limpar os indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**painel Mensagens**|Mostra os erros, avisos e mensagens informativas que foram geradas durante a criação do relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erros**, **avisos**ou **informações**, expanda a categoria de mensagens e clique em uma mensagem.|  
  
