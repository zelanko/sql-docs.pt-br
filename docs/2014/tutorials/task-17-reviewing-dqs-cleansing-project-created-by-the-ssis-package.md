---
title: 'Tarefa 17: revisando o projeto de limpeza DQS criado pelo pacote SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fc6cc258-72f5-4593-8edb-9f5bc66de9db
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d60355e28327d7953d0782782e3ec55950314fe5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067089"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>Tarefa 17: Examinando o projeto de limpeza do DQS criado pelo pacote SSIS
  Nesta tarefa, você abrirá o projeto do DQS criado pelo pacote do SSIS no Cliente DQS, analisará os resultados do processo de limpeza e, se desejar, executará a limpeza interativa e exportará os resultados.  
  
1.  Iniciar **Data Quality Client**.  
  
2.  Clique em **monitoramento de atividade** no painel **Administração** .  
  
3.  Classifique a lista com base na **hora de início da atividade** para ver o registro mais recente.  
  
4.  Observe que você vê um nome do projeto no seguinte formato: **CleanseAndCurate. Cleanse Supplier Data. GUID**.  
  
     ![Projeto de Limpeza do DQS criado por pacote do SSIS](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "Projeto de Limpeza do DQS criado por pacote do SSIS")  
  
5.  Observe que o valor no campo **is active** é **ativo**.  
  
6.  Clique na guia **Profiler** no painel inferior para ver as estatísticas do criador de perfil para a atividade de limpeza que o pacote SSIS realizou.  
  
7.  Clique em **fechar** para fechar a tela de **Administração** .  
  
8.  Na página principal do **cliente do DQS**, clique em **Abrir projeto de qualidade de dados** no painel projetos de qualidade de **dados** .  
  
9. Na lista de projetos, selecione o projeto criado pelo componente Limpeza do DQS do SSIS. O nome do projeto deve estar no formato: **CleanseAndCurate. Cleanse Supplier Data. GUID (em cor vermelha)**. Talvez seja necessário classificar a lista com base na coluna **data de criação** e procurar o registro mais recente.  
  
10. Clique em **Próximo**.  
  
11. A página **gerenciar e exibir resultados** deve ser familiar a você da limpeza interativa que você fez anteriormente neste tutorial.  
  
12. Revise os resultados da limpeza. Você também pode executar a limpeza interativa e exportar resultados para um arquivo do Excel ou para um banco de dados na página seguinte.  
  
13. Clique em **Próximo**. Nessa página **Exportar** , você pode exportar os resultados para um arquivo do Excel, um arquivo CSV ou um banco de dados SQL.  
  
14. Clique em **concluir** para concluir a atividade.  
  
15. Na página principal do **cliente do DQS**, clique em **monitoramento de atividade** no painel **Administração** .  
  
16. Observe que o valor do campo **IsActive** para o projeto é **encerrado** agora.  
  
## <a name="next-step"></a>Próxima etapa  
 [Conclusão](../../2014/tutorials/conclusion.md)  
  
  
