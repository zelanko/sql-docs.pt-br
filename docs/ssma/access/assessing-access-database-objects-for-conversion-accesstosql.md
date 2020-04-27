---
title: Avaliando objetos de banco de dados do Access para conversão (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- assessing SQL
- assessing syntax
- assessment reports
- creating assessment reports
- estimating migration effort
- reports
- SQL, assessing
- syntax, assessing
ms.assetid: 8b9e23d6-da62-437a-8c05-8ad2628b9441
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 4c2f5bc6953ab0e96397ca728391cbe22a73dd50
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67910697"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>Avaliando objetos de banco de dados do Access para conversão (AccessToSQL)
Antes de carregar objetos e migrar dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o ou SQL Azure, você deve determinar quanto da migração será bem-sucedida e por quanto tempo a conversão pode demorar. O SSMA pode criar um relatório de avaliação que mostra a porcentagem de objetos que foram convertidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com êxito em ou SQL Azure estimativas de sintaxe e tempo para executar a migração. O SSMA também permite que você exiba os problemas específicos que causaram falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Quando ele cria um relatório de avaliação, o SSMA converte os objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados do Access selecionados em ou SQL Azure sintaxe e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados do Access, selecione os bancos de dados que você deseja avaliar.  
  
2.  Para omitir objetos individuais, desmarque as caixas de seleção ao lado dos objetos que você não deseja avaliar.  
  
3.  Clique com o botão direito do mouse em **bancos de dados**e selecione **criar relatório**.  
  
    Você também pode analisar objetos individuais clicando com o botão direito do mouse em um objeto e selecionando **criar relatório**.  
  
    O SSMA mostra o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
Quando a avaliação for concluída, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] janela Assistente de migração para acesso: relatório de avaliação será exibida.  
  
## <a name="using-assessment-reports"></a>Usando relatórios de avaliação  
A janela relatório de avaliação contém três painéis: um Explorer, um painel de detalhes e um painel de mensagens.  
  
-   O painel Gerenciador permite procurar os objetos que foram avaliados. Você pode clicar em itens neste painel para fazer uma busca detalhada em tabelas, índices e chaves individuais.  
  
-   O painel detalhes mostra as estatísticas de conversão para o objeto selecionado.  
  
-   O painel de mensagens mostra erros, avisos e mensagens informativas para a conversão e estimativas de tempo para a execução das etapas de correção de erro individual e de migração.  
  
Você deve corrigir os erros antes de executar o relatório de avaliação novamente ou converter esquemas. Para localizar erros, clique no botão **erros** no painel mensagens e, em seguida, expanda cada erro para exibir uma lista de objetos em que o erro ocorreu. Se você clicar em um objeto no painel mensagens, todos os erros e avisos para esse objeto aparecerão no painel detalhes.  
  
## <a name="next-step"></a>Próxima etapa  
[Converter objetos de banco de dados do Access](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
