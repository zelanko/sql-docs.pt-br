---
title: Contadores de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], performance counters
- performance counters [Integration Services]
- data flow [Integration Services], performance
- counters [Integration Services]
- data flow engine [Integration Services]
ms.assetid: 11e17f4e-72ed-44d7-a71d-a68937a78e4c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b20ac056894066114883153030943bec1c05963
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423293"
---
# <a name="performance-counters"></a>Contadores de desempenho
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala um conjunto de contadores de desempenho que podem ser usados para monitorar o desempenho do mecanismo de fluxo de dados. Por exemplo, é possível observar o contador "Buffers em spool" para determinar se os buffers de dados estão sendo gravados temporariamente no disco durante a execução de um pacote. Essa troca reduz o desempenho e indica que o computador não tem memória suficiente.  
  
> [!NOTE]  
>  se você instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador que está executando o [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]e atualizar o computador para o [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)], o processo de atualização removerá os contadores de desempenho do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] do computador. Para restaurar os contadores de desempenho do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no computador, execute a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de reparo.  
  
 A tabela a seguir descreve os contadores de desempenho.  
  
|Contador de desempenho|Descrição|  
|-------------------------|-----------------|  
|Bytes de BLOB lidos|O número de bytes dos dados de BLOB (objetos binários grandes) que o mecanismo de fluxo de dados leu em todas as fontes.|  
|Bytes de BLOB gravados|O número de bytes de dados de BLOB que o mecanismo de fluxo de dados gravou em todos os destinos.|  
|Arquivos de BLOB em uso|O número de arquivos de BLOB que o mecanismo de fluxo de dados está usando atualmente para o spool.|  
|Memória de buffer|A quantidade de memória que está em uso. Isto pode incluir memória física e virtual. Quando esse número é maior que a quantidade de memória física, a contagem de **Buffers em spool** aumenta como uma indicação de que a troca de memória está aumentando. O aumento da troca de memória reduz a velocidade do desempenho do mecanismo de fluxo de dados.|  
|Buffers em uso|O número de objetos de buffer, de todos os tipos, que todos os componentes de fluxo de dados e do mecanismo de fluxo de dados estão usando atualmente.|  
|Buffers em spool|O número de buffers gravados atualmente no disco. Se o mecanismo do fluxo de dados ficar com pouca memória física, os buffers que não estão em uso no momento são gravados no disco e depois recarregados quando necessário.|  
|Memória de buffer simples|A quantidade total de memória, em bytes que todos os buffers simples utilizam. Buffers simples são blocos de memória que um componente usa para armazenar dados. Um buffer simples é um grande bloco de bytes que é acessado, byte por byte.|  
|Buffers simples em uso|O número de buffers simples que o mecanismo de fluxo de dados usa. Todos os buffers simples são buffers privados.|  
|Memória de buffer privada|A quantidade total de memória em uso por todos os buffers privados. Um buffer não será privado se o mecanismo de fluxo de dados o criar para oferecer suporte ao fluxo de dados. Um buffer privado é um buffer que uma transformação usa apenas para trabalho temporário. Por exemplo, a transformação Agregação usa buffers privados para fazer seu trabalho.|  
|Buffers privados em uso|O número de buffers que as transformações usam.|  
|Linhas lidas|O número de linhas que uma fonte produz. O número não inclui linhas de tabelas de referência lidas pela transformação Pesquisa.|  
|Linhas gravadas|O número de linhas oferecido a um destino. O número não reflete linhas gravadas no armazenamento de dados de destino.|  
  
 Você usa o snap-in do MMC (Microsoft Management Console) de Desempenho para criar um log que capture contadores de desempenho.  
  
 Para obter informações sobre como melhorar o desempenho, consulte [Recursos de desempenho de fluxo de dados](../data-flow/data-flow-performance-features.md).  
  
## <a name="obtain-performance-counter-statistics"></a>Obter a estatística do contador de desempenho  
 Para projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode obter a estatística do contador de desempenho usando a função [dm_execution_performance_counters &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/functions-dm-execution-performance-counters).  
  
 No exemplo a seguir, a função retorna a estatística para uma execução com ID 34.  
  
```  
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
 No exemplo a seguir, a função retorna a estatística de todas as execuções realizadas no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
```  
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
> [!IMPORTANT]  
>  Se você for membro da função de banco de dados `ssis_admin`, as estatísticas de desempenho de todas as execuções em andamento serão retornadas.  Se você não for membro da função de banco de dados `ssis_admin`, as estatísticas de desempenho das execuções em andamento para as quais você tem permissões de leitura serão retornadas.  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Ferramenta, [SSIS Performance Visualization for Business Intelligence Development Studio (projeto CodePlex)](https://go.microsoft.com/fwlink/?LinkId=146626), em codeplex.com.  
  
-   Vídeo, [Measuring and Understanding the Performance of Your SSIS Packages in the Enterprise (vídeo do SQL Server)](https://go.microsoft.com/fwlink/?LinkId=150497)(Medindo e compreendendo o desempenho de seus pacotes do SSIS na empresa), em msdn.microsoft.com.  
  
-   Artigo de suporte, [The SSIS performance counter is no longer available in the Performance Monitor after you upgrade to Windows Server 2008](https://go.microsoft.com/fwlink/?LinkId=235319), em support.microsoft.com.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de projetos e pacotes](../packages/run-integration-services-ssis-packages.md)  
  
  
