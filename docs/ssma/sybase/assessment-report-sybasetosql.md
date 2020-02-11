---
title: Relatório de avaliação (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c6d83e81253430f243fcaed55b66f6d0de6299ca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083501"
---
# <a name="assessment-report-sybasetosql"></a>Relatório de avaliação (SybaseToSQL)
A janela relatório de avaliação mostra os resultados da conversão de objetos de banco [!INCLUDE[tsql](../../includes/tsql-md.md)] de dados em sintaxe e também pode ajudá-lo a estimar a complexidade e o custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecione objetos a serem convertidos no Gerenciador de metadados de origem, clique com o botão direito do mouse em **bancos de dados**e selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
**Estatísticas de conversão**  
Mostra as estatísticas de conversão por tipo de instrução. Esse painel só é visível quando um objeto de grupo, como um esquema, ou um objeto sem código é selecionado no painel esquerdo.  
  
**Objetos por categoria**  
Mostra as estatísticas de conversão por tipo de objeto. Esse painel só é visível quando um objeto de grupo, como um esquema, ou um objeto sem código é selecionado no painel esquerdo.  
  
**Estatísticas**  
Mostra as estatísticas de conversão para o objeto selecionado. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo. Talvez seja necessário expandir as **estatísticas** para exibir esse painel.  
  
**Navegação de origem**  
Mostra o código do ASE para o objeto selecionado e realça o código que não foi convertido [!INCLUDE[tsql](../../includes/tsql-md.md)]em. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo.  
  
Clique nos números de linha para definir ou limpar os indicadores. Use os botões na parte superior do painel para navegar pelo código.  
  
**Navegação de destino**  
Mostra o código resultante [!INCLUDE[tsql](../../includes/tsql-md.md)] da conversão para o objeto selecionado e mensagens de erro para o código que não foi convertido. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo.  
  
Clique nos números de linha para definir ou limpar os indicadores. Use os botões na parte superior do painel para navegar pelo código.  
  
**painel Mensagens**  
Mostra os erros, avisos e mensagens de informações que são gerados durante a criação do relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erro**, **aviso**ou **informações**, expanda a categoria de mensagens e clique em uma mensagem.  
  
