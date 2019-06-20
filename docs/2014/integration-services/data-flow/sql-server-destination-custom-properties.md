---
title: Propriedades personalizadas de destino do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b736aa6d-c154-44a0-be08-f25733fca1d9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 202fd03beea5ec2fbf4b3fc29978ba9e112010df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900830"
---
# <a name="sql-server-destination-custom-properties"></a>Propriedades personalizadas do destino SQL Server
  O destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|AlwaysUseDefaultCodePage|Booliano|Força o uso do valor da propriedade DefaultCodePage. O valor padrão dessa propriedade é `False`.|  
|BulkInsertCheckConstraints|Booliano|Um valor que especifica se a inserção em massa verifica restrições. O valor padrão dessa propriedade é `True`.|  
|BulkInsertFireTriggers|Booliano|Um valor que especifica se a inserção em massa aciona gatilhos em tabelas. O valor padrão dessa propriedade é `False`.|  
|BulkInsertFirstRow|Integer|Um valor que especifica a primeira linha a ser inserida. O valor padrão dessa propriedade é **-1**, que indica que nenhum valor foi atribuído|  
|BulkInsertKeepIdentity|Booliano|Um valor que especifica se podem ser inseridos valores em colunas de identidade. O valor padrão dessa propriedade é `False`.|  
|BulkInsertKeepNulls|Booliano|Um valor que especifica se a inserção em massa mantém valores Nulos. O valor padrão dessa propriedade é `False`.|  
|BulkInsertLastRow|Integer|Um valor que especifica a última linha a ser inserida. O valor padrão dessa propriedade é **-1**, que indica que nenhum valor foi atribuído.|  
|BulkInsertMaxErrors|Integer|Um valor que especifica o número de erros que podem ocorrer antes que a inserção em massa seja interrompida. O valor padrão dessa propriedade é **-1**, que indica que nenhum valor foi atribuído.|  
|BulkInsertOrder|Cadeia de caracteres|Os nomes das colunas de classificação. Cada coluna pode ser classificada em ordem crescente ou decrescente. Se forem usadas várias colunas de classificação, os nomes de coluna serão separados por vírgulas.|  
|BulkInsertTableName|Cadeia de caracteres|A tabela ou exibição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados para o qual os dados são copiados.|  
|BulkInsertTablock|Booliano|Um valor que especifica se a tabela é bloqueada durante a inserção em massa. O valor padrão dessa propriedade é `True`.|  
|DefaultCodePage|Integer|A página de código a ser usada quando informações de página de código não estão disponíveis na fonte de dados.|  
|MaxInsertCommitSize|Integer|Um valor que especifica o número máximo de linhas a serem inseridas em um lote. Quando o valor é zero, todas as linhas são inseridas em um único lote.|  
|Tempo Limite|Integer|Um valor que especifica a duração em segundos da espera do destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] até a conclusão, se não houver dados disponíveis para inserção. O valor 0 significa que não há tempo limite para o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O valor padrão dessa propriedade é 30.|  
  
 A entrada e as colunas de entrada do destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino do SQL Server](sql-server-destination.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades comuns](../common-properties.md)  
  
  
