---
title: Salvar rastreamentos e modelos de rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- exporting trace templates
- importing trace templates
- SQL Server Profiler, templates
ms.assetid: 957e6bf8-e7a3-4a59-a1cd-0a41538a8158
author: stevestein
ms.author: sstein
ms.openlocfilehash: 36db7ccfd8b185d60eb39c20a58842f469e7878d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048308"
---
# <a name="save-traces-and-trace-templates"></a>Salvar rastreamentos e modelos de rastreamento
  É importante distinguir entre salvar arquivos de rastreamento e salvar modelos de rastreamento. Salvar um arquivo de rastreamento envolve salvar, em um local especificado, os dados de evento capturados. Salvar um modelo de rastreamento envolve salvar a definição do rastreamento, como as colunas de dados, as classes de evento ou os filtros especificados.  
  
## <a name="saving-traces"></a>salvando rastreamentos  
 Salve os dados de evento capturados em um arquivo ou tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando for preciso analisá-los ou reproduzi-los mais tarde. Use um arquivo de rastreamento para fazer o seguinte:  
  
-   Usar um arquivo ou tabela de rastreamento para criar uma carga de trabalho utilizada como entrada no Orientador de Otimização do Mecanismo de Banco de Dados.  
  
-   Usar um arquivo de rastreamento para capturar eventos e enviar o arquivo de rastreamento ao provedor de suporte para análise.  
  
-   Usar as ferramentas de processamento de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acessar ou exibir os dados no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Apenas membros da função de servidor fixa **sysadmin** ou o criador da tabela podem acessar a tabela de rastreamento diretamente.  
  
> [!NOTE]  
>  Capturar dados de rastreamento em uma tabela é uma operação mais demorada do que capturá-los em um arquivo. Uma alternativa é capturar os dados de rastreamento em um arquivo, abrir o arquivo e salvar o rastreamento como tabela de rastreamento.  
  
 Quando é usado um arquivo de rastreamento, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] salva os dados de evento capturados (e não as definições de rastreamento) em um arquivo de Rastreamento do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (\*.trc). A extensão é adicionada automaticamente ao final do arquivo quando o arquivo de rastreamento é salvo, independentemente de qualquer outra extensão especificada. Por exemplo, se você especificar um arquivo de rastreamento chamado **Trace.dat**, o arquivo criado será denominado **Trace.dat.trc**.  
  
> [!IMPORTANT]  
>  Os usuários que tiverem a permissão SHOWPLAN, ALTER TRACE ou VIEW SERVER STATE poderão exibir consultas capturadas na saída do Plano de Execução. Essas consultas podem conter informações confidenciais, como senhas. Portanto, é recomendável que você somente conceda essas permissões a usuários autorizados a exibir informações confidenciais, como membros da função de banco de dados fixa **db_owner** ou membros da função de servidor fixa **sysadmin** . Além disso, também é recomendável somente salvar arquivos do Plano de Execução ou arquivos de rastreamento que contenham eventos relacionados ao Plano de Execução em um local que use o sistema de arquivos NTFS e restringir o acesso a usuários autorizados a exibir informações confidenciais.  
  
## <a name="saving-templates"></a>Salvando modelos  
 A definição de modelo de um rastreamento inclui as classes de evento, as colunas de dados, os filtros e todas as outras propriedades (menos os dados de evento capturados) que são usadas para criar um rastreamento. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] fornece modelos de sistema predefinidos para tarefas comuns de rastreamento e para tarefas específicas, como criar uma carga de trabalho que o Orientador de Otimização do Mecanismo de Banco de Dados pode usar para ajustar o design de banco de dados físico. Também é possível criar e salvar modelos definidos pelo usuário.  
  
### <a name="importing-and-exporting-templates"></a>Importando e exportando modelos  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] permite importar e exportar modelos de um servidor para outro. A exportação de um modelo é a migração de uma cópia de um modelo existente para um diretório especificado. A importação de um modelo é a criação de uma cópia de um modelo especificado. Quando esses modelos são exibidos no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], é possível distingui-los dos modelos do sistema, devido ao termo "(user)" que acompanha seu nome. Não é possível substituir ou modificar diretamente um modelo do sistema predefinido.  
  
### <a name="analyzing-performance-with-templates"></a>Analisando o desempenho com modelos  
 Se você monitorar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]com frequência, use modelos para analisar o desempenho. Os modelos capturam sempre os mesmos dados de eventos e usam a mesma definição de rastreamento para monitorar os mesmos eventos. Você não precisa definir as classes de evento e colunas de dados toda vez que cria um rastreamento. Além disso, um modelo pode ser passado a outro usuário para o monitoramento de eventos específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, um provedor de suporte pode fornecer um modelo a um cliente. O cliente usa o modelo para capturar os dados de evento necessários e, então, envia-os ao provedor de suporte para análise.  
  
 **Para salvar um rastreamento em um arquivo**  
  
 [Salvar resultados de rastreamento em um arquivo &#40;SQL Server Profiler&#41;](save-trace-results-to-a-file-sql-server-profiler.md)  
  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)  
  
## <a name="see-also"></a>Consulte Também  
 [Salvar resultados de rastreamento em uma tabela &#40;SQL Server Profiler&#41;](save-trace-results-to-a-table-sql-server-profiler.md)   
 [Criar um modelo de rastreamento &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)   
 [Derivar um modelo de um rastreamento em execução &#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [Derivar um modelo de um arquivo ou de uma tabela de rastreamento &#40;SQL Server Profiler&#41;](derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [Exportar um modelo de rastreamento &#40;SQL Server Profiler&#41;](export-a-trace-template-sql-server-profiler.md)   
 [Importar um modelo de rastreamento &#40;SQL Server Profiler&#41;](import-a-trace-template-sql-server-profiler.md)  
  
  
