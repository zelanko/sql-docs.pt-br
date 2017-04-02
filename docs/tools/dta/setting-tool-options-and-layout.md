---
title: "Definindo o layout e op&#231;&#245;es de ferramentas | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "Mecanismo de banco de dados [SQL Server], tutoriais"
ms.assetid: 43e97ce0-97bc-4a27-9485-5bbeb7190b85
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Definindo o layout e op&#231;&#245;es de ferramentas
É possível definir as opções que configuram o que a GUI (interface gráfica do usuário) do Orientador de Otimização do Mecanismo de Banco de Dados exibe na inicialização, quais fontes ela usa e outra ferramenta de funcionalidade para oferecer o melhor suporte na hora de usá-la. As práticas nesta página irão familiarizá-lo com as opções de definição e como defini-las.  
  
### Definir as opções de ferramenta  
  
1.  Inicie o Orientador de Otimização do Mecanismo de Banco de Dados. No menu **Iniciar** do Windows, aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Desempenho**e clique em **Orientador de Otimização do Mecanismo de Banco de Dados**.  
  
2.  No menu **Ferramentas** , clique em **Opções**.  
  
3.  Na caixa de diálogo **Opções** , exiba as seguintes opções:  
  
    -   Expanda a lista **Na inicialização** para exibir o que o Orientador de Otimização do Mecanismo de Banco de Dados pode exibir ao ser iniciado. Por padrão, está selecionado **Mostrar uma nova sessão** .  
  
    -   Clique em **Alterar Fonte** para consultar quais fontes você pode escolher para as listas de bancos de dados e tabelas na guia **Geral** . As fontes escolhidas para essa opção também serão usadas nos relatórios e grades de recomendação do Orientador de Otimização do Mecanismo de Banco de Dados após a execução do ajuste. Por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados usa fontes de sistema.  
  
    -   O **Número de itens nas listas usadas mais recentemente** pode ser definido entre **1** e **10**. Isso define o número máximo de itens nas listas exibidas ao se clicar em **Sessões Recentes** ou **Arquivos Recentes** no menu **Arquivo** . Por padrão, essa opção está definida como **4**.  
  
    -   Quando **Lembrar minhas últimas opções de ajuste** está marcada, por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados usa as opções de ajuste especificadas em sua última sessão de ajuste para a próxima sessão. Desmarque essa caixa de seleção para usar as opções de ajuste padrão do Orientador de Otimização do Mecanismo de Banco de Dados. Por padrão, essa opção é selecionada.  
  
    -   Por padrão, **Perguntar antes de excluir permanentemente as sessões** está marcada para evitar excluir sessões de ajuste acidentalmente.  
  
    -   Por padrão, **Perguntar antes de parar a análise da sessão** está marcada para evitar parar uma sessão de ajuste acidentalmente antes que o Orientador de Otimização do Mecanismo de Banco de Dados termine de analisar uma carga de trabalho.  
  
## Próxima lição  
[Lição 2: Usando o Orientador de Otimização do Mecanismo de Banco de Dados](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
  
  
  
