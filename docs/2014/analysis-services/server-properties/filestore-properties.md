---
title: Propriedades do repositório de filestore | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Income property
- InitialBonus property
- PercentScanPerPrice property
- FileStore properties
- BackgroundTrimCost property
- Tax property
- PerformanceTrace property
- MinimumBalance property
- UnbufferedThreshold property
- BackgroundTrimAmount property
- MaximumBalance property
- MemoryLimitMin property
- MemoryLimit property
ms.assetid: 580cf0aa-7425-4d48-aa8d-128f5b488fcd
author: minewiskan
ms.author: owend
ms.openlocfilehash: db238092ac4c77e94961152808c7a7b6e76e9790
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940677"
---
# <a name="filestore-properties"></a>Propriedades FileStore
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor de armazenamento de arquivos listadas nas tabelas a seguir. Estas são todas as propriedades avançadas que não devem ser alteradas, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações sobre as propriedades de servidor adicionais e como defini-las, consulte [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** modo de servidor multidimensional e tabular  
  
## <a name="properties"></a>Propriedades  
 `MemoryLimit`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryLimitMin`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `PercentScanPerPrice`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `PerformanceTrace`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `RandomFileAccessMode`  
 Uma propriedade Booliana que indica se os arquivos de banco de dados e arquivos armazenados em cache são acessados em modo de acesso aleatório ao arquivo. Essa propriedade é desativada por padrão. Por padrão, o Analysis Services não define o sinalizador de acesso ao arquivo aleatório ao abrir arquivos de dados de partição para acesso de leitura.  
  
 Em sistemas avançados, especialmente os com recursos de memória grandes e vários nós NUMA, pode ser vantajoso usar acesso aleatório ao arquivo. No modo de acesso aleatório, o Windows ignora operações de mapeamento de página que leem dados do disco no cache de arquivo do sistema, diminuindo, portanto, a contenção no cache.  
  
 Você precisará executar testes de comparação para determinar se o desempenho da consulta melhorou como o resultado da alteração desta propriedade. Para conhecer as práticas recomendadas sobre como fazer testes de comparação, inclusive limpar o cache e evitar erros comuns, consulte [Guia de operações do SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539). Para obter informações adicionais sobre as compensações de usar essa propriedade, consulte [https://support.microsoft.com/kb/2549369](https://support.microsoft.com/kb/2549369) .  
  
 Para exibir ou modificar esta propriedade no Management Studio, habilite a lista de propriedades avançadas na página de propriedades do servidor. Você também pode alterar a propriedade no arquivo msmdsrv.ini. Reiniciar o servidor é recomendado depois de definir esta propriedade; caso contrário, os arquivos que já estão abertos continuarão sendo acessados no modo anterior.  
  
 `UnbufferedThreshold`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="memory-model-category"></a>Categoria de modelo de memória  
 `MemoryModel\Tax`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryModel\Income`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryModel\MaximumBalance`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryModel\MinimumBalance`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryModel\InitialBonus`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar propriedades do servidor no Analysis Services](server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
