---
title: Notificações (caixa de diálogo de opções de armazenamento) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.notifications.f1
ms.assetid: 5675cdbf-bfaa-4b6e-b716-31b8e9da72b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f6ba7fd0995066b90ef984f8dfa436864e06db95
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193696"
---
# <a name="notifications-storage-options-dialog-box-analysis-services---multidimensional-data"></a>Notificações (caixa de diálogo Opções de Armazenamento) (Analysis Services - Dados Multidimensionais)
  Use a guia **Notificações** da caixa de diálogo **Opções de Armazenamento** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir o método de notificação e as configurações relacionadas para uma dimensão, cubo, grupo de medidas ou partição.  
  
> [!NOTE]  
>  Você deve estar familiarizado com a funcionalidade de modo de armazenamento e de cache pró-ativo para modificar essas configurações. Para obter mais informações, consulte [Cache pró-ativo &#40;Partições&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Modo de armazenamento**|Seleciona o modo de armazenamento a ser usado para o objeto.<br /><br /> **MOLAP**<br /> O objeto usa armazenamento MOLAP (OLAP multidimensional).<br /><br /> **HOLAP**<br /> O objeto usa armazenamento HOLAP (OLAP híbrido).<br /><br /> **ROLAP**<br /> O objeto usa armazenamento ROLAP (OLAP relacional).|  
|**Habilitar cache pró-ativo**|Habilita o cache pró-ativo.<br /><br /> Observação: se essa opção não estiver selecionada, todas as opções, exceto **Modo de armazenamento** , estarão desabilitadas.|  
|**SQL Server**|Usa um mecanismo de rastreamento especializado no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para identificar alterações nas tabelas subjacentes do objeto.|  
|**Especificar tabelas de acompanhamento**|Especifique as tabelas subjacentes a serem controladas para o objeto e, em seguida, digite uma lista de tabelas delimitadas por ponto e vírgula (;) ou clique no botão de reticências (**...**) para abrir a caixa de diálogo **Objetos Relacionais** e escolha as tabelas a serem controladas. Para obter mais informações, consulte [Caixa de diálogo Objetos Relacionais &#40;Analysis Services – Dados Multidimensionais&#41;](relational-objects-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Se essa opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tentará determinar a lista de tabelas subjacentes a serem controladas para o objeto, se determinados requisitos forem atendidos. Para obter mais informações sobre esses requisitos, consulte [Cache proativo &#40;Partições&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).|  
|**Cliente iniciado**|Selecione para usar o XML para o comando Analysis (XMLA), `NotifyTableChange`, para identificar alterações nas tabelas subjacentes do objeto. Essa opção será selecionada normalmente se você planejar usar um processo de notificação baseado em cliente.|  
|**Especificar tabelas de acompanhamento**|Selecione para especificar que as tabelas subjacentes a serem controladas para o objeto e, em seguida, digite uma lista de tabelas delimitadas por ponto e vírgula (;) ou clique no botão de reticências (**...**) para abrir a caixa de diálogo **Objetos Relacionais** e escolha as tabelas a serem controladas. Para obter mais informações, consulte [Caixa de diálogo Objetos Relacionais &#40;Analysis Services – Dados Multidimensionais&#41;](relational-objects-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Se essa opção não estiver selecionada, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tentará determinar a lista de tabelas subjacentes a serem controladas para o objeto, se determinados requisitos forem atendidos. Para obter mais informações sobre esses requisitos, consulte [Cache proativo &#40;Partições&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).|  
|**Sondagem agendada**|Usa um mecanismo de sondagem para identificar alterações executando uma série de consultas nas tabelas subjacentes do objeto.|  
|**Intervalo de sondagem**|Especifica o intervalo e as unidades de tempo do período que deve decorrer antes que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] execute as consultas sondagem e consultas de processamento definidas na grade de sondagem.|  
|**Habilitar atualizações incrementais**|Atualiza de maneira incremental o cache MOLAP para um objeto com base em um conjunto de consultas sondagem e de processamento com o objetivo de identificar apenas dados adicionais. Se esta opção for selecionada, a consulta sondagem será associada a um identificador de tabela na exibição da fonte de dados. Em seguida, a consulta de processamento será usada para comparar o valor atual com o valor armazenado da consulta sondagem executada anteriormente para identificar alterações.<br /><br /> Se essa opção não estiver selecionada, o cache MOLAP será completamente atualizado. A consulta sondagem é usada para identificar se a alteração ocorreu e nenhuma consulta de processamento ou identificador de tabela é necessário.|  
|**Grade de sondagem**|Contém as consultas sondagem, consultas de processamento e identificadores de tabela usados pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para sondar a fonte de dados e identificar alterações nas tabelas subjacentes do objeto. A grade contém as seguintes colunas:<br /><br /> **Consulta sondagem**: digite a consulta singleton executada no intervalo de sondagem para identificar alterações para o objeto ou clique no botão de reticências (**...** ) para abrir o **criar consulta sondagem** caixa de diálogo caixa e definir a consulta singleton. Para obter mais informações, consulte [Caixa de diálogo Criar Consulta Sondagem &#40;Analysis Services – Dados Multidimensionais&#41;](create-polling-query-dialog-box-analysis-services-multidimensional-data.md). Se **Habilitar atualizações incrementais** estiver selecionada, a consulta de sondagem deverá retornar um valor que identifica o último registro adicionado à tabela identificada em **Tabela**. Se **Habilitar atualizações incrementais** não estiver selecionada, a consulta de sondagem deverá retornar um valor que identifica o número de registros atual na tabela.<br /><br /> **Consulta de processamento**: digite a consulta executada no intervalo de sondagem para recuperar novos registros da tabela identificada em **tabela**, ou clique no botão de reticências (**...** ) para abrir o **criar consulta de processamento** caixa de diálogo caixa e definir a consulta. Para obter mais informações, consulte [Caixa de diálogo Criar Consulta de Processamento &#40;Analysis Services – Dados Multidimensionais&#41;](create-processing-query-dialog-box-analysis-services-multidimensional-data.md). A consulta deve ser parametrizada para aceitar dois parâmetros, o valor anterior retornado pela consulta em **Consulta sondagem** e o valor retornado pela consulta em **Consulta sondagem**, que pode ser usada para identificar e extrair apenas os registros que foram adicionados durante o período de sondagem. Observe que essa opção será habilitada somente se **Habilitar atualizações incrementais** estiver selecionada.<br /><br /> **Tabela**: digite o identificador da tabela para a qual a consulta no **consulta sondagem** controla o último registro ou clique no botão de reticências (**...** ) para abrir o **localizar tabela** caixa de diálogo e selecione a tabela. Para obter mais informações, consulte a [Caixa de diálogo Localizar Tabela &#40;Analysis Services – dados multidimensionais&#41;](find-table-dialog-box-analysis-services-multidimensional-data.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de opções de armazenamento &#40;Analysis Services - dados multidimensionais&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)  
  
  
