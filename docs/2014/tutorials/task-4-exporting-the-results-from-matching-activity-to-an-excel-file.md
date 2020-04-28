---
title: 'Tarefa 4: exportando os resultados da atividade correspondente para um arquivo do Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4ed1d29af328a162eafadb1ce7a160c262bdcba3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177244"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>Tarefa 4: Exportando os resultados da atividade de correspondência para um arquivo do Excel
  Nesta tarefa, você exportará os resultados da atividade de correspondência para um arquivo do Excel.

1.  Na página **Exportar** , selecione **arquivo do Excel** para o **tipo de destino**.

2.  Selecione a opção **sobrevivência Results** . No processo sobrevivência, o DQS determina um registro sobrevivente para cada cluster com base na **regra sobrevivência** selecionada.

3.  Clique em **procurar** e navegue até a pasta onde você deseja armazenar o arquivo de saída.

4.  Digite **cleaned e MATCHED suppliers. xls** para o nome e clique em **abrir**.

5.  Confirme se o **registro dinâmico** está selecionado para a **regra sobrevivência**. Quando você selecionar essa opção, o registro dinâmico de cada cluster será escolhido como a saída de um cluster. As outras opções para a Regra de Sobrevivência são:

    1.  **Registro mais completo:** O registro sobrevivente é aquele com o maior número de campos preenchidos.

    2.  **Registro mais longo:** O registro sobrevivente é aquele com o maior número de termos em campos de origem.

    3.  **Registro mais completo e mais longo:** O registro sobrevivente é aquele com o maior número de campos preenchidos e tem o maior número de termos em cada campo.

     ![Exportar Resultados da página correspondente](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "Exportar Resultados da página correspondente")

6.  Clique em **Exportar** para exportar os resultados para um arquivo do Excel.

7.  Clique em **fechar** para fechar a caixa de diálogo **exportação de correspondência** .

8.  Clique em **concluir** para concluir a atividade de correspondência.

9. Abra o arquivo **supplied e MATCHED Vendors. xlsx** e confirme se você não vê duplicatas (CódigoDoFornecedor).

 Agora, você tem dados de fornecedor que foram limpos e correspondidos para remover duplicatas.

## <a name="next-step"></a>Próxima etapa
 [Lição 4: Armazenando dados do fornecedor no MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)


