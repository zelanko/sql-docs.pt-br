---
title: Caixa de diálogo Propriedades do Conjunto de Dados, Parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10150"
- sql12.rtp.rptdesigner.datasetproperties.parameters.f1
ms.assetid: 43b00aab-e2c3-4e85-abe1-a2b5a21efeed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d621895212e72479090363a980ddc00fa2b5a0c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107330"
---
# <a name="dataset-properties-dialog-box-parameters"></a>Caixa de diálogo Propriedades do Conjunto de Dados, Parâmetros
  Selecione **Parâmetros** na caixa de diálogo **Propriedades do Conjunto de Dados** para adicionar, alterar e excluir os parâmetros de consulta, incluindo os parâmetros de consulta que estabelecem vínculo com os parâmetros de relatório.  
  
 Sempre que a consulta é alterada na guia de consulta, o comando de consulta é analisado. Para cada parâmetro de consulta identificado, um parâmetro de relatório com um nome com diferenciação de maiúsculas e minúsculas idêntico é criado. Por padrão, o parâmetro de consulta é adicionado automaticamente à lista de parâmetros de consulta e vinculado ao parâmetro de relatório correspondente.  
  
 Se houver dependências dos valores padrão de um parâmetro de relatório ou de outro parâmetro de relatório que estiver vinculado ao parâmetro de consulta, a ordem dos parâmetros de relatório (conforme são exibidos na caixa de diálogo **Propriedades de Parâmetros de Relatório** ) será importante. Os últimos parâmetros de relatório da lista podem fazer referência aos primeiros parâmetros de relatório da lista. Para obter mais informações sobre parâmetros de relatório, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="options"></a>Opções  
 **Adicionar**  
 Adicione um novo parâmetro à lista.  
  
 **Delete (excluir)**  
 Remova o parâmetro selecionado da lista.  
  
 **Nome do parâmetro**  
 Digite o nome de um parâmetro de consulta que você adicionou ao conjunto de dados na guia **Consulta** da caixa de diálogo **Propriedades do Conjunto de Dados** .  
  
 **Valor de parâmetro**  
 Informe um valor para o parâmetro de consulta. Esse valor pode ser estático ou uma expressão que faça referência a um objeto dentro do relatório, mas ele não pode fazer referência a todos os itens ou campos do relatório. Por padrão, **Valor** contém uma expressão que aponta para um parâmetro de relatório.  
  
 **Seta para cima**  
 Mova o parâmetro selecionado para cima na lista.  
  
 **Seta para baixo**  
 Mova o parâmetro selecionado para baixo na lista.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-datasets-ssrs.md)   
 [Alterar a ordem de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
  
