---
title: Exibir e analisar rastreamentos com o SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], viewing traces
- SQL Server Profiler, viewing traces
- traces [SQL Server], viewing
- SQL Server Profiler, troubleshooting
- troubleshooting [SQL Server], traces
- events [SQL Server], finding inside trace
- Profiler [SQL Server Profiler], troubleshooting
- traces [SQL Server], events
ms.assetid: 17e821ca-a12e-4192-acc1-96765d9ae266
author: stevestein
ms.author: sstein
ms.openlocfilehash: b3e848fe9a07d838631eef1737c2a7679b67e649
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040019"
---
# <a name="view-and-analyze-traces-with-sql-server-profiler"></a>Exibir e analisar rastreamentos com o SQL Server Profiler
  Use [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para exibir dados de evento capturados em um rastreamento. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibe dados com base em propriedades de rastreamento definidas. Um modo de analisar os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é copiá-los para outro programa, como o Orientador de Otimização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . [!INCLUDE[ssDE](../../includes/ssde-md.md)] O Orientador de Otimização poderá usar um arquivo de rastreamento contendo um lote SQL e eventos de RPC (chamada de procedimento remoto) se a coluna de dados **Text** estiver incluída no rastreamento. Para certificar-se de que os eventos e colunas corretos são capturados para uso com o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , use o modelo Ajuste predefinido, que é fornecido com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 Ao abrir um rastreamento por meio do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], o arquivo de rastreamento não precisa ter a extensão de arquivo .trc, caso tenha sido criado pelo [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ou por procedimentos armazenados do sistema do Rastreamento do SQL.  
  
> [!NOTE]  
>  O [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] também pode ler arquivos .log do Rastreamento do SQL e arquivos de script SQL genéricos. Ao abrir um arquivo .log do Rastreamento do SQL cuja extensão de arquivo não seja .log, como trace.txt, especifique **SQLTrace_Log** como formato de arquivo.  
  
 Você pode configurar o formato de exibição de data e hora do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] como auxílio para a análise do rastreamento.  
  
## <a name="troubleshooting-data"></a>Solucionando problemas de dados  
 Por meio do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], é possível solucionar problemas de dados agrupando rastreamentos ou arquivos de rastreamento pelas colunas de dados **Duration**, **CPU**, **Reads**ou **Writes** . Exemplos de dados cujos problemas podem ser solucionados são consultas com baixo desempenho ou com números excepcionalmente altos de operações lógicas de leitura.  
  
 Informações adicional podem ser encontradas salvando-se os rastreamentos em tabelas e usando [!INCLUDE[tsql](../../includes/tsql-md.md)] para consultar os dados de eventos. Por exemplo, para determinar quais eventos **SQL:BatchCompleted** tiveram um tempo de espera excessivo, execute o seguinte:  
  
```  
SELECT  TextData, Duration, CPU  
FROM    trace_table_name  
WHERE   EventClass = 12 -- SQL:BatchCompleted events  
AND     CPU < (Duration * 1000)  
```  
  
> [!NOTE]  
>  O servidor relata a duração de um evento em microssegundos (um milionésimo de segundo ou 10<sup>-6</sup>segundo) e o tempo de CPU usado pelo evento em milissegundos (um milésimo de segundo ou 10<sup>-3</sup>segundo). A interface gráfica do usuário do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibe a coluna **Duration** em milissegundos, por padrão; porém, quando um rastreamento é salvo em um arquivo ou tabela de banco de dados, o valor da coluna **Duration** é gravado em microssegundos.  
  
## <a name="displaying-object-names-when-viewing-traces"></a>Exibindo nomes de objeto ao visualizar rastreamentos  
 Se desejar exibir o nome de um objeto, em vez de seu identificador (**Object ID**), capture as colunas de dados **Server Name** e **Database ID** junto com a coluna de dados **Object Name** .  
  
 Se preferir agrupar pela coluna de dados **Object ID** , certifique-se de agrupar primeiro pelas colunas de dados **Server Name** e **Database ID** e, depois, pela coluna de dados **Object ID** . Similarmente, se preferir agrupar pela coluna de dados **Index ID** , certifique-se de agrupar primeiro pelas colunas de dados **Server Name**, **Database ID**e **Object ID** e, depois, pelas colunas de dados **Index ID** . É necessário agrupar nessa ordem porque as IDs de objeto e de índice não são exclusivas entre servidores e bancos de dados (e entre objetos quanto às IDs de índice).  
  
## <a name="finding-specific-events-within-a-trace"></a>Localizando eventos específicos em um rastreamento  
 Para localizar e agrupar eventos em um rastreamento, siga estas etapas:  
  
1.  Crie seu rastreamento.  
  
    -   Ao definir o rastreamento, capture as colunas de dados **Event Class**, **ClientProcessID**e **Start Time** , mais quaisquer outras que desejar. Para obter mais informações, consulte [Criar um rastreamento &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md).  
  
    -   Agrupe os dados capturados pela coluna de dados **Event Class**e capture o rastreamento em um arquivo ou tabela. Para agrupar os dados capturados, clique em **Organizar Colunas** na guia **Seleção de Eventos** da caixa de diálogo Propriedades do Rastreamento. Para obter mais informações, consulte [Organizar colunas exibidas em um rastreamento &#40;SQL Server Profiler&#41;](organize-columns-displayed-in-a-trace-sql-server-profiler.md).  
  
    -   Inicie o rastreamento e interrompa-o quando o tempo apropriado for atingido ou assim que o número de eventos tiver sido capturado.  
  
2.  Localize os eventos visados.  
  
    -   Abra o arquivo ou tabela de rastreamento e expanda o nó da classe de evento desejada; por exemplo, **Deadlock Chain**. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) ou do [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md).  
  
    -   Pesquise os dados do rastreamento até localizar os eventos que está buscando (use o comando **Localizar** do menu **Editar** do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para ajudá-lo a localizar valores no rastreamento). Observe os valores nas colunas de dados **ClientProcessID** e **Start Time** dos eventos rastreados.  
  
3.  Exiba os eventos em contexto.  
  
    -   Exiba as propriedades de rastreamento e agrupe pela coluna de dados **ClientProcessID**, em vez da **Event Class** .  
  
    -   Expanda os nós de cada ID de processo cliente que desejar exibir. Pesquise o rastreamento manualmente ou use **Localizar** até encontrar os valores de **Start Time**observados anteriormente para os eventos visados. Os eventos são exibidos em ordem cronológica com os outros eventos que pertencem a cada ID de processo cliente selecionado. Por exemplo, os eventos **Deadlock** e **Deadlock Chain**, capturados no rastreamento, aparecem imediatamente após os eventos **SQL:BatchStarting**events within the expeed client process ID.  
  
 A mesma técnica pode ser usada para localizar qualquer evento agrupado. Após localizar os eventos que procura, agrupe-os por **ClientProcessID**, **ApplicationName**ou outra classe de evento para ver a atividade relacionada em ordem cronológica.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir um rastreamento salvo &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-a-saved-trace-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)   
 [Exibir informações de filtro &#40;SQL Server Profiler&#41;](view-filter-information-sql-server-profiler.md)   
 [Exibir informações de filtro &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-filter-information-transact-sql.md)   
 [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md)   
 [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)  
  
  
