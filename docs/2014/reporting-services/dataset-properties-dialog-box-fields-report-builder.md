---
title: Caixa de diálogo Propriedades do conjunto de, campos (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10021"
ms.assetid: 75c7e54a-3d20-4c9a-88da-ab36dce2ce42
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 375d8eda6f0863dbe3852f1a88ea2e58ecc85b80
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109429"
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
  
 **Origem de Campo**  
 Insira um valor para o campo.  
  
 Para um campo calculado, a origem do campo deve ter o nome de um campo existente recuperado pela consulta do conjunto de dados ou uma expressão criada por você. Por exemplo, para criar um campo que represente 10 vezes o valor no campo de consulta Sales, use a expressão `=10 * Fields!Sales.Value`.  
  
 Para um campo de consulta, a origem do campo deve ter o nome de um campo existente recuperado pela consulta de conjunto de dados.  
  
 **Expressão (fx)**  
 Adicione ou altere uma expressão para o novo campo calculado. Esse botão só é exibido quando você clica em **Adicionar** e seleciona **Campo Calculado**.  
  
## <a name="see-also"></a>Consulte Também  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Criar um conjunto de um DataSet compartilhado ou um conjunto de &#40;inserido Construtor de Relatórios e SSRS&#41;](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Construtor de Relatórios ajuda para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Caixa de diálogo Propriedades do conjunto de, opções &#40;Construtor de Relatórios&#41;](report-data/dataset-properties-dialog-box-options-report-builder.md)   
 [Caixa de diálogo Propriedades do conjunto de, filtros &#40;Construtor de Relatórios&#41;](../../2014/reporting-services/dataset-properties-dialog-box-filters-report-builder.md)   
 [Caixa de diálogo Propriedades do conjunto de, parâmetros &#40;Construtor de Relatórios&#41;](../../2014/reporting-services/dataset-properties-dialog-box-parameters-report-builder.md)   
 [Caixa de diálogo Propriedades do conjunto de &#40;, Construtor de Relatórios de consulta&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  
