---
title: 'Tarefa 3: Criando e executando um projeto de qualidade de dados para correspondência | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6260e911-ea8b-4c69-a39d-d1bccd565a32
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: abca2dcf68472884eb3c1e42f0ff9c14004098c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250015"
---
# <a name="task-3-creating-and-running-a-data-quality-project-for-matching"></a>Tarefa 3: Criar e executar um projeto de qualidade de dados para correspondência
  Nesta tarefa, você criará um Projeto do Data Quality para a atividade de correspondência e executará o processo de correspondência nos dados de fornecedor limpos para remover as duplicatas nos dados.  
  
1.  Na página principal do **cliente DQS**, clique em **novo projeto de qualidade de dados**.  
  
2.  Tipo de **remover duplicatas do fornecedor** da **nome do projeto**.  
  
3.  Selecione **fornecedores** na lista de bases de dados para o **usar a Base de dados de Conhecimento** campo. Você criou uma política de correspondência nessa base de dados de conhecimento na lição anterior.  
  
4.  Selecione **correspondentes** da **lista de atividades** no painel inferior direito.  
  
     ![Novo projeto de qualidade de dados - correspondência selecionada](../../2014/tutorials/media/et-creatingandrunningadqpformatching.jpg "novo projeto de qualidade de dados - correspondência selecionada")  
  
5.  Clique em **Avançar**.  
  
6.  Na página **Mapear** , selecione **Arquivo do Excel** em **Fonte de Dados**.  
  
7.  Clique em **navegue** e selecione **Cleansed Supplier List**, que é o arquivo de saída da atividade de limpeza.  
  
8.  Mapa **SupplierID** coluna de origem para o **Supplier ID** domínio, **Supplier Name** coluna **Supplier Name** edomínio**ContactEmailAddress** coluna para **Contact Email** domínio.  
  
9. Clique em **próxima** para alternar para o **correspondentes** página.  
  
10. Clique em **iniciar** para iniciar o processo de correspondência. Você deverá visualizar resultados semelhantes aos da tarefa anterior, pois usou o mesmo arquivo de entrada para definir a política de correspondência.  
  
11. Revise todos os registros correspondentes e sua pontuação na caixa de listagem. Os resultados deverão ser iguais aos exibidos na tarefa anterior. Consulte as etapas na tarefa anterior para analisar os resultados dessa atividade de correspondência.  
  
12. Clique em **próxima** para alternar para o **exportar** página.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 4: Exportando os resultados de correspondência de atividade para um arquivo do Excel](../../2014/tutorials/task-4-exporting-the-results-from-matching-activity-to-an-excel-file.md)  
  
  
