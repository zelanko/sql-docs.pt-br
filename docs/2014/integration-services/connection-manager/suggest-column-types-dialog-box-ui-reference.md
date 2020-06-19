---
title: Referência de interface do usuário da caixa de diálogo Sugerir Tipos de Coluna | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.suggestdatatypes.f1
ms.assetid: 8d5652e0-cf57-483f-828b-10f00c08418b
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c1c0946d766ed273de9dd8b0a1215208aab5722c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920187"
---
# <a name="suggest-column-types-dialog-box-ui-reference"></a>Referência da interface do usuário da caixa de diálogo Sugerir Tipos de Coluna
  Use a caixa de diálogo **Sugerir Tipos de Coluna** para identificar o tipo de dados e o tamanho das colunas em um Gerenciador de Conexões de Arquivos Simples, com base em uma amostragem do conteúdo dos arquivos.  
  
 Para saber mais sobre os tipos de dados usados pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Tipos de dados do Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="options"></a>Opções  
 **Número de linhas**  
 Digite ou selecione o número de linhas na amostra que o algoritmo usa.  
  
 **Sugerir o menor tipo de dados inteiros**  
 Desmarque esta caixa de seleção para ignorar a avaliação. Se selecionada, determina o menor tipo de dados inteiro possível para colunas que contêm dados numéricos integrais.  
  
 **Sugerir o menor tipo de dados reais**  
 Desmarque esta caixa de seleção para ignorar a avaliação. Se selecionada, determina se as colunas que contêm dados numéricos reais podem usar o menor tipo de dados reais, DT_R4.  
  
 **Identificar colunas de Boolianos usando os seguintes valores**  
 Digite os dois valores que deseja usar como valores Boolianos verdadeiro e falso. Os valores devem ser separados por uma vírgula, com o primeiro valor representando Verdadeiro.  
  
 **Preencher colunas de cadeia de caracteres**  
 Marque esta caixa de seleção para habilitar o preenchimento da cadeia de caracteres.  
  
 **Porcentagem de enchimento**  
 Digite ou selecione a porcentagem pela qual aumentar o tamanho de coluna para tipos de dados de caracteres. A porcentagem deve ser um inteiro.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../integration-services-error-and-message-reference.md)   
 [Gerenciador de Conexões de Arquivos Simples](file-connection-manager.md)  
  
  
