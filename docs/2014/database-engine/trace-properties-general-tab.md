---
title: Propriedades do rastreamento (guia geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.traceproperties.general.f1
helpviewer_keywords:
- Trace Properties dialog box
ms.assetid: 25227268-143b-477e-aac9-8268bcaf2078
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 573c8d13b9a7431c33d8c3b104712a2bf31b3fbf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089529"
---
# <a name="trace-properties-general-tab"></a>Propriedades do Rastreamento (guia Geral)
  Use a guia **Geral** da caixa de diálogo **Propriedades do Rastreamento** para exibir ou especificar propriedades de um rastreamento.  
  
## <a name="options"></a>Opções  
 **Nome do rastreamento**  
 Especifique o nome do rastreamento.  
  
 **Nome do provedor de rastreamento**  
 Exibe o nome da instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que será rastreada. Esse campo é populado automaticamente com o nome do servidor que você especificou ao se conectar. Para alterar o nome do provedor de rastreamento, clique em **Cancelar** para fechar a caixa de diálogo e iniciar um novo rastreamento.  
  
 **Tipo de provedor de rastreamento**  
 Exibe o tipo de servidor que está fornecendo o rastreamento. O arquivo de definição de rastreamento popula o campo **Tipo de provedor de rastreamento** automaticamente. Não é possível modificar esse campo.  
  
 **Versão**  
 Exibe a versão do servidor que está fornecendo o rastreamento. O arquivo de definição de rastreamento popula o campo **Versão** automaticamente. Não é possível modificar esse campo.  
  
 **Usar o modelo**  
 Selecione um modelo do diretório modelo. O diretório é populado com os modelos padrões e qualquer modelo definido pelo usuário, criados para o tipo de provedor de rastreamento atual.  
  
 **Salvar no arquivo**  
 Capture os dados de rastreamento para um arquivo .trc. Salvar dados de rastreamento é útil para revisão e análise posteriores.  
  
 **Definir tamanho máximo do arquivo (MB)**  
 Se você optar por salvar os dados de rastreamento em um arquivo, especifique o tamanho máximo do arquivo de rastreamento. O padrão é 5 MB (megabytes). O tamanho máximo é limitado somente pelo sistema de arquivos (NTFS, FAT) onde o arquivo é salvo.  
  
 \<Gráfico> **salvar como**  
 Depois de selecionar para salvar, é possível selecionar esse ícone para alterar o nome de arquivo.  
  
 **Habilitar substituição de arquivo**  
 Selecione para habilitar a criação de arquivos adicionais para aceitar os dados de rastreamento, quando o tamanho máximo de arquivo for atingido. Cada nome de arquivo novo consiste do nome de arquivo .trc original, numerado em sequência. Por exemplo, ao alcançar o tamanho máximo do arquivo, **NewTrace.trc** é fechado e um novo arquivo **NewTrace_1.trc**é aberto, seguido de **NewTrace_2.trc**e assim por diante. A substituição de arquivos é habilitada por padrão quando você salvar um rastreamento em um arquivo.  
  
 **Dados de rastreamento de processos do servidor**  
 Especifique que o servidor que executa o rastreamento deve processar os dados de rastreamento. Usando essa opção a sobrecarga de desempenho devido ao rastreamento é reduzida. Se selecionada, nenhum evento é ignorado mesmo sob condições de tensão. Se essa caixa de seleção for desmarcada, o processamento será executado pelo SQL Server Profiler, e há uma possibilidade de que alguns eventos não sejam rastreados sob condições de tensão.  
  
 **Salvar na tabela**  
 Capture os dados de rastreamento para uma tabela de banco de dados. Salvar dados de rastreamento é útil para revisão e análise posteriores. Entretanto, ao salvar dados de rastreamento para uma tabela isso pode levar a uma sobrecarga significativa no servidor no qual o rastreamento está sendo salvo. Se possível, não salve a tabela de rastreamento no mesmo servidor que está sendo rastreado.  
  
 \<Tabela de **destino** do gráfico>  
 Depois de selecionar para salvar os dados de rastreamento para uma tabela de banco de dados, é possível selecionar esse ícone para alterar o nome da tabela.  
  
 **Definir máximo de linhas (em milhares)**  
 Especifique o número maior de linhas nas quais salvar dados. O padrão é 1000 linhas.  
  
 **Habilitar hora de parada do rastreamento**  
 Defina a data e hora para o rastreamento ser concluído e se fechar.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um rastreamento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
