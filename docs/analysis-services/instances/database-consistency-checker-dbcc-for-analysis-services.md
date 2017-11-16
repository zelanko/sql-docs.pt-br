---
title: "Banco de dados (DBCC) do verificador de consistência para o Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 28714c32-718f-4f31-a597-b3289b04b864
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2e8ecc3c51619c7f1ebbe5b109f0710500184a27
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="database-consistency-checker-dbcc-for-analysis-services"></a>Verificador de consistência do banco de dados (DBCC) para o Analysis Services
  O DBCC fornece validação de banco de dados sob demanda para bancos de dados Multidimensionais e Tabulares em uma instância do Analysis Services. Você pode executar o DBCC em uma janela de consulta MDX ou XMLA no SSMS (SQL Server Management Studio) e rastrear a saída do DBCC no SQL Server Profiler ou nas sessões do xEvent no SSMS.  
O comando usa uma definição de objeto e retornará um conjunto de resultados vazio ou informações de erro detalhadas se o objeto estiver corrompido.   Neste artigo, você vai aprender a executar o comando, interpretar os resultados e resolver os problemas que surgirem.  
  
 Para bancos de dados tabulares, verificações de consistência executadas pelo DBCC são equivalentes à validação interna que ocorre automaticamente sempre que você recarrega, sincroniza ou restaura um banco de dados.  Por outro lado, verificações de consistência de bancos de dados multidimensionais ocorrem somente quando você executa o DBCC sob demanda.  
  
 O intervalo de verificações de validação variam por modo, com bancos de dados tabulares sujeitos a uma variedade maior de verificações.  
 As características de carga de trabalho DBCC também variam de acordo com o modo de servidor. Operações de verificação de bancos de dados multidimensionais envolvem a leitura de dados do disco, construção de índices temporários para comparação com índices reais; o que demora leva significativamente mais tempo para concluir.  
  
 A sintaxe de comando para o DBCC usa os metadados de objeto específicos para o tipo de banco de dados que você está verificando:  
  
-   Bancos de dados Multidimensionais e bancos de dados com nível de compatibilidade 1100 ou 1103 de Tabela anteriores ao SQL Server 2016 são descritos em construtos de modelagem multidimensional como **cubeID**, **measuregroupID**e **partitionID**.  
  
-   Metadados para novos bancos de dados de modelo de tabela no nível de compatibilidade 1200 e maior consistem em descritores como **TableName** e **PartitionName**.  
  
 O DBCC para Analysis Services será executado em qualquer banco de dados do Analysis Services em qualquer nível de compatibilidade, desde que o banco de dados esteja em execução em uma instância do SQL Server 2016. Verifique se que você está usando a sintaxe de comando correta para cada tipo de banco de dados.  
  
> [!NOTE]  
>  Se você estiver familiarizado com [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md), você perceberá rapidamente que o DBCC no Analysis Services tem um escopo muito mais estreito. O DBCC no Analysis Services é um único comando que reporta exclusivamente sobre dados corrompidos entre o banco de dados ou em objetos individuais. Se você tiver outras tarefas em mente, como coleta de informações, tente usar scripts do PowerShell do AMO ou XMLA. Consulte [Monitor an Analysis Services Instance](../../analysis-services/instances/monitor-an-analysis-services-instance.md) para obter links com mais informações.  
  
## <a name="permission-requirements"></a>Requisitos de permissão  
 Você deve ser um administrador do servidor ou do banco de dados do Analysis Services (um membro da função de servidor) para executar o comando. Consulte [Conceder permissões de banco de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) ou [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) para obter instruções.  
  
## <a name="command-syntax"></a>Sintaxe de comando 
 Níveis mais altos de compatibilidade e de bancos de dados tabulares na 1200 usam metadados tabulares para definições de objeto. A sintaxe completa de DBCC para um banco de dados tabular criado em um nível funcional do SQL Server 2016 é ilustrada no exemplo a seguir.  
  
 Principais diferenças entre as duas sintaxes incluem um namespace mais recente do XMLA, não \<objeto > elemento e não \<modelo > elemento (há apenas um modelo por banco de dados).  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2014/engine">  
     <DatabaseID>MyTabular1200DB_7811b5d8-c407-4203-8793-12e16c3d1b9b</DatabaseID>  
     <TableName>FactSales</TableName>  
     <PartitionName>FactSales 4</PartitionName>  
