---
title: Avaliar os objetos de banco de dados do Access para conversão (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 98d7b1276251e171ce849e04862ac6057a510d4e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>Avaliar os objetos de banco de dados do Access para conversão (AccessToSQL)
Antes de carregar objetos e migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você deve determinar a quantidade de migração seja bem-sucedida, e quanto tempo levará a conversão. O SSMA pode criar um relatório de avaliação que mostra o percentual de objetos que foram convertidos com êxito em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou estimativas de sintaxe SQL Azure e a hora para executar a migração. O SSMA permite exibir os problemas específicos que causou a falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Quando cria um relatório de avaliação, o SSMA converte os objetos de banco de dados de acesso selecionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de SQL Azure e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados de acesso, selecione o banco de dados ou bancos de dados que você deseja avaliar.  
  
2.  Para omitir a objetos individuais, desmarque as caixas de seleção ao lado dos objetos que você não deseja avaliar.  
  
3.  Clique com botão direito **bancos de dados**e, em seguida, selecione **criar relatório**.  
  
    Você também pode analisar os objetos individuais, clicando duas vezes um objeto e, em seguida, selecionando **criar relatório**.  
  
    O SSMA mostra o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
Quando a avaliação for concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para acesso: aparecerá no relatório de avaliação.  
  
## <a name="using-assessment-reports"></a>Usando relatórios de avaliação  
A janela de relatório de avaliação contém três painéis: um pesquisador de objetos, um painel de detalhes e um painel de mensagens.  
  
-   Painel do explorer permite procurar os objetos que foram avaliados. Você pode clicar em itens neste painel para fazer drill down até as chaves, índices e tabelas individuais.  
  
-   O painel de detalhes mostra as estatísticas de conversão para o objeto selecionado.  
  
-   O painel mostra os erros, avisos e mensagens informativas para a conversão e estimativas de tempo para executar a migração e etapas de correção de erros individuais.  
  
Você deve corrigir os erros antes de executar o relatório de avaliação novamente ou converter esquemas. Para localizar erros, clique o **erros** botão no painel de mensagens e, em seguida, expanda cada erro para exibir uma lista de objetos em que ocorreu o erro. Se você clicar em um objeto no painel de mensagens, todos os erros e avisos para o objeto serão exibido no painel de detalhes.  
  
## <a name="next-step"></a>Próxima etapa  
[Converter objetos de banco de dados do Access](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
