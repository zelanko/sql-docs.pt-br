---
title: Caixa de diálogo de propriedades do conjunto de dados, parâmetros (construtor de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10023"
ms.assetid: 3a0672ad-c969-455b-b952-585164ce1dda
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fe7194c8a6f54da50eeef21891bc1049735ddd1e
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59968219"
---
# <a name="dataset-properties-dialog-box-parameters-report-builder"></a>Caixa de diálogo Propriedades do Conjunto de Dados, Parâmetros (Construtor de Relatórios)
  Selecione **parâmetros** sobre o **propriedades do conjunto de dados** caixa de diálogo para adicionar, alterar e excluir parâmetros de consulta.  
  
 Para conjunto de dados inserido, as opções se aplicam a um conjunto de dados na definição do relatório.  
  
 Para conjunto de dados compartilhado, as opções se aplicam à definição do conjunto de dados compartilhado no servidor de relatório.  
  
 Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados &#40;Construtor de Relatórios e SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opções  
 **Adicionar**  
 Adicione um novo parâmetro à lista.  
  
 **Delete (excluir)**  
 Remova o parâmetro selecionado da lista.  
  
 **Seta para cima**  
 Mova o parâmetro selecionado para cima na lista.  
  
 **Seta para baixo**  
 Mova o parâmetro selecionado para baixo na lista.  
  
 **Nome do parâmetro**  
 Digite o nome de um parâmetro de consulta que você adicionou ao conjunto de dados na guia **Consulta** da caixa de diálogo **Propriedades do Conjunto de Dados** .  
  
 **Valor do parâmetro**  
 Somente para conjuntos de dados inseridos.  
  
 Informe um valor para o parâmetro de consulta. Esse valor pode ser estático ou uma expressão que faça referência a um objeto dentro do relatório, mas ele não pode fazer referência a todos os itens ou campos do relatório. Por padrão, **Valor** contém uma expressão que aponta para um parâmetro de relatório.  
  
 **Valor padrão**  
 Somente para conjuntos de dados compartilhados.  
  
 Marque a caixa de seleção para especificar um valor padrão.  
  
 Insira um valor padrão. Esse pode ser um valor estático ou uma expressão que referencie um objeto dentro do relatório. A expressão não pode se referir a itens de relatório, parâmetros de relatório ou campos.  
  
 Para especificar um espaço em branco, deixe a caixa de texto vazia.  
  
 Para especificar um nulo, selecione a opção Anulável.  
  
 **Somente Leitura**  
 Somente para conjuntos de dados compartilhados.  
  
 Selecione essa opção para marcar esse parâmetro como somente leitura na definição do conjunto de dados compartilhado. Quando o conjunto de dados compartilhado for adicionado a um relatório, o parâmetro não aparecerá nas propriedades. Quando o conjunto de dados compartilhado for armazenado em cache no servidor de relatório, não será possível alterar o valor.  
  
 **Permite valor nulo**  
 Somente para conjuntos de dados compartilhados.  
  
 Selecione esta opção para permitir um valor nulo.  
  
 **Omitir da consulta**  
 Somente para conjuntos de dados compartilhados.  
  
 Selecione esta opção quando uma referência a um parâmetro de relatório estiver em uma expressão no filtro do conjunto de dados compartilhado e não na consulta. Quando você selecionar essa opção, não será necessário especificar um valor padrão para esse parâmetro quando a consulta for executada.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Caixa de diálogo de propriedades do conjunto de dados, consulta &#40;construtor de relatórios&#41;](report-data/dataset-properties-dialog-box-query-report-builder.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Tutorial: Adicionar um parâmetro ao relatório &#40;Construtor de Relatórios&#41;](tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Designers de Consultas &#40;Construtor de Relatórios&#41;](../../2014/reporting-services/query-designers-report-builder.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
  
