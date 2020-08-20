---
description: Propriedades personalizadas do destino Treinamento do Modelo de Mineração de Dados
title: Propriedades personalizadas do destino do treinamento do modelo de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f0a70216-fdac-44ae-af29-35f65626217c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6427b808d31c9b1938b093da2bdf14d59bec90cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457358"
---
# <a name="data-mining-model-training-destination-custom-properties"></a>Propriedades personalizadas do destino Treinamento do Modelo de Mineração de Dados

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O destino Treinamento do Modelo de Mineração de Dados tem propriedades personalizadas e as propriedades comum a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Treinamento do Modelo de Mineração de Dados. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|O identificador exclusivo do gerenciador de conexões.|  
|ASConnectionString|String|A cadeia de caracteres de conexão com uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou com um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|ObjectRef|String|Uma marca XML que identifica a estrutura de mineração de dados usada pela transformação.|  
  
 A entrada e as colunas de entrada do destino Treinamento do Modelo de Mineração de Dados não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino de treinamento do modelo de Data Mining](../../integration-services/data-flow/data-mining-model-training-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
