---
title: 'Tarefa 4: Exportando os resultados de correspondência de atividade para um arquivo do Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 13fcd1b697be6ad7aeebd933da1059955dc0649f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178975"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>Tarefa 4: Exportando os resultados da atividade de correspondência para um arquivo do Excel
  Nesta tarefa, você exportará os resultados da atividade de correspondência para um arquivo do Excel.  
  
1.  No **exportar** página, selecione **arquivo do Excel** para o **tipo de destino**.  
  
2.  Selecione **resultados de sobrevivência** opção. No processo de sobrevivência, o DQS determina o registro sobrevivente para cada cluster de acordo com o **regra de sobrevivência** você selecionou.  
  
3.  Clique em **procurar** e navegue até a pasta onde você deseja armazenar o arquivo de saída.  
  
4.  Tipo de **Cleansed and Matched Suppliers. xls** para o nome e clique **abrir**.  
  
5.  Confirme **registro dinâmico** está selecionado para o **regra de sobrevivência**. Quando você selecionar essa opção, o registro dinâmico de cada cluster será escolhido como a saída de um cluster. As outras opções para a Regra de Sobrevivência são:  
  
    1.  **Registro mais completo:** o registro sobrevivente é aquele com o maior número de campos populados.  
  
    2.  **Registro mais longo:** o registro sobrevivente é aquele com o maior número de termos nos campos de origem.  
  
    3.  **Registro mais completo e mais longo:** o registro sobrevivente é aquele com o maior número de campos populados e com o maior número de termos em cada campo.  
  
     ![Exportar resultados da página correspondente](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "exportar resultados da página correspondente")  
  
6.  Clique em **exportar** para exportar os resultados para um arquivo do Excel.  
  
7.  Clique em **feche** para fechar o **exportação de correspondência** caixa de diálogo.  
  
8.  Clique em **concluir** para concluir a atividade de correspondência.  
  
9. Abra o **Cleansed and Matched Suppliers** de arquivo e confirme que você não vir nenhuma duplicata (SupplierID).  
  
 Agora, você tem dados de fornecedor que foram limpos e correspondidos para remover duplicatas.  
  
## <a name="next-step"></a>Próxima etapa  
 [Lição 4: Armazenando dados do fornecedor no MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)  
  
  
