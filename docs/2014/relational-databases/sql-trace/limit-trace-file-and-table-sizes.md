---
title: Limitar o tamanho de tabelas e arquivos de rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- maximum file size for traces
- traces [SQL Server], file size
- size [SQL Server], tables
- file rollover option [SQL Server]
- size [SQL Server], files
ms.assetid: 88c31b02-f44c-4a14-be8b-437f2097de12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 59e6a79d868e4bfa0ec0af7190d54a8bc13bf395
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63136457"
---
# <a name="limit-trace-file-and-table-sizes"></a>Limitar o tamanho de arquivos e tabelas de rastreamento
  Os resultados do Rastreamento do SQL variam em tamanho, dependendo das classes de evento incluídas e da forma com que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] é usado. Se você rastreia classes de evento que ocorrem com frequência, é possível minimizar a quantidade de dados coletados pelo rastreamento definindo o tamanho máximo de arquivo ou o número máximo de linhas. Especificando o tamanho máximo de arquivo ou de linhas, garante-se que o arquivo ou tabela de rastreamento não ultrapassem esse limite.  
  
> [!NOTE]  
>  Se os dados do rastreamento forem salvos em um arquivo que já existe, é possível adicionar dados ao arquivo ou substituir os que ele contém. Se optar por acrescentar os dados ao arquivo e o arquivo de rastreamento atingir ou exceder o tamanho máximo especificado, você será notificado e terá a oportunidade de aumentar o tamanho máximo de arquivo ou especificar um novo arquivo. O mesmo vale para tabelas de rastreamento.  
  
## <a name="maximum-file-size"></a>Tamanho máximo de arquivo  
 Um rastreamento que possua tamanho máximo de arquivo parará de salvar informações no arquivo assim que esse tamanho for alcançado. Esta opção permite-lhe agrupar eventos em arquivos menores e mais fáceis de gerenciar. Além disso, limitar o tamanho do arquivo torna mais segura a execução de rastreamentos autônomos, pois o rastreamento é interrompido quando o tamanho máximo de arquivo é alcançado. Você pode definir o tamanho máximo de arquivos para rastreamentos criados por meio de procedimentos armazenados Transact-SQL ou usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 Há um limite de 1 gigabyte (GB) para a opção de tamanho máximo de arquivo. O tamanho máximo de arquivo padrão é de 5 megabytes (MB).  
  
### <a name="enabling-file-rollover"></a>Habilitando a substituição de arquivo  
 A opção de substituição de arquivo faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] feche o arquivo atual e crie um novo arquivo quando o tamanho máximo é atingido. O novo arquivo tem o mesmo nome do anterior mais um número inteiro, que é adicionado ao nome para indicar a sequência. Por exemplo, se o arquivo de rastreamento original for nomeado nomedoarquivo_1.trc, o próximo arquivo de rastreamento será nomedoarquivo_2.trc, e assim por diante. Se o nome atribuído a um novo arquivo de substituição já estiver sendo usado por um arquivo existente, este último será substituído, exceto se for somente leitura. A opção de substituição de arquivo é habilitada por padrão quando você salva dados de rastreamento em um arquivo.  
  
> [!NOTE]  
>  Com a opção de substituição de arquivo ativada, o rastreamento continua até que seja interrompido de alguma outra maneira. Para interromper o rastreamento quando o limite de tamanho de arquivo for atingido, desabilite a opção de substituição de arquivo.  
  
 **Para definir um tamanho máximo para um arquivo de rastreamento**  
  
 [Definir um tamanho máximo para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
## <a name="maximum-number-of-rows"></a>Número máximo de linhas  
 Um rastreamento que possui um número máximo de linhas para de salvar informações na tabela assim que esse número é atingido. Cada evento constitui uma linha; logo, este parâmetro define um limite para o número de eventos coletados. Definir o número máximo de linhas facilita a execução de rastreamentos autônomos. Por exemplo, se for preciso iniciar um rastreamento que salva dados em uma tabela, mas você desejar interrompê-lo se a tabela se tornar grande demais, isso pode ser feito automaticamente.  
  
 Quando for especificado um número máximo de linhas e esse número for atingido, o rastreamento continuará a ser executado enquanto o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] estiver em execução, mas as informações deixarão de ser registradas. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] continuará a exibir os resultados do rastreamento até que este seja interrompido.  
  
 **Para definir um número máximo de linhas para um rastreamento**  
  
 [Definir um tamanho máximo para uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)  
  
  