</DBCC>  
```  
  
 Você pode omitir os objetos de nível inferior, como nomes de tabela ou de partição, para verificar o esquema inteiro.  
  
 Você pode obter os nomes de objeto e o DatabaseID no Management Studio, por meio da página de propriedades de cada objeto.  
  
## <a name="command-syntax-for-multidimensional-and-tabular-110x-databases"></a>A sintaxe de comando para bancos de dados Multidimensionais e Tabulares 110x  
 O DBCC usa sintaxe idêntica para bancos de dados multidimensionais, bem como bancos de dados 1100 e 1103. Você pode executar o DBCC em objetos de banco de dados específicos, incluindo o banco de dados inteiro. Consulte [Elemento Object &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) Para obter mais informações sobre a definição do objeto.  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2006</PartitionID>  
     </Object>  
</DBCC>  
  
```  
  
 Para executar o DBCC em objetos superiores na cadeia de objeto, exclua todos elementos de ID de objeto de nível inferior que não sejam necessários:  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
     </Object>  
</DBCC>  
  
```  
  
 Para bancos de dados tabulares 110x, a sintaxe de definição do objeto é modelada após a sintaxe do comando de processo (especificamente, em como as tabelas são mapeadas para dimensões e grupos de medidas).  
  
-   **CubeID** mapeia para a ID do modelo, que é **Model**.  
  
-   **MeasureGroupID** mapeia para uma ID da tabela.  
  
-   **PartitionID** mapeia para uma ID da partição.  
  
## <a name="usage"></a>Uso  
 No SQL Server Management Studio, você pode invocar DBCC usando uma janela de consulta MDX ou XMLA. Além disso, você pode usar um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Profiler ou o Analysis Services xEvents para exibir a saída do DBCC. Observe que mensagens do SSAS DBCC não são relatadas ao log de eventos de aplicativos do Windows ou ao arquivo msmdsrv.log.  
  
 O DBCC verifica os dados corrompidos físicos, bem como os dados corrompidos lógicos que ocorrem quando existem membros órfãos em um segmento. Um banco de dados deve ser processado antes que você possa executar o DBCC. Ele ignora as partições remotas, vazias ou não processadas.  
  
 O comando é executado em uma transação de leitura e, portanto, pode ser inicializado pelo tempo limite de confirmação de força. As verificações de partição são executadas em paralelo.  
  
 Uma reinicialização do serviço pode ser necessária para acompanhar quaisquer erros de corrupção que ocorreram desde a última reinicialização do serviço. Reconectar-se ao servidor não é suficiente para acompanhar as alterações.  
  
### <a name="run-dbcc-commands-in-management-studio"></a>Execute os comandos do DBCC no Management Studio  
 Para consultas ad hoc, abra uma janela de consulta MDX ou XMLA no SQL Server Management Studio. Para fazer isso, clique com o botão direito do mouse no banco de dados | **Nova Consulta** | **XMLA**) para executar o comando e ler a saída.  
  
 ![Comando DBCC XML no Management Studio](../../analysis-services/instances/media/ssas-dbcc-ssms.gif "comando DBCC XML no Management Studio")  
  
 A guia Resultados indicará um conjunto de resultados vazio definido (como mostrado na captura de tela), se nenhum problema for detectado.  
  
 A guia Mensagens fornece informações detalhadas, mas nem sempre é confiável para bancos de dados menores. As mensagens de status às vezes são cortadas, indicando que o comando foi concluído, mas sem as mensagens de verificação de status em cada objeto. Um relatório de mensagem típico pode ser semelhante ao mostrado a seguir.  
  
 **As mensagens relatadas do DBCC para a verificação de validação do cubo**  
  
```  
Executing the query ...  
READS, 0  
READ_KB, 0  
WRITES, 0  
WRITE_KB, 0  
CPU_TIME_MS, 0  
ROWS_SCANNED, 0  
ROWS_RETURNED, 0  
  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
<Object>  
<DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
<CubeID>Adventure Works</CubeID>  
</Object>  
</DBCC>  
Started checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2012' partition.  
Finished checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2013' partition.  
Finished checking segment indexes for the 'Internet_Sales_2012' partition.  
Started checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2011' partition.  
Finished checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2012' partition.  
Started checking segment indexes for the 'Internet_Orders_2013' partition.  
Finished checking segment indexes for the 'Internet_Orders_2012' partition.  
...   
Run complete  
  
