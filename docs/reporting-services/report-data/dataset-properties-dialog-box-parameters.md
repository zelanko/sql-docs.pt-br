---
title: Caixa de diálogo Propriedades do Conjunto de Dados, Parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-data
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- "10150"
- sql13.rtp.rptdesigner.datasetproperties.parameters.f1
- "10023"
ms.assetid: 43b00aab-e2c3-4e85-abe1-a2b5a21efeed
caps.latest.revision: 40
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3a6cb62404bc37e48bdf87d370fc3277341cbcff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="dataset-properties-dialog-box-parameters"></a>Caixa de diálogo Propriedades do Conjunto de Dados, Parâmetros
  Selecione **Parâmetros** na caixa de diálogo **Propriedades do Conjunto de Dados** para adicionar, alterar e excluir os parâmetros de consulta, incluindo os parâmetros de consulta que estabelecem vínculo com os parâmetros de relatório.  
  
 Sempre que a consulta é alterada na guia de consulta, o comando de consulta é analisado. Para cada parâmetro de consulta identificado, um parâmetro de relatório com um nome com diferenciação de maiúsculas e minúsculas idêntico é criado. Por padrão, o parâmetro de consulta é adicionado automaticamente à lista de parâmetros de consulta e vinculado ao parâmetro de relatório correspondente.  
  
 Se houver dependências dos valores padrão de um parâmetro de relatório ou de outro parâmetro de relatório que estiver vinculado ao parâmetro de consulta, a ordem dos parâmetros de relatório (conforme são exibidos na caixa de diálogo **Propriedades de Parâmetros de Relatório** ) será importante. Os últimos parâmetros de relatório da lista podem fazer referência aos primeiros parâmetros de relatório da lista. Para obter mais informações sobre parâmetros de relatório, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="options"></a>Opções  
 **Adicionar**  
 Adicione um novo parâmetro à lista.  
  
 **Delete (excluir)**  
 Remova o parâmetro selecionado da lista.  
  
 **Nome do parâmetro**  
 Digite o nome de um parâmetro de consulta que você adicionou ao conjunto de dados na guia **Consulta** da caixa de diálogo **Propriedades do Conjunto de Dados** .  
  
 **Valor do parâmetro**  
 Informe um valor para o parâmetro de consulta. Esse valor pode ser estático ou uma expressão que faça referência a um objeto dentro do relatório, mas ele não pode fazer referência a todos os itens ou campos do relatório. Por padrão, **Valor** contém uma expressão que aponta para um parâmetro de relatório.  
  
 **Seta para cima**  
 Mova o parâmetro selecionado para cima na lista.  
  
 **Seta para baixo**  
 Mova o parâmetro selecionado para baixo na lista.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Alterar a ordem de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
  
