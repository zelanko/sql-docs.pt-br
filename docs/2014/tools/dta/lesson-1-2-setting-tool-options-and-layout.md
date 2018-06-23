---
title: Definindo opções de ferramenta e Layout | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 43e97ce0-97bc-4a27-9485-5bbeb7190b85
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 067e9cfe54b06a226e103c41aeb3a9f41f058954
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120254"
---
# <a name="setting-tool-options-and-layout"></a>Definindo o layout e opções de ferramentas
  É possível definir as opções que configuram o que a GUI (interface gráfica do usuário) do Orientador de Otimização do Mecanismo de Banco de Dados exibe na inicialização, quais fontes ela usa e outra ferramenta de funcionalidade para oferecer o melhor suporte na hora de usá-la. As práticas nesta página irão familiarizá-lo com as opções de definição e como defini-las.  
  
### <a name="set-the-tool-options"></a>Definir as opções de ferramenta  
  
1.  Inicie o Orientador de Otimização do Mecanismo de Banco de Dados. No menu **Iniciar** do Windows, aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Desempenho**e clique em **Orientador de Otimização do Mecanismo de Banco de Dados**.  
  
2.  No menu **Ferramentas** , clique em **Opções**.  
  
3.  Na caixa de diálogo **Opções** , exiba as seguintes opções:  
  
    -   Expanda a lista **Na inicialização** para exibir o que o Orientador de Otimização do Mecanismo de Banco de Dados pode exibir ao ser iniciado. Por padrão, está selecionado **Mostrar uma nova sessão** .  
  
    -   Clique em **Alterar Fonte** para consultar quais fontes você pode escolher para as listas de bancos de dados e tabelas na guia **Geral** . As fontes escolhidas para essa opção também serão usadas nos relatórios e grades de recomendação do Orientador de Otimização do Mecanismo de Banco de Dados após a execução do ajuste. Por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados usa fontes de sistema.  
  
    -   O **Número de itens nas listas usadas mais recentemente** pode ser definido entre **1** e **10**. Isso define o número máximo de itens nas listas exibidas ao se clicar em **Sessões Recentes** ou **Arquivos Recentes** no menu **Arquivo** . Por padrão, essa opção está definida como **4**.  
  
    -   Quando **Lembrar minhas últimas opções de ajuste** está marcada, por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados usa as opções de ajuste especificadas em sua última sessão de ajuste para a próxima sessão. Desmarque essa caixa de seleção para usar as opções de ajuste padrão do Orientador de Otimização do Mecanismo de Banco de Dados. Por padrão, essa opção é selecionada.  
  
    -   Por padrão, **Perguntar antes de excluir permanentemente as sessões** está marcada para evitar excluir sessões de ajuste acidentalmente.  
  
    -   Por padrão, **Perguntar antes de parar a análise da sessão** está marcada para evitar parar uma sessão de ajuste acidentalmente antes que o Orientador de Otimização do Mecanismo de Banco de Dados termine de analisar uma carga de trabalho.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  