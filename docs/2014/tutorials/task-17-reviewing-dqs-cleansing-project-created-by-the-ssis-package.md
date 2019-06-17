---
title: 'Tarefa 17: Revisando a limpeza do DQS projeto criado pelo pacote SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fc6cc258-72f5-4593-8edb-9f5bc66de9db
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 285eae7ea20d5919fa73bd0d514c755fe73d9de0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484708"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>Tarefa 17: Revisar o projeto de limpeza do DQS criado pelo pacote SSIS
  Nesta tarefa, você abrirá o projeto do DQS criado pelo pacote do SSIS no Cliente DQS, analisará os resultados do processo de limpeza e, se desejar, executará a limpeza interativa e exportará os resultados.  
  
1.  Inicie **cliente Data Quality**.  
  
2.  Clique em **monitoramento de atividades** na **administração** painel.  
  
3.  Classificar a lista com base em **hora de início da atividade** para ver o registro mais recente.  
  
4.  Observe que você verá o nome do projeto no seguinte formato: **Cleanseandcurate. Cleanse Supplier Data. GUID**.  
  
     ![Projeto de limpeza do DQS criado pelo pacote SSIS](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "projeto de limpeza do DQS criado pelo pacote SSIS")  
  
5.  Observe que o valor de **está ativo** campo é **Active**.  
  
6.  Clique em **Profiler** guia no painel inferior para ver as estatísticas do criador de perfil para a atividade de limpeza que executou o pacote do SSIS.  
  
7.  Clique em **feche** para fechar o **administração** tela.  
  
8.  Na página principal do **cliente DQS**, clique em **Abrir projeto de qualidade de dados** no **projetos de qualidade de dados** painel.  
  
9. Na lista de projetos, selecione o projeto criado pelo componente Limpeza do DQS do SSIS. O nome do projeto deve estar no formato:  **Cleanseandcurate. Cleanse Supplier Data. GUID (em vermelho)** . Talvez seja necessário classificar a lista com base em **data de criação** coluna e procurar o registro mais recente.  
  
10. Clique em **Avançar**.  
  
11. O **gerenciar e exibir resultados** página deve ser familiar para você, desde a limpeza interativa feita anteriormente neste tutorial.  
  
12. Revise os resultados da limpeza. Você também pode executar a limpeza interativa e exportar resultados para um arquivo do Excel ou para um banco de dados na página seguinte.  
  
13. Clique em **Avançar**. Neste **exportar** página, você pode exportar os resultados para um arquivo do excel, arquivo CSV, ou para um banco de dados SQL.  
  
14. Clique em **concluir** para concluir a atividade.  
  
15. Na página principal do **cliente DQS**, clique em **monitoramento de atividade** no **administração** painel.  
  
16. Observe que o valor de **IsActive** campo para o projeto está **concluído** agora.  
  
## <a name="next-step"></a>Próxima etapa  
 [Conclusão](../../2014/tutorials/conclusion.md)  
  
  
