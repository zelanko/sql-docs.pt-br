---
title: "Processando os dados manualmente (SSAS tabular) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.datarefreshprogressdb.f1"
ms.assetid: 0918c04c-c1e6-45b4-acfa-96fa578e684b
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 18
---
# Processando os dados manualmente (SSAS tabular)
  Este tópico descreve como processar manualmente dados de espaço de trabalho no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Ao criar um modelo de tabela que usa dados externos, é possível atualizar os dados manualmente usando o comando Processar. Você pode processar uma única tabela, todas as tabelas no modelo ou uma ou mais partições. Sempre que os dados são processados, também pode ser necessário recalculá-los.  Processar os dados significa obter os dados mais recentes de fontes externas. Recalcular significa atualizar o resultado de qualquer fórmula que usa os dados.  
  
 Seções neste tópico:  
  
-   [Processando os dados manualmente](#bkmk_mahually_process)  
  
-   [Progresso do Processo de Dados](#bkmk_data_process_progress)  
  
##  <a name="bkmk_mahually_process"></a> Processando os dados manualmente  
  
#### Para processar dados de uma única tabela ou de todas as tabelas em um modelo  
  
1.  No designer de modelos, clique na tabela que você quer processar.  
  
2.  Clique no menu **Modelo** , clique em **Processar**e clique em **Processar** ou **Processar Tudo**.  
  
#### Para processar dados para todas as tabelas usando a mesma conexão  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Conexões Existentes**.  
  
2.  Na caixa de diálogo **Conexões Existentes** , selecione uma conexão, e clique em **Processar**.  
  
#### Para processar dados para uma ou mais partições  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** , aponte para **Processar**e em **Processar Partições**.  
  
2.  Na caixa de diálogo **Processar Partições** , em **Modo**, selecione um dos modos de processo a seguir:  
  
    |Modo|Description|  
    |----------|-----------------|  
    |**Processar Padrão**|Detecta o estado de processamento de um objeto de partição e realiza o processamento necessário para passar os objetos de partição não processados ou parcialmente processados para um estado completamente processado. Os dados para tabelas vazias e partições são carregados; hierarquias, colunas calculadas e relações são criadas ou recriadas.|  
    |**Processar Completo**|Processa um objeto de partição e todos os objetos que ele contém. Quando o comando Processar Completo for executado para um objeto que já foi processado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] removerá todos os dados do objeto e processará o objeto. Esse tipo de processamento é necessário quando uma alteração estrutural é feita em um objeto.|  
    |**Processar Dados**|Carregue os dados em uma partição ou uma tabela sem recriar hierarquias ou relações ou recalcular colunas calculadas e medidas.|  
    |**Processar Limpeza**|Remove todos os dados de uma partição.|  
    |**Processar adição**|Atualize a partição incrementalmente com novos dados.|  
  
3.  Na lista de partições, selecione as partições que você deseja processar e clique em **OK**.  
  
##  <a name="bkmk_data_process_progress"></a> Progresso do Processo de Dados  
 A caixa de diálogo **Progresso do Processo de Dados** o habilita a monitorar o processamento de dados que você importou de uma fonte externa para o modelo. Para acessar essa caixa de diálogo, clique no menu **Modelo** , clique em **Processar Partições**, em **Processar Tabela** ou **Processar Tudo**.  
  
 **Status**  
 Indica se a operação de processo foi bem-sucedida ou não.  
  
 **Detalhes**  
 Lista as tabelas e as exibições que foram importadas, o número de linhas que foram importadas e fornece um link para um relatório de qualquer problema.  
  
 **Parar Atualização**  
 Clique para interromper a operação de processo. Essa opção será útil se a operação estiver demorando muito ou se houver muitos erros.  
  
## Consulte também  
 [Processar dados &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/process-data-ssas-tabular.md)   
 [Solucionar problemas de dados de processo &#40;SSAS tabular&#41;](../../analysis-services/troubleshoot-process-data-ssas-tabular.md)  
  
  