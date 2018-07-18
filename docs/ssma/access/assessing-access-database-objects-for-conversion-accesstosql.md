---
title: Avaliar os objetos de banco de dados do Access para conversão (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: d2d804734432cfd396acb017d6358310debeec1f
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979418"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>Avaliar os objetos de banco de dados do Access para conversão (AccessToSQL)
Antes de carregar objetos e migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você deve determinar o quanto da migração seja bem-sucedida, e quanto a conversão pode levar. O SSMA pode criar um relatório de avaliação que mostra o percentual de objetos que foram convertidos com êxito para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou estimativas de sintaxe do SQL Azure e a hora para executar a migração. O SSMA também permite que você exiba os problemas específicos que causava falhas de conversão.  
  
## <a name="creating-assessment-reports"></a>Criando relatórios de avaliação  
Quando ele cria um relatório de avaliação, o SSMA converte os objetos de banco de dados de acesso selecionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de SQL Azure e, em seguida, mostra os resultados.  
  
**Para criar um relatório de avaliação**  
  
1.  No Gerenciador de metadados de acesso, selecione o banco de dados ou bancos de dados que você deseja avaliar.  
  
2.  Para omitir objetos individuais, desmarque as caixas de seleção ao lado de objetos que você não deseja avaliar.  
  
3.  Clique com botão direito **bancos de dados**e, em seguida, selecione **criar relatório**.  
  
    Você também pode analisar objetos individuais clicando duas vezes um objeto e, em seguida, selecionando **criar relatório**.  
  
    O SSMA mostra o progresso na barra de status na parte inferior da janela. Se o painel de saída estiver visível, você também verá mensagens no painel de saída.  
  
Quando a avaliação for concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Access: relatório de avaliação de janela é exibida.  
  
## <a name="using-assessment-reports"></a>Usando relatórios de avaliação  
A janela de relatório de avaliação contém três painéis: um explorador, um painel de detalhes e um painel de mensagens.  
  
-   O painel do explorer permite procurar os objetos que foram avaliados. Você pode clicar em itens neste painel para detalhar as chaves, índices e tabelas individuais.  
  
-   O painel de detalhes mostra as estatísticas de conversão para o objeto selecionado.  
  
-   O painel mostra os erros, avisos e mensagens informativas para a conversão e estimativas de tempo para executar a migração e as etapas de correção de erros individuais.  
  
Você deve corrigir os erros antes de executar o relatório de avaliação novamente ou converter esquemas. Para encontrar erros, clique o **erros** botão no painel de mensagens e, em seguida, expanda cada erro para exibir uma lista de objetos onde ocorreu o erro. Se você clicar em um objeto no painel de mensagens, todos os erros e avisos para esse objeto aparecerá no painel de detalhes.  
  
## <a name="next-step"></a>Próxima etapa  
[Converter objetos de banco de dados do Access](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
