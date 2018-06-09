---
title: Propriedades de recurso | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8ee5a58d5c04cbfbb1f47f0d073ba6614490970c
ms.sourcegitcommit: 6e55a0a7b7eb6d455006916bc63f93ed2218eae1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35238916"
---
# <a name="feature-properties"></a>Propriedades de recurso
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

  As propriedades do recurso pertencem aos recursos do produto, a maioria delas avançadas, incluindo propriedades que controlam vínculos entre instâncias do servidor.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades de servidor listadas na tabela a seguir. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** somente modo de servidor multidimensional  
  
## <a name="properties"></a>Propriedades  
  
|Propriedade|Padrão|Description|  
|--------------|-------------|-----------------|  
|**ManagedCodeEnabled**|1|Uma propriedade booliana que indica se procedimentos armazenados CLR estão habilitados.|  
|**LinkInsideInstanceEnabled**|1|Uma propriedade booliana que indica se um objeto vinculado pode ser criado dentro da mesma instância do servidor.|  
|**LinkToOtherInstanceEnabled**|0|Uma propriedade booliana que indica se objetos em servidores remotos podem ser vinculados.|  
|**LinkFromOtherInstanceEnabled**|0|Uma propriedade booliana que indica se objetos podem ser vinculados de outras instâncias do servidor.|  
|**ConnStringEncryptionEnabled**|1|Uma propriedade booliana que indica se a cadeia de caracteres de conexão está criptografada no arquivo de configuração de servidor.|  
|**UseCachedPageAllocators**|0|Uma propriedade booliana que indica se alocadores da página em cache estão habilitados.|  
|**ComUdfEnabled**|0|Uma propriedade booliana que indica se as funções definidas pelo usuário como objetos COM estão habilitadas.|  
|**SQMSupportEnabled**|1|Uma propriedade booliana que indica se os relatórios de erro e de uso de recursos são enviados automaticamente ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|  
|**ResourceMonitoringEnabled**|1|Uma propriedade booliana que indica se os contadores de monitoramento de recursos internos estão habilitados. Essa propriedade é ativada por padrão. Quando está habilitada, esta propriedade permite que os contadores coletem dados de uso sobre CPU, memória e atividade de E/S.<br /><br /> Os contadores de monitoramento de recursos internos são usados pelo DMV (Exibições de gerenciamento dinâmico) que relatam sobre a utilização do recurso. Se você desabilitar esta propriedade, as consultas do DMV ainda serão executadas, mas o conjunto de resultados será inválido. Os DMVs que dependem desta propriedade incluem o seguinte:<br /><br /> **DISCOVER_OBJECT_ACTIVITY**<br /><br /> **DISCOVER_COMMAND_OBJECTS**<br /><br /> **DISCOVER_SESSIONS** (para SESSION_READS, SESSION_WRITES, SESSION_CPU_TIME_MS)<br /><br /> <br /><br /> Observação: em um sistema de vários núcleos que usa arquitetura de NUMA, desabilitar esta propriedade pode melhorar o desempenho da consulta, particularmente para cargas de trabalho altas de vários usuários. Você precisará executar testes de comparação para determinar se o desempenho da consulta melhorou como o resultado da alteração desta propriedade. Para conhecer as práticas recomendadas sobre como fazer testes de comparação, inclusive limpar o cache e evitar erros comuns, consulte [Guia de operações do SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).|  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Usar DMVs &#40;Exibições de Gerenciamento Dinâmico&#41; para monitorar o Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