```  
  
 **Saída ao executar DBCC em uma versão anterior do Analysis Services**  
  
 O DBCC só tem suporte em bancos de dados em execução em uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Executar o comando em sistemas mais antigos retornará esse erro.  
  
```  
Executing the query ...  
The DBCC element at line 7, column 87 (namespace http://schemas.microsoft.com/analysisservices/2003/engine) cannot appear under Envelope/Body/Execute/Command.  
Execution complete  
  
```  
  
### <a name="trace-dbcc-output-in-sql-server-profiler-2016"></a>Rastreamento de saída do DBCC no SQL Server Profiler 2016  
 Você pode exibir a saída do DBCC em um rastreamento do Profiler que inclui eventos de relatórios de andamento (Início do Relatório de Andamento, Relatório de Andamento Atual, Final do Relatório de Andamento e Erro no Relatório de Andamento).  
  
1.  Iniciar um rastreamento. Consulte [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md) para obter ajuda sobre como usar o SQL Server Profiler com o Analysis Services.  
  
2.  Escolha **Command Begin** e o **Comando End** mais algum ou todos os eventos do **Relatório de Andamento** .  
  
3.  Execute o comando DBCC no Management Studio em uma janela de consulta XMLA ou MDX, usando a sintaxe fornecida em uma seção anterior.  
  
4.  No SQL Server Profiler, atividade do DBCC é indicada por meio de eventos de **Command** com uma subclasse de evento de DBCC:  
  
     ![SSAS dbcc-profiler eventsubclass](../../analysis-services/instances/media/ssas-dbcc-profiler-eventsubclass.PNG "ssas dbcc-profiler eventsubclass")  
  
     O código de evento 32 é a execução de DBCC.  
  
     O código de evento 64 é um relatório de andamento do DBCC sobre objetos individuais.  
  
     O código de evento 63 é uma verificação de segmento de objetos multidimensionais.  
  
     Para ambas as subclasses de eventos, examine os valores do **TextData** para as mensagens retornadas por DBCC.  
  
     Mensagens de status começam com "Verificando a consistência da \<objeto >", "verificação iniciada \<objeto >", ou "terminar verificando \<objeto >".  
  
    > [!NOTE]  
    >  No CTP 3.0, os objetos são identificados por nomes internos. Por exemplo, uma hierarquia de categorias é articulada como H$ Categories -\<objectID >. Nomes internos devem ser substituídos por nomes amigáveis de usuário em um CTP futuro.  
  
     As mensagens de erro estão listadas abaixo.  
  
### <a name="trace-dbcc-output-in-an-xevent-session-in-ssms"></a>Rastreie a saída do DBCC em uma sessão xEvent no SSMS  
 Sessões de eventos estendidos podem usar eventos do Profiler ou do xEvents. Consulte a seção anterior para obter diretrizes sobre como adicionar eventos **Command** e **Progress Report** .  
  
1.  Inicie uma sessão clicando com o botão direito do mouse em um banco de dados > **Gerenciamento** >**Eventos Estendidos** >  **Sessões** > **Nova Sessão**. Consulte  [Monitor Analysis Services with SQL Server Extended Events](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) para obter mais informações.  
  
2.  Escolha um ou todos os eventos do **Relatório de Andamento** para a categoria de evento do Profiler ou eventos **RequestProgress** da categoria PureXevent.  
  
3.  Execute o comando DBCC no Management Studio em uma janela de consulta XMLA ou MDX, usando a sintaxe fornecida em uma seção anterior.  
  
4.  No SSMS, atualize a pasta Sessões. Clique com o botão direito do mouse no nome da sessão > **Observar Dados Dinâmicos**.  
  
5.  Examine os valores de TextData para mensagens retornadas pelo DBCC.  TextData é uma propriedade de um campo de evento e mostra o status e as mensagens de erro retornadas pelo evento.  
  
     Mensagens de status começam com "Verificando a consistência da \<objeto >", "verificação iniciada \<objeto >", ou "terminar verificando \<objeto >".  
  
     As mensagens de erro estão listadas abaixo.  
  
## <a name="reference-consistency-checks-and-errors-for-multidimensional-databases"></a>Referência: verificações de consistência e erros de bancos de dados multidimensionais  
 Para bancos de dados multidimensionais, somente os índices de partição são validados.  Durante a execução, o DBCC criará um índice temporário para cada partição e o comparará com o índice persistente no disco.  Compilar um índice temporário requer ler todos os dados dos dados da partição no disco e, em seguida, manter o índice temporário na memória para comparação. Dada a carga de trabalho adicional, o servidor terá um consumo de memória e E/S de disco significativo durante a execução de uma execução de DBCC.  
  
 A detecção de corrupção de índice Multidimensional inclui as seguintes verificações. Os erros nesta tabela aparecem no xEvent ou o Profiler rastreia falhas no nível do objeto.  
  
||||  
|-|-|-|  
|**Objeto**|**Descrição de verificação do DBCC**|**Erro na falha**|  
|Índice de Partição|Verifique os índices e estatísticas do segmento.<br /><br /> Compara a ID de cada membro no índice de partição temporária com as estatísticas de partição armazenadas no disco.  Se um membro for encontrado no índice temporário com um valor de ID de dados fora do intervalo armazenado para as estatísticas de índice de partição no disco, as estatísticas de índice serão consideradas corrompidas.|As estatísticas do segmento da partição estão corrompidas.|  
|Índice de Partição|Valida os metadados.<br /><br /> Verifica que cada membro no índice temporário pode ser encontrado no arquivo de cabeçalho de índice do segmento no disco.|O segmento da partição está corrompido.|  
|Índice de Partição|Verificar segmentos para procurar corrupção física.<br /><br /> Lê o arquivo de índice em disco para cada membro no índice temporário e verifica se o tamanho dos registros de índice correspondem e que as mesmas páginas de dados são sinalizadas como tendo registros para o membro atual.|O segmento da partição está corrompido.|  
  
## <a name="reference-consistency-checks-and-errors-for-tabular-databases"></a>Referência: verificações de consistência e erros de bancos de dados tabulares  
 A tabela a seguir é a lista de todas as verificações de consistência executadas em objetos tabulares, juntamente com os erros que são gerados se a verificação indica corrupção. Os erros nesta tabela aparecem no xEvent ou o Profiler rastreia falhas no nível do objeto.  
  
||||  
|-|-|-|  
|**Objeto**|**Descrição de verificação do DBCC**|**Erro na falha**|  
|Banco de dados|Verifica a contagem de tabelas no banco de dados.  Um valor menor que zero indica corrupção.|Há corrupção na camada de armazenamento. A coleção de tabelas no banco de dados '%{parent/}' está corrompida.|  
|Banco de dados|Verifica a estrutura interna usada para rastrear a integridade referencial e lança um erro se o tamanho estiver incorreto.|Os arquivos de banco de dados não passaram nas verificações de consistência.|  
|Table|Verifica o valor interno usado para determinar se a tabela é uma tabela de dimensão ou de fatos.  Um valor que está fora do intervalo conhecido que indica corrupção.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar as estatísticas da tabela.|  
|Table|Verifica se o número de partições no mapa do segmento da tabela corresponde ao número de partições definidas para a tabela.|Há corrupção na camada de armazenamento. A coleção de partições na tabela '%{parent/}' está corrompida.|  
|Table|Se um banco de dados tabular for criado ou importado do PowerPivot para Excel 2010 e tiver uma contagem de partição maior que um, um erro será gerado, pois o suporte de partição foi adicionado em versões posteriores e isso poderia indicar corrupção.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar o mapa do segmento.|  
|Partition|Verifica para cada partição que o número de segmentos do banco de dados e a contagem de registros de cada segmento de dados do segmento correspondem aos valores armazenados no índice do segmento.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar o mapa do segmento.|  
|Partition|Gerar um erro se o número total de registros, segmentos ou registros por segmento não é válido (menor que zero) ou o número de segmentos não corresponde ao número calculado de segmentos necessários com base na contagem total de registros.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar o mapa do segmento.|  
|Relação|Gerará um erro se a estrutura usada para armazenar dados sobre o relacionamento não contiver registros ou se o nome da tabela usada na relação estiver vazio.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar a relação.|  
|Relação|Verifique se que o nome da tabela primária, a coluna primária, a tabela estrangeira e a coluna externa são definidas e se as colunas e as tabelas envolvidas na relação podem ser acessadas.<br /><br /> Verifique se os tipos de coluna envolvidos são válidos e se os valores de índice de chave primária/chave estrangeira resultam em uma estrutura de pesquisa válida.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar a relação.|  
|Hierarquia|Gerar um erro se a ordem de classificação da hierarquia não for um valor reconhecido.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar a hierarquia '%{hier/}'.|  
|Hierarquia|As verificações executadas na hierarquia dependem do tipo interno de esquema de mapeamento de hierarquia usado.<br /><br /> Todas as hierarquias são verificadas em relação ao estado processado correto, se a hierarquia de repositório existe e se, quando aplicável, estruturas de dados usadas para uma conversão de ID de dados para posição de hierarquia existem.<br /><br /> Supondo que todas essas verificações passem, a estrutura da hierarquia será movimentada para verificar se cada posição na hierarquia corresponde ao membro correto.<br />Se algum desses testes falhar, um erro será gerado.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar a hierarquia '%{hier/}'.|  
|Hierarquia definida pelo usuário|Verifica se os nomes de nível de hierarquia são definidos.<br /><br /> Se a hierarquia foi processada, verifique se o armazenamento de dados da hierarquia interna tem o formato correto.  Verifique se o repositório de hierarquia interna não contém nenhum valor de dados inválido.<br /><br /> Se a hierarquia for marcada como não processada, confirme que esse estado se aplicará a estruturas de dados antigas e que todos os níveis da hierarquia serão marcados como vazios.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar a hierarquia '%{hier/}'.|  
|Coluna|Gerar um erro se a codificação usada para a coluna não for definida para um valor conhecido.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar as estatísticas da coluna.|  
|Coluna|Verifique se a coluna foi compactada pelo mecanismo na memória ou não.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar as estatísticas da coluna.|  
|Coluna|Verifique o tipo de compactação na coluna de valores conhecidos.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar as estatísticas da coluna.|  
|Coluna|Quando a coluna "geração de tokens" não estiver definida para um valor conhecido, um erro será gerado.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar as estatísticas da coluna.|  
|Coluna|Se o intervalo de ID armazenado para um dicionário de dados de colunas não coincidir com o número de valores no dicionário de dados ou estiver fora do intervalo permitido, será gerado um erro.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar o dicionário de dados.|  
|Coluna|Verifique se o número de segmentos de dados de uma coluna corresponde ao número de segmentos de dados da tabela à qual ela pertence.|Há corrupção na camada de armazenamento. A coleção de segmentos da coluna '%{parent/}' está corrompida.|  
|Coluna|Verifique se o número de partições de uma coluna de dados corresponde ao número de partições do mapa de segmento de dados da coluna.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar o mapa do segmento.|  
|Coluna|Verifique se o número de registros em um segmento de coluna corresponde à contagem de registros armazenada no índice desse segmento de coluna.|Há corrupção na camada de armazenamento. A coleção de segmentos da coluna '%{parent/}' está corrompida.|  
|Coluna|Se uma coluna não tiver nenhuma estatística de segmento, será gerado um erro.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar as estatísticas do segmento.|  
|Coluna|Se uma coluna não tiver informações de compactação ou de armazenamento de segmento, será gerado um erro.|Os arquivos de banco de dados não passaram nas verificações de consistência.|  
|Coluna|Relate um erro se as estatísticas do segmento de uma coluna não coincidirem com os valores da coluna real para a ID de dados mínimos, ID de dados máximos, número de valores distintos, número de linhas ou a presença de valores NULL.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar as estatísticas do segmento.|  
|ColumnSegment|Se a ID de dados mínimos ou a ID de dados máximos for menor que o valor do sistema reservado para NULL, marque as informações de segmento de coluna como corrompido.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar as estatísticas do segmento.|  
|ColumnSegment|Se não houver nenhuma linha para este segmento, os valores mínimo e máximo de dados da coluna devem ser definidos para o valor do sistema reservado para NULL.  Se o valor não for nulo, será gerado um erro.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar as estatísticas do segmento.|  
|ColumnSegment|Se a coluna tiver linhas e pelo menos um valor não nulo, verifique que a ID de dados mínimos e máximos da coluna é maior que o valor do sistema reservado para NULL.|As verificações de consistência do banco de dados (DBCC) falharam ao verificar as estatísticas do segmento.|  
|Internal|Verifique se que a dica de geração de tokens do repositório é definida e que, se o repositório for processado, haverá ponteiros válidos para tabelas internas.  Se o repositório não for processado, verifique se que todos os ponteiros são nulos.<br />Caso contrário, retorne um erro genérico de DBCC.|Os arquivos de banco de dados não passaram nas verificações de consistência.|  
|Banco de dados do DBCC|Gere um erro se o esquema de banco de dados não tiver nenhuma tabela ou uma ou mais tabelas não puder ser acessada.|Há corrupção na camada de armazenamento. A coleção de tabelas no banco de dados '%{parent/}' está corrompida.|  
|Banco de dados do DBCC|Gere um erro se uma tabela for marcada como temporária ou tiver um tipo desconhecido.|Um tipo de tabela inválido foi encontrado.|  
|Banco de dados do DBCC|Gere um erro se o número de relações de uma tabela tiver um valor negativo ou se qualquer tabela que tiver uma relação definida e uma estrutura de relação correspondente não puder ser encontrada.|Há corrupção na camada de armazenamento. A coleção de relações na tabela '%{parent/}' está corrompida.|  
|Banco de dados do DBCC|Se o nível de compatibilidade do banco de dados for 1050 (SQL Server 2008 R2/PowerPivot v1.0) e o número de relações exceder o número de tabelas no modelo, o banco de dados será marcado como corrompido.|Os arquivos de banco de dados não passaram nas verificações de consistência.|  
|Tabela de DBCC|Para a tabela em validação, verifique se o número de colunas é menor que zero e gere um erro se for verdadeiro.  Também ocorrerá um erro se o repositório de coluna de uma coluna na tabela for NULL.|Há corrupção na camada de armazenamento. A coleção de colunas na tabela '%{parent/}' está corrompida.|  
|Partição do DBCC|Verifica se a quem a tabela que pertence a partição que está sendo validada pertence e se o número de colunas da tabela for menor que zero, indica que a coleção de colunas está corrompida para a tabela. Também ocorrerá um erro se o repositório de coluna de uma coluna na tabela for NULL.|Há corrupção na camada de armazenamento. A coleção de colunas na tabela '%{parent/}' está corrompida.|  
|Partição do DBCC|Percorre cada coluna da partição selecionada e verifica se cada segmento da partição tem um link válido para uma estrutura de segmento de coluna.  Se nenhum segmento tiver um link NULL, a partição será considerada corrompida.|Há corrupção na camada de armazenamento. A coleção de segmentos da coluna '%{parent/}' está corrompida.|  
|Coluna|Retornará um erro se o tipo de coluna não for válido.|Um tipo de segmento inválido foi encontrado.|  
|Coluna|Retornará um erro se qualquer coluna tiver uma contagem negativa para o número de segmentos em uma coluna ou se o ponteiro para a estrutura de segmento de coluna de um segmento tiver um link NULL.|Há corrupção na camada de armazenamento. A coleção de segmentos da coluna '%{parent/}' está corrompida.|  
|Comando DBCC|O comando DBCC relatará várias mensagens de status conforme ele passa para a operação de DBCC.  Ele relatará uma mensagem de status antes de iniciar, que inclui o banco de dados, a tabela ou o nome de coluna do objeto e novamente após a conclusão de cada verificação de objeto.|Verificando a consistência do \<objectname > \<objecttype >. Fase: pré-verificação.<br /><br /> Verificando a consistência do \<objectname > \<objecttype >. Fase: pós-verificação.|  
  
## <a name="common-resolutions-for-error-conditions"></a>Resoluções comuns para condições de erro  
 Os seguintes erros aparecem no SQL Server Management Studio ou em arquivos msmdsrv.log. Esses erros aparecem quando uma ou mais verificações não forem aprovadas. Dependendo do erro, a resolução recomendada é reprocessar um objeto, excluir e reimplantar uma solução ou restaurar o banco de dados.  
  
|Erro|Problema|Resolução|  
|-----------|-----------|----------------|  
|**Erros no gerenciador de metadados**<br /><br /> A referência de objeto '\<objectID >' não é válido. Ela não corresponde à estrutura da hierarquia da classe de metadados.|comando malformado|Verifique a sintaxe do comando. Provavelmente, você incluiu um objeto de nível inferior sem especificar um ou mais dos seus objetos pai.|  
|**Erros no gerenciador de metadados**<br /><br /> Ou o \<objeto > com a ID '\<objectID >' não existe no \<parentobject > com a ID '\<parentobjectID >', ou o usuário não tem permissões para acessar o objeto.|Corrupção de índice (multidimensional)|Reprocesse o objeto e todos os objetos dependentes.|  
|**Erro durante a verificação de consistência da partição**<br /><br /> Ocorreu um erro ao verificar a consistência do \<nome da partição > partição do \<nome do grupo de medidas > grupo de medidas para o \<nome do cubo > do cubo do \<nome do banco de dados > banco de dados. Processe novamente a partição ou os índices para corrigir a corrupção.|Corrupção de índice (multidimensional)|Reprocesse o objeto e todos os objetos dependentes.|  
|**As estatísticas do segmento da partição estão corrompidas**|Corrupção de índice (multidimensional)|Reprocesse o objeto e todos os objetos dependentes.|  
|**O segmento da partição está corrompido**|Corrupção de metadados (multidimensional ou tabular)|Excluir e reimplantar o projeto ou restaurar de um backup e reprocessar.<br /><br /> Consulte [How to Deal with Corruption in Analysis Services (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Como lidar com danos nos bancos de dados do Analysis Services) para obter instruções.|  
|**Metadados de tabela corrompidos**<br /><br /> Tabela \<nome da tabela > arquivo de metadados está corrompido. A tabela principal não foi encontrada no nó DataFileList.|Corrupção de metadados (somente tabular)|Excluir e reimplantar o projeto ou restaurar de um backup e reprocessar.<br /><br /> Consulte [How to Deal with Corruption in Analysis Services (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Como lidar com danos nos bancos de dados do Analysis Services) para obter instruções.|  
|**Corrupção na camada de armazenamento**<br /><br /> Corrupção na camada de armazenamento: coleção de \<nome do tipo > em \<pai-name > \<tipo pai > está corrompido.|Corrupção de metadados (somente tabular)|Excluir e reimplantar o projeto ou restaurar de um backup e reprocessar.<br /><br /> Consulte [How to Deal with Corruption in Analysis Services (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Como lidar com danos nos bancos de dados do Analysis Services) para obter instruções.|  
|**A tabela do sistema está ausente**<br /><br /> Tabela do sistema \<nome da tabela > está ausente.|Corrupção do objeto (somente tabular)|Reprocesse o objeto e todos os objetos dependentes|  
|**As estatísticas de tabela estão corrompidas**<br /><br /> Estatísticas de tabela do sistema \<nome da tabela > está ausente.|Corrupção de metadados (somente tabular)|Excluir e reimplantar o projeto ou restaurar de um backup e reprocessar.<br /><br /> Consulte [How to Deal with Corruption in Analysis Services (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Como lidar com danos nos bancos de dados do Analysis Services) para obter instruções.|  
  
## <a name="disable-automatic-consistency-checks-on-database-load-operations-through--the-msmdsrvini-configuration-file"></a>Desabilitar verificações automáticas de consistência em operações de carregamento de banco de dados por meio do arquivo de configuração msmdsrv.ini  
 Embora não seja recomendado, você pode desabilitar as verificações de consistência do banco de dados integrado que ocorrem automaticamente em eventos de carregamento de banco de dados (somente em bancos de dados tabulares). Para fazer isso, você precisará modificar uma definição de configuração no arquivo msmdsrv.ini:  
  
```  
<ConfigurationSettings>  
     <Vertipaq />  
          <DisableConsistencyChecks />  
```  
  
 Essa configuração não está presente no arquivo de configuração e deve ser adicionada manualmente.  
  
 Estes são os valores válidos:  
  
-   O DBCC**-2** (padrão) está habilitado. Se o servidor puder resolver o erro logicamente com um alto grau de certeza, uma correção será aplicada automaticamente. Caso contrário, um erro será registrado.  
  
-   O DBCC**-1** está parcialmente habilitado. Ele é habilitado para restauração e em validações de pré-confirmação que verificam o estado do banco de dados ao final de uma transação.  
  
-   O DBCC do**0** está parcialmente habilitado. Verificações de consistência do banco de dados são executadas durante as operações RESTORE, IMAGELOAD, LOCALCUBELOAD e ATTACH  
         .  
  
-   O DBCC do**1** está desabilitado. As verificações de integridade de dados estão desabilitadas, no entanto, ainda ocorrerão verificações de desserialização.  
  
> [!NOTE]  
>  Essa configuração não terá impacto no DBCC quando o comando for executado sob demanda.  
  
## <a name="see-also"></a>Consulte também  
 [Processar banco de dados, tabela ou partição &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [Processando um modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Monitorar uma instância do Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)   
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  

