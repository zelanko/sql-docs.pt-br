---
title: Caixa de diálogo de propriedades do conjunto de dados, campos (construtor de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10021"
ms.assetid: 75c7e54a-3d20-4c9a-88da-ab36dce2ce42
caps.latest.revision: 14
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 8e9fa18bb0edfc2edac3e58e22467ba49a01cf50
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009935"
---
# <a name="dataset-properties-dialog-box-fields-report-builder"></a>Caixa de diálogo Propriedades do Conjunto de Dados, Campos (Construtor de Relatórios)
  Selecione **Campos** na caixa de diálogo **Propriedades do Conjunto de Dados** para alterar a coleção de campos para o conjunto de dados de relatório. A lista de campos é preenchida automaticamente, mas você pode usar os **Campos** para adicionar, editar e excluir campos calculados e consultas.  
  
 Somente há suporte para campos calculados em conjuntos de dados inseridos. Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opções  
 **Adicionar**  
 Adicione uma nova consulta ou campo calculado ao conjunto de dados.  
  
 **Delete (excluir)**  
 Exclua o campo selecionado do conjunto de dados.  
  
 **Nome do campo**  
 Digite um nome para o campo. O campo deve ser exclusivo no conjunto de dados. Para cada campo existente no conjunto de dados, o nome é pré-preenchido.  
  
 **Origem do campo**  
 Insira um valor para o campo.  
  
 Para um campo calculado, a origem do campo deve ter o nome de um campo existente recuperado pela consulta do conjunto de dados ou uma expressão criada por você. Por exemplo, para criar um campo que represente 10 vezes o valor no campo de consulta Sales, use a expressão `=10 * Fields!Sales.Value`.  
  
 Para um campo de consulta, a origem do campo deve ter o nome de um campo existente recuperado pela consulta de conjunto de dados.  
  
 **Expressão (fx)**  
 Adicione ou altere uma expressão para o novo campo calculado. Esse botão só é exibido quando você clica em **Adicionar** e seleciona **Campo Calculado**.  
  
## <a name="see-also"></a>Consulte também  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Caixa de diálogo de propriedades do conjunto de dados, opções &#40;construtor de relatórios&#41;](report-data/dataset-properties-dialog-box-options-report-builder.md)   
 [Caixa de diálogo de propriedades do conjunto de dados, filtros &#40;construtor de relatórios&#41;](../../2014/reporting-services/dataset-properties-dialog-box-filters-report-builder.md)   
 [Caixa de diálogo de propriedades do conjunto de dados, parâmetros &#40;construtor de relatórios&#41;](../../2014/reporting-services/dataset-properties-dialog-box-parameters-report-builder.md)   
 [Caixa de diálogo de propriedades do conjunto de dados, a consulta &#40;construtor de relatórios&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  