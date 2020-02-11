---
title: Utilitário bcp | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server]
- exporting data
- row exporting [SQL Server]
- copying data [SQL Server], bcp utility
- command prompt utilities [SQL Server], bcp
- tables [SQL Server], importing data
- column importing [SQL Server]
- bcp utility [SQL Server], command options
- file exporting [SQL Server]
- bulk copy [SQL Server]
- bcp utility [SQL Server], about bcp utility
- tables [SQL Server], exporting data
- row importing [SQL Server]
- importing data, bcp utility
- file importing [SQL Server]
- column exporting [SQL Server]
ms.assetid: c0af54f5-ca4a-4995-a3a4-0ce39c30ec38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 24367bfec4b0e25fec60eb49c77a74e1ccd54f46
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68187153"
---
# <a name="bcp-utility"></a>Utilitário bcp
  O utilitário **bcp** copia dados em massa entre uma instância [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] do e um arquivo de dados em um formato especificado pelo usuário. O utilitário **bcp** pode ser usado para importar grande número de novas linhas para tabelas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou para exportar dados de tabelas para arquivos de dados. Exceto quando usado com a opção **queryout** , o utilitário não requer conhecimento de [!INCLUDE[tsql](../includes/tsql-md.md)]. Para importar dados para uma tabela, você deve usar um arquivo de formato criado para aquela tabela ou entender a estrutura da tabela e os tipos de dados válidos para suas colunas.  
  
 ![Ícone de link do tópico](../../2014/database-engine/media/topic-link.gif "Ícone de link do tópico") Para obter as convenções de sintaxe usadas para a sintaxe **bcp** , consulte [convenções de sintaxe transact-SQL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).  
  
> [!NOTE]  
>  Se você usar **bcp** para fazer backup de seus dados, crie um arquivo de formato para registrar o formato dos dados. os arquivos de dados **bcp** não incluem nenhuma informação de esquema ou formato, portanto, se uma tabela ou exibição for descartada e você não tiver um arquivo de formato, talvez não seja possível importar os dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
   bcp [database_name.] schema.{table_name | view_name | "query" {indata_file | outdata_file | queryoutdata_file | format nul}  
  
[-apacket_size]  
[-bbatch_size]  
[-c]  
[-C { ACP | OEM | RAW | code_page } ]  
[-ddatabase_name]  
[-eerr_file]  
[-E]  
[-fformat_file]  
[-Ffirst_row]  
[-h"hint [,...n]"]   
[-iinput_file]  
[-k]  
[-Kapplication_intent]  
[-Llast_row]  
[-mmax_errors]  
[-n]  
[-N]  
[-ooutput_file]  
[-Ppassword]  
[-q]  
[-rrow_term]  
[-R]  
[-S [server_name[\instance_name]]  
[-tfield_term]  
[-T]  
[-Ulogin_id]  
[-v]  
[-V (80 | 90 | 100 | 110)]  
[-w]  
[-x]  
/?  
```  
  
## <a name="arguments"></a>Argumentos  
 *data_file*  
 É o caminho completo do arquivo de dados. Quando dados são importados em massa para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o arquivo de dados contém os dados a serem copiados na tabela ou exibição especificada. Quando dados são exportados em massa do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o arquivo de dados contém os dados copiados da tabela ou exibição. O caminho pode ter de 1 a 255 caracteres. O arquivo de dados pode conter no máximo 2<sup>63</sup> -1 linhas.  
  
 *database_name*  
 É o nome do banco de dados no qual a tabela ou exibição especificada reside. Se não estiver especificado, esse será o banco de dados padrão do usuário.  
  
 Você também pode especificar explicitamente o nome de banco de dados com `d-`.  
  
 **em** _data_file_ | **out**__ data_file | __ data_file | **formato** de**consulta**NUL  
 Especifica a direção da cópia em massa, do seguinte modo:  
  
-   **em** cópias de um arquivo para a tabela ou exibição de banco de dados.  
  
-   **saída** de cópias da tabela ou exibição de banco de dados para um arquivo. Se você especificar um arquivo existente, o arquivo será substituído. Ao extrair dados, observe que o utilitário **bcp** representa uma cadeia de caracteres vazia como nula e uma cadeia de caracteres nula como uma cadeia de caracteres vazia.  
  
-   **consultar** cópias de uma consulta e deve ser especificado somente ao copiar dados em massa de uma consulta.  
  
-   o **formato** cria um arquivo de formato com base na opção especificada (**-n**, `-c`, `-w`ou **-n**) e nos delimitadores de exibição ou tabela. Quando você copia dados em massa, o comando **bcp** pode recorrer a um arquivo de formato, o que libera você da necessidade de inserir novamente as informações de formato de forma interativa. A opção **format** exige a opção **-f** ; a criação de um arquivo de formato XML também exige a opção **-x** . Para obter mais informações, consulte [Criar um arquivo de formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md). É necessário especificar **nul** como o valor (**format nul**).  
  
 *proprietário*  
 Corresponde ao nome do proprietário da tabela ou exibição. o *proprietário* será opcional se o usuário que executa a operação possuir a tabela ou exibição especificada. Se *owner* não estiver especificado e o usuário que está executando a operação não for proprietário da tabela ou exibição especificada, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] retornará uma mensagem de erro e a operação será cancelada.  
  
 **"** _consulta_ **"**  
 É uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que retorna um conjunto de resultados. Se a consulta retornar vários conjuntos de resultados, somente o primeiro conjunto de resultados será copiado no arquivo de dados; os conjuntos de resultados subsequentes serão ignorados. Coloque a consulta entre aspas duplas e qualquer coisa incorporada na consulta entre aspas simples. **queryout** também deve ser especificado ao copiar dados em massa de uma consulta.  
  
 A consulta pode fazer referência a um procedimento armazenado desde que todas as tabelas referenciadas no procedimento armazenado existam antes da execução da instrução bcp. Por exemplo, se o procedimento armazenado gerar uma tabela temporária, ocorrerá uma falha com a instrução **bcp** , pois a tabela temporária ficará disponível somente durante o tempo de execução e não durante o tempo de execução da instrução. Nesse caso, considere a inserção do resultado do procedimento armazenado em uma tabela e, em seguida, use **bcp** para copiar os dados da tabela em um arquivo de dados.  
  
 *table_name*  
 Nome da tabela de destino ao importar dados para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**in**) e da tabela de origem ao exportar dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**out**).  
  
 *view_name*  
 Nome da exibição de destino ao copiar dados no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**in**) e da exibição de origem ao copiar dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (**out**). Somente as exibições nas quais todas as colunas fazem referência à mesma tabela podem ser usadas como exibições de destino. Para obter mais informações sobre as restrições para copiar dados em exibições, veja [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql).  
  
 **-um** _packet_size_  
 Especifica o número de bytes por pacote de rede enviado de e para o servidor. Uma opção de configuração do servidor pode ser definida usando [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (ou o procedimento armazenado do sistema **sp_configure** ). Contudo, a opção de configuração do servidor pode ser substituída individualmente usando-se esta opção. *packet_size* pode ser de 4096 a 65535 bytes; o padrão é 4096.  
  
 Um tamanho de pacote maior pode aumentar o desempenho de operações de cópia em massa. Se um pacote maior for pedido mas não puder ser concedido, o padrão será usado. As estatísticas de desempenho geradas pelo utilitário **bcp** mostram o tamanho de pacote usado.  
  
 **-b** _batch_size_  
 Especifica o número de linhas por lote de dados importados. Cada lote é importado e registrado como uma transação separada que importa o lote inteiro antes de ser confirmado. Por padrão, todas as linhas no arquivo de dados são importadas como um lote. Para distribuir as linhas entre vários lotes, especifique um *batch_size* que seja menor do que o número de linhas no arquivo de dados. Se a transação apresentar falha para qualquer lote, só serão revertidas as inserções do lote atual. Lotes já importados por transações confirmadas não serão afetados por uma falha posterior.  
  
 Não use essa opção em conjunto com a opção **-h "** ROWS_PER_BATCH ** = *`bb`*"** .  
  
 `-c`  
 Executa a operação usando um tipo de dados de caractere. Essa opção não solicita cada campo; Ele usa `char` como o tipo de armazenamento, sem prefixos e com **\t** (caractere de tabulação) como o separador de campo e **\r\n** (caractere de nova linha) como terminador de linhas. 
  `-c` não é compatível com `-w`.  
  
 Para obter mais informações, veja [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).  
  
 **-C** {*code_page* **brutos** | de**OEM** | do **ACP** | }  
 Especifica a página de código dos dados no arquivo de dados. *code_page* só será relevante se os dados contiverem `char`colunas, `varchar`ou `text` com valores de caracteres maiores que 127 ou menores que 32.  
  
> [!NOTE]  
>  Recomendamos que você especifique um nome de ordenação para cada coluna em um arquivo de formato.  
  
|Valor da página de código|DESCRIÇÃO|  
|---------------------|-----------------|  
|ACP|
  [!INCLUDE[vcpransi](../includes/vcpransi-md.md)]/Microsoft Windows (ISO 1252).|  
|OEM|Página de código padrão usada pelo cliente. Essa é a página de código padrão usada se **-C** não for especificado.|  
|RAW|Não ocorre nenhuma conversão de uma página de código para outra. Essa é a opção mais rápida porque não acontece nenhuma conversão.|  
|*code_page*|Um número de página de código específico, por exemplo, 850.<br /><br /> **&#42;&#42; importante &#42;&#42;** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não dá suporte à página de código 65001 (codificação UTF-8).|  
  
 `-d`*database_name*  
 Especifica o banco de dados que deve ser conectado. Por padrão, bcp.exe se conecta ao banco de dados padrão do usuário. Se `-d` *database_name* e um nome de três partes (*database_name. Schema. Table*, passado como o primeiro parâmetro para bcp. exe) for especificado, ocorrerá um erro porque você não pode especificar o nome do banco de dados duas vezes. Se *database_name* começar com um hífen (-) ou uma barra (/), não adicione um espaço entre `-d` o e o nome do banco de dados.  
  
 **-e** _err_file_  
 Especifica o caminho completo de um arquivo de erro usado para armazenar as linhas que o utilitário **bcp** não pode transferir do arquivo para o banco de dados. As mensagens de erro do comando **bcp** vão para a estação de trabalho do usuário. Se essa opção não for usada, o arquivo de erros não será criado.  
  
 Se *err_file* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-e** e o valor *err_file* .  
  
 **-E**  
 Especifica que o valor, ou valores, de identidade no arquivo de dados importado deve ser usado para a coluna de identidade. Se **-E** não for fornecido, os valores de identidade para essa coluna no arquivo de dados que está sendo importado serão ignorados e o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] atribuirá automaticamente valores exclusivos com base nos valores semente e de incremento especificados durante a criação da tabela.  
  
 Se o arquivo de dados não contiver valores para a coluna de identidade na tabela ou exibição, use um arquivo de formato para especificar que a coluna de identidade na tabela ou exibição deve ser ignorada ao importar dados. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] atribui valores exclusivos para a coluna automaticamente. Para obter mais informações, veja [DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql).  
  
 A opção **-E** tem um requisito de permissões especial. Para obter mais informações, consulte "Comentários" mais adiante neste tópico.  
  
 **-f** _format_file_  
 Especifica o caminho completo de um arquivo de formato. O significado dessa opção depende do ambiente no qual é usada, do seguinte modo:  
  
-   Se **-f** for usado com a opção **format** , o *format_file* especificado será criado para a tabela ou exibição especificada. Para criar um arquivo de formato XML, especifique também a opção **-x** . Para obter mais informações, consulte [Criar um arquivo de formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md).  
  
-   Se for usado com a opção **in** ou **out** , **-f** exigirá um arquivo de formato existente.  
  
    > [!NOTE]  
    >  O uso de um arquivo de formato com a opção **in** ou **out** é opcional. Na ausência da opção **-f** , se **-n**, `-c`, `-w`ou **-n** não for especificado, o comando solicitará informações de formato e permitirá que você salve suas respostas em um arquivo de formato (cujo nome de arquivo padrão é bcp. fmt).  
  
 Se *format_file* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-f** e o valor *format_file* .  
  
 **-F** _first_row_  
 Especifica o número da primeira linha que deve ser exportada de uma tabela ou importada de um arquivo de dados. Esse parâmetro requer um valor maior que (>) 0, mas menor que\<() ou igual a (=) o número total de linhas. Na ausência desse parâmetro, o padrão é a primeira linha do arquivo.  
  
 *first_row* pode ser um inteiro positivo com um valor de até 2 ^ 63-1. **-F**_first_row_ é baseado em 1.  
  
 **-h "** _dica_[ **,**... *n*] **"**  
 Especifica a dica ou dicas a serem usadas durante uma importação de dados em massa para uma tabela ou exibição.  
  
 Order **(**_coluna_[ASC | DESC] [**,**... *n*] **)**  
 A ordem de classificação dos dados no arquivo de dados. O desempenho da importação em massa será melhorado se os dados importados forem armazenados de acordo com o índice clusterizado na tabela, se houver. Se o arquivo de dados for armazenado em uma ordem diferente, ou seja, distinta da ordem de uma chave de índice clusterizado, ou se não houver nenhum índice clusterizado na tabela, a cláusula ORDER será ignorada. Os nomes das colunas fornecidos devem ser nomes de colunas válidas na tabela de destino. Por padrão, o **bcp** supõe que o arquivo de dados não está classificado. Para obter uma importação em massa otimizada, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] também valida que os dados importados sejam classificados.  
  
 ROWS_PER_BATCH **=** _BB_  
 Número de linhas de dados por lote (como *bb*). É usado quando **-b** não é especificado, resultando no envio de todo o arquivo de dados ao servidor como uma transação única. O servidor otimiza o carregamento em massa de acordo com o valor *bb*. Por padrão, ROWS_PER_BATCH é desconhecido.  
  
 KILOBYTES_PER_BATCH **=** _CC_  
 Número aproximado de kilobytes de dados por lote (como *cc*). Por padrão, KILOBYTES_PER_BATCH é desconhecido.  
  
 TABLOCK  
 Especifica que um bloqueio no nível de tabela de atualização em massa é adquirido durante a operação de carregamento em massa, caso contrário, um bloqueio no nível de linha é adquirido. Essa dica melhora significativamente o desempenho porque manter um bloqueio durante a operação de cópia em massa reduz a contenção de bloqueios na tabela. Uma tabela pode ser carregada simultaneamente por vários clientes se a tabela não tiver nenhum índice e **TABLOCK** for especificado. Por padrão, o comportamento de bloqueio é determinado pela opção de tabela **bloqueio de tabela em carregamento em massa**.  
  
 CHECK_CONSTRAINTS  
 Especifica que todas as restrições na tabela ou exibição de destino devem ser verificadas durante a operação de importação em massa. Sem a dica CHECK_CONSTRAINTS, todas as restrições CHECK e FOREIGN KEY são ignoradas e, depois da operação, a restrição na tabela é marcada como não confiável.  
  
> [!NOTE]  
>  As restrições UNIQUE, PRIMARY KEY e NOT NULL são sempre impostas.  
  
 Em algum momento, você precisará verificar as restrições em toda a tabela. Se a tabela não estava vazia antes da operação de importação em massa, o custo de revalidação da restrição poderá exceder o custo da aplicação de restrições CHECK aos dados incrementais. Portanto, recomendamos que normalmente você habilite a verificação de restrições durante uma importação incremental em massa.  
  
 Uma situação na qual talvez você queira desabilitar as restrições (o comportamento padrão) é quando os dados de entrada contiverem linhas que violam as restrições. Com as restrições CHECK desabilitadas, é possível importar os dados e usar instruções [!INCLUDE[tsql](../includes/tsql-md.md)] para remover os dados inválidos.  
  
> [!NOTE]  
>  o **bcp** agora impõe a validação de dados e as verificações de dados que podem causar falhas nos scripts se eles forem executados em dados inválidos em um arquivo de dados.  
  
> [!NOTE]  
>  A opção **-m** _max_errors_ não se aplica à verificação de restrição.  
  
 FIRE_TRIGGERS  
 Especificado com o argumento **in** , todos os gatilhos de inserção definidos na tabela de destino serão executados durante a operação de cópia em massa. Se FIRE_TRIGGERS não for especificado, nenhum gatilho de inserção será executado. FIRE_TRIGGERS é ignorado para os argumentos **out**, **queryout**e **format** .  
  
 **-i** _input_file_  
 Especifica o nome de um arquivo de resposta, que contém as respostas às perguntas de prompt de comando para cada campo de dados quando uma cópia em massa está sendo executada usando o `-c`modo `-w`interativo (**-n**,, ou **-n** não especificado).  
  
 Se *input_file* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-i** e o valor *input_file* .  
  
 **-k**  
 Especifica que colunas vazias devem reter um valor nulo durante a operação, em vez de qualquer valor padrão nas colunas inseridas. Para obter mais informações, veja [Manter valores nulos ou usar os valores padrão durante a importação em massa &#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 **-K** _application_intent_  
 Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. O único valor possível é **ReadOnly**. Se **-K** não for especificado, o utilitário bcp não oferecerá suporte à conectividade a uma réplica secundária em um grupo de disponibilidade AlwaysOn. Para obter mais informações, consulte secundários [ativos: réplicas secundárias legíveis (grupos de disponibilidade AlwaysOn)](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 **-L** _last_row_  
 Especifica o número da última linha a ser exportada de uma tabela ou importada de um arquivo de dados. Esse parâmetro requer um valor maior que (>) 0, mas menor que\<() ou igual a (=) o número da última linha. Na ausência desse parâmetro, o padrão é a última linha do arquivo.  
  
 *last_row* pode ser um inteiro positivo com um valor de até 2 ^ 63-1.  
  
 **-m** _max_errors_  
 Especifica o número máximo de erros de sintaxe que podem ocorrer antes que a operação **bcp** seja cancelada. Um erro de sintaxe implica em um erro de conversão de dados para o tipo de dados de destino. O total de *max_errors* exclui todos os erros que podem ser detectados apenas no servidor, como violações de restrição.  
  
 Uma linha que não possa ser copiada pelo utilitário **bcp** é ignorada e contada como um erro. Se essa opção não estiver incluída, o padrão será 10.  
  
> [!NOTE]  
>  A opção **-m** também não se aplica à conversão dos `money` tipos `bigint` de dados ou.  
  
 **-n**  
 Executa a operação de cópia em massa usando os tipos de dados nativos (banco de dados) dos dados. Essa opção não solicita informações para cada campo; ela usa os valores nativos.  
  
 Para obter mais informações, veja [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).  
  
 **-N**  
 Executa a operação de cópia em massa usando os tipos de dados nativos (banco de dados) dos dados para dados de não caractere e caracteres Unicode para dados de caractere. Essa opção oferece um desempenho mais elevado alternativo à opção `-w` e deve ser usada para transferir dados de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para outra usando um arquivo de dados. Ela não solicita informações para cada campo. Use essa opção quando estiver transferindo dados que contenham caracteres ANSI estendidos e quiser aproveitar o desempenho do modo nativo.  
  
 Para obter mais informações, veja [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).  
  
 Se você exportar e importar dados para o mesmo esquema de tabela usando bcp. exe com **-N**, você poderá ver um aviso de truncamento se houver uma coluna de caracteres não Unicode de comprimento fixo (por exemplo, `char(10)`).  
  
 O aviso pode ser ignorado. Uma maneira de resolver este aviso é usar **-n** em vez de **-N**.  
  
 **-o** _output_file_  
 Especifica o nome de um arquivo que recebe a saída redirecionada do prompt de comando.  
  
 Se *output_file* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-o** e o valor *output_file* .  
  
 **-P** _senha_  
 Especifica a senha para a ID de logon. Se essa opção não for usada, o comando **bcp** solicitará uma senha. Se essa opção for usada ao término do prompt de comando sem uma senha, o **bcp** usará a senha padrão (NULL).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]  
  
 Para mascarar a senha, não especifique a opção **-P** juntamente com a opção **-U** . Em vez disso, depois de especificar o **bcp** junto com a opção **-U** e outras opções (não especificar **-P**), pressione ENTER e o comando solicitará uma senha. Esse método garante que sua senha será mascarada quando for inserida.  
  
 Se *password* começar com um hífen (-) ou uma barra (/), não adicione um espaço entre **-P** e o valor *password* .  
  
 `-q`  
 Executa a instrução SET QUOTED_IDENTIFIERS ON na conexão entre o utilitário **bcp** e uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Use essa opção para especificar um nome de banco de dados, proprietário, tabela ou exibição que contenha um espaço ou aspas simples. Inclua todo o nome da tabela de três partes ou da exibição entre aspas duplas ("").  
  
 Para especificar um nome de banco de dados que contenha um espaço ou aspas simples, você deve usar a opção **-q**.  
  
 
  `-q` não se aplica a valores passados para `-d`.  
  
 Para obter mais informações, consulte Comentários posteriormente neste tópico.  
  
 **-r** _row_term_  
 Especifica o terminador de linha. O padrão é **\n** (caractere de nova linha). Use esse parâmetro para substituir o terminador de linha padrão. Para obter mais informações, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 Se você especificar o terminador de linha em notação hexadecimal em um comando bcp.exe, o valor será truncado em 0x00. Por exemplo, se você especificar 0x410041, 0x41 será usado.  
  
 Se *row_term* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre **-r** e o valor *row_term* .  
  
 **-R**  
 Especifica que dados de moeda, data e horário são copiados em massa no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o formato regional definido para as configurações de localidade do computador cliente. Por padrão, as configurações regionais são ignoradas.  
  
 **-S** _server_name_[ **\\** _instance_name_]  
 Especifica uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à qual se conectar. Se nenhum servidor for especificado, o utilitário **bcp** se conectará à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador local. Essa opção é requerida quando um comando **bcp** é executado de um computador remoto na rede ou de uma instância local nomeada. Para se conectar à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um servidor, especifique apenas *server_name*. Para se conectar a uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], especifique *server_name**_\\_** instance_name*.  
  
 `-t`*field_term*  
 Especifica o terminador de campo. O padrão é **\t** (caractere de tabulação). Use esse parâmetro para substituir o terminador de campo padrão. Para obter mais informações, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 Se você especificar o terminador de campo em notação hexadecimal em um comando bcp.exe, o valor será truncado em 0x00. Por exemplo, se você especificar 0x410041, 0x41 será usado.  
  
 Se *field_term* começar com um hífen (-) ou uma barra (/), não inclua um espaço entre `-t` e o valor de *field_term* .  
  
 **-T**  
 Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. As credenciais de segurança do usuário de rede, *login_id*e *password* não são necessárias. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para que o logon tenha êxito.  
  
 **-U** _login_id_  
 Especifica a ID de logon usada para conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Quando o utilitário **bcp** estiver se conectando ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada, use a opção **-T** (conexão confiável) em vez da combinação *user name* e *password* .  
  
 **-v**  
 Relata o número de versão e os direitos autorais do utilitário **bcp** .  
  
 **-V** (**80** | **90** | **100**| **110**)  
 Executa a operação de cópia em massa usando tipos de dados de uma versão anterior do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Essa opção não solicita informações para cada campo; ela usa os valores padrão.  
  
 **80** = [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]  
  
 **90** = [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]  
  
 **** =  100[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
  
 **110 =[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]**  
  
 Por exemplo, para gerar dados para tipos sem suporte no [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)], mas que foram incorporados nas versões posteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use a opção -V80.  
  
 Para obter mais informações, consulte [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
 `-w`  
 Executa a operação de cópia em massa usando caracteres Unicode. Essa opção não solicita cada campo; Ele usa `nchar` como o tipo de armazenamento, sem prefixos, **\t** (caractere de tabulação) como separador de campo e **\n** (caractere de nova linha) como terminador de linhas. 
  `-w` não é compatível com `-c`.  
  
 Para obter mais informações, consulte [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).  
  
 **-x**  
 Usado com as opções **format** e **-f**_format_file_ , gera um arquivo de formato baseado em XML em vez do arquivo de formato não XML padrão. O **-x** não funciona ao importar ou exportar dados. Ele gera um erro se for usado sem **format** nem **-f**_format_file_.  
  
## <a name="remarks"></a>Comentários  
 O cliente **bcp** 12,0 é instalado quando você instala [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] as ferramentas do. Se as ferramentas forem instaladas para o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e para uma versão anterior do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], dependendo do valor na variável de ambiente PATH, você poderá estar usando o cliente **bcp** anterior em vez do cliente **bcp** 12.0. Essa variável de ambiente define o conjunto de diretórios usado pelo Windows para pesquisar por arquivos executáveis. Para descobrir qual versão você está usando, execute o comando **bcp /v** no Prompt de Comando do Windows. Para obter mais informações sobre como definir o caminho de comando na variável de ambiente PATH, consulte a Ajuda do Windows.  
  
 Os arquivos de formato XML só têm suporte quando as ferramentas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] são instaladas junto com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client.  
  
 Para obter mais informações sobre onde encontrar ou como executar o utilitário **bcp** e sobre as convenções de sintaxe dos utilitários de prompt de comando, confira [Referência de utilitário de linha de comando &#40;Mecanismo de Banco de Dados&#41;](../tools/command-prompt-utility-reference-database-engine.md).  
  
 Para obter informações sobre como preparar dados para importar ou exportar operações em massa, veja [Preparar dados para exportar ou importar em massa &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 Para obter informações sobre quando as operações de inserção de linhas executadas por importações em massa são registradas no log de transações, veja [Pré-requisitos para log mínimo em importação em massa](../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
## <a name="native-data-file-support"></a>Suporte de arquivos de dados nativos  
 No [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], o **utilitário bcp** dá suporte a arquivos de dados [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]nativos [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]compatíveis [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]com [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)],, [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], e.  
  
## <a name="computed-columns-and-timestamp-columns"></a>Colunas computadas e colunas de carimbo de data/hora  
 Os valores no arquivo de dados sendo para computado ou colunas `timestamp` são ignorados e o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] atribui valores automaticamente. Se o arquivo de dados não contiver valores para as colunas computadas ou de `timestamp` na tabela, use um arquivo de formato para especificar que as colunas computadas ou de `timestamp` na tabela devem ser ignoradas ao importar dados; o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] automaticamente atribuirá valores para a coluna.  
  
 Colunas computadas e de `timestamp` são copiadas em massa do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um arquivo de dados, como sempre.  
  
## <a name="specifying-identifiers-that-contain-spaces-or-quotation-marks"></a>Especificando identificadores que contêm espaços ou aspas  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podem incluir caracteres como espaços inseridos e aspas. Tais identificadores devem ser tratados do seguinte modo:  
  
-   Quando você especificar um identificador ou nome de arquivo que inclua um espaço ou aspas no prompt de comando, coloque o identificador entre aspas ("").  
  
     Por exemplo, o comando `bcp out` a seguir cria um arquivo de dados nomeado `Currency Types.dat`:  
  
    ```  
    bcp AdventureWorks2012.Sales.Currency out "Currency Types.dat" -T -c  
    ```  
  
-   Para especificar um nome de banco de dados que contenha um espaço ou aspas, você deve usar a opção `-q`.  
  
-   Para nomes de proprietário, tabela ou exibição que contenham espaços inseridos ou aspas, você também pode:  
  
    -   Especificar a opção `-q` ou  
  
    -   Inserir o nome de proprietário, tabela ou exibição entre colchetes ([]) dentro das aspas.  
  
## <a name="data-validation"></a>Validação de dados  
 o **bcp** agora impõe a validação de dados e as verificações de dados que podem causar falhas nos scripts se eles forem executados em dados inválidos em um arquivo de dados. Por exemplo, o **bcp** agora verifica se:  
  
-   A representação nativa de tipos de dados `float` ou `real` é válida.  
  
-   Dados Unicode têm um comprimento regular de byte.  
  
 Formas de dados inválidos que podiam ser importadas em massa em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podem falhar ao serem carregadas agora; enquanto em versões anteriores a falha só ocorria quando um cliente tentava acessar os dados inválidos. A validação adicional minimiza as surpresas ao consultar os dados depois do carregamento em massa.  
  
## <a name="bulk-exporting-or-importing-sqlxml-documents"></a>Exportando ou importando documentos SQLXML em massa  
 Para exportar ou importar dados SQLXML em massa, use um dos tipos de dados a seguir em seu arquivo de formato.  
  
|Tipo de dados|Efeito|  
|---------------|------------|  
|SQLCHAR ou SQLVARYCHAR|Os dados são enviados na página de código do cliente ou na página de código implicada pela ordenação. O efeito é o mesmo que especificar a opção `-c` sem especificar um arquivo de formato.|  
|SQLNCHAR ou SQLNVARCHAR|Os dados são enviados como Unicode. O efeito é o mesmo que especificar a opção `-w` sem especificar um arquivo de formato.|  
|SQLBINARY ou SQLVARYBIN|Os dados são enviados sem qualquer conversão.|  
  
## <a name="permissions"></a>Permissões  
 Uma operação **bcpout** exige a permissão SELECT na tabela de origem.  
  
 Uma operação **bcpin** exige, no mínimo, as permissões SELECT/INSERT na tabela de destino. Além disso, a permissão ALTER TABLE será necessária se qualquer das seguintes afirmações for verdadeira:  
  
-   Existem restrições e a dica CHECK_CONSTRAINTS não foi especificada.  
  
    > [!NOTE]  
    >  Desabilitar restrições é o comportamento padrão. Para habilitar restrições explicitamente, use a opção **-h** com a dica CHECK_CONSTRAINTS.  
  
-   Existem gatilhos e a dica FIRE_TRIGGER não foi especificada.  
  
    > [!NOTE]  
    >  Por padrão, os gatilhos não são disparados. Para disparar gatilhos explicitamente, use a opção **-h** com a dica FIRE_TRIGGERS.  
  
-   Use a opção **-E** para importar valores de identidade de um arquivo de dados.  
  
> [!NOTE]  
>  A exigência da permissão ALTER TABLE na tabela de destino era nova no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]. Essa nova exigência pode provocar falha em scripts **bcp** que não impõem verificações de gatilhos e de restrições se a conta do usuário não tiver permissões ALTER TABLE para a tabela de destino.  
  
## <a name="character-mode--c-and-native-mode--n-best-practices"></a>Práticas recomendadas de modo de caractere (-c) e modo nativo (-n)  
 Esta seção apresenta recomendações para modo de caractere (-c) e modo nativo (-n).  
  
-   (Administrador/Usuário) Quando possível, use o formato nativo (-n) para evitar o problema de separador. Use o formato nativo para exportar e importar com o uso do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Exporte dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o uso da opção -c ou -w se os dados serão importados para um banco de dados do[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   (Administrador) Verifique dados ao usar BCP OUT. Por exemplo, quando você usa BCP OUT, BCP IN e, em seguida, BCP OUT, verifique se os dados são exportados corretamente e se os valores de terminador não são usados como parte de algum valor de dados. Considere substituir os terminadores padrão (com as opções -t e -r) com valores hexadecimais aleatórios para evitar conflitos entre valores de terminadores e os valores de dados.  
  
-   (Usuário) Use um terminador longo e exclusivo (qualquer sequência de bytes ou de caracteres) para minimizar a possibilidade de um conflito com o valor da cadeia de caracteres real. Isso pode ser feito com as opções -t e -r.  
  
## <a name="examples"></a>Exemplos  
 Esta seção contém os seguintes exemplos:  
  
-   a. Copiando linhas de tabela em um arquivo de dados (com uma conexão confiável)  
  
-   B. Copiando linhas de tabela em um arquivo de dados (com autenticação mista)  
  
-   C. Copiando dados de um arquivo em uma tabela  
  
-   D. Copiando uma coluna específica em um arquivo de dados  
  
-   E. Copiando uma linha específica em um arquivo de dados  
  
-   F. Copiando dados de uma consulta em um arquivo de dados  
  
-   G. Criando um arquivo de formato não XML  
  
-   H. Criando um arquivo de formato XML  
  
-   I. Usando um arquivo de formato para importação em massa com **bcp**  
  
### <a name="a-copying-table-rows-into-a-data-file-with-a-trusted-connection"></a>a. Copiando linhas de tabela em um arquivo de dados (com uma conexão confiável)  
 O exemplo a seguir ilustra a opção **out** na tabela `AdventureWorks2012.Sales.Currency` . Este exemplo cria um arquivo de dados nomeado `Currency.dat` e copia os dados da tabela nesse arquivo usando formato de caractere. O exemplo presume que você esteja usando a Autenticação do Windows e tenha uma conexão confiável com a instância do servidor na qual está executando o comando **bcp** .  
  
 No prompt de comando, digite o seguinte comando:  
  
```  
bcp AdventureWorks2012.Sales.Currency out Currency.dat -T -c  
```  
  
### <a name="b-copying-table-rows-into-a-data-file-with-mixed-mode-authentication"></a>B. Copiando linhas de tabela em um arquivo de dados (com autenticação mista)  
 O exemplo a seguir ilustra a opção **out** na tabela `AdventureWorks2012.Sales.Currency` . Este exemplo cria um arquivo de dados nomeado `Currency.dat` e copia os dados da tabela nesse arquivo usando formato de caractere.  
  
 O exemplo pressupõe que você esteja usando autenticação mista; é necessário usar a opção **-U** para especificar sua ID de logon. Além disso, a menos que você esteja se conectando à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador local, use a opção **-S** para especificar o nome do sistema e, opcionalmente, um nome de instância.  
  
```  
bcp AdventureWorks2012.Sales.Currency out Currency.dat -c -U<login_id> -S<server_name\instance_name>  
```  
  
 O sistema solicitará sua senha.  
  
### <a name="c-copying-data-from-a-file-to-a-table"></a>C. Copiando dados de um arquivo em uma tabela  
 O exemplo a seguir ilustra a opção **in** usando o arquivo criado no exemplo anterior (`Currency.dat`). Porém, primeiro este exemplo cria uma cópia vazia da tabela `AdventureWorks2012 Sales.Currency`, `Sales.Currency2` na qual os dados são copiados. O exemplo presume que você esteja usando a Autenticação do Windows e tenha uma conexão confiável com a instância do servidor na qual está executando o comando **bcp** .  
  
 Para criar a tabela vazia, execute o seguinte código no Editor de Consultas:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO AdventureWorks2012.Sales.Currency2   
FROM AdventureWorks2012.Sales.Currency WHERE 1=2;  
```  
  
 Para copiar em massa os dados de caractere na nova tabela, isto é, para importar os dados, insira o comando a seguir no prompt de comando:  
  
```  
bcp AdventureWorks2012.Sales.Currency2 in Currency.dat -T -c  
```  
  
 Para verificar se o comando teve sucesso, exiba o conteúdo da tabela no Editor de Consultas e digite:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM Sales.Currency2  
```  
  
### <a name="d-copying-a-specific-column-into-a-data-file"></a>D. Copiando uma coluna específica em um arquivo de dados  
 Para copiar uma coluna específica, você pode usar a opção **queryout** . O exemplo a seguir copia apenas a coluna `Name` da tabela `Sales.Currency` em um arquivo de dados. O exemplo presume que você esteja usando a Autenticação do Windows e tenha uma conexão confiável com a instância do servidor na qual está executando o comando **bcp** .  
  
 No prompt de comando do Windows, digite:  
  
```  
bcp "SELECT Name FROM AdventureWorks.Sales.Currency" queryout Currency.Name.dat -T -c  
```  
  
### <a name="e-copying-a-specific-row-into-a-data-file"></a>E. Copiando uma linha específica em um arquivo de dados  
 Para copiar uma linha específica, você pode usar a opção **queryout** . O exemplo a seguir copia somente a linha do contato chamado `Jarrod Rana` da tabela `AdventureWorks2012.Person.Person` em um arquivo de dados (`Jarrod Rana.dat`). O exemplo presume que você esteja usando a Autenticação do Windows e tenha uma conexão confiável com a instância do servidor na qual está executando o comando **bcp**.  
  
 No prompt de comando do Windows, digite:  
  
```  
bcp "SELECT * FROM AdventureWorks2012.Person.Person WHERE FirstName='Jarrod' AND LastName='Rana' "  queryout "Jarrod Rana.dat" -T -c  
```  
  
### <a name="f-copying-data-from-a-query-to-a-data-file"></a>F. Copiando dados de uma consulta em um arquivo de dados  
 Para copiar o conjunto de resultados de uma instrução [!INCLUDE[tsql](../includes/tsql-md.md)] em um arquivo de dados, use a opção **queryout** . O exemplo a seguir copia os nomes da tabela `AdventureWorks2012.Person.Person` , classificados pelo sobrenome e depois pelo prenome, no arquivo de dados `Contacts.txt` . O exemplo presume que você esteja usando a Autenticação do Windows e tenha uma conexão confiável com a instância do servidor na qual está executando o comando **bcp** .  
  
 No prompt de comando do Windows, digite:  
  
```  
bcp "SELECT FirstName, LastName FROM AdventureWorks2012.Person.Person ORDER BY LastName, Firstname" queryout Contacts.txt -c -T  
```  
  
### <a name="g-creating-a-non-xml-format-file"></a>G. Criando um arquivo de formato não XML  
 O exemplo a seguir cria um arquivo de formato não XML, `Currency.fmt`, para a tabela `Sales.Currency` no banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]. O exemplo presume que você esteja usando a Autenticação do Windows e tenha uma conexão confiável com a instância do servidor na qual está executando o comando **bcp** .  
  
 No prompt de comando do Windows, digite:  
  
```  
bcp AdventureWorks2012.Sales.Currency format nul -T -c  -f Currency.fmt  
```  
  
 Para obter mais informações, veja [Arquivos de formato não XML &#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md).  
  
### <a name="h-creating-an-xml-format-file"></a>H. Criando um arquivo de formato XML  
 O exemplo a seguir cria um arquivo de formato XML nomeado `Currency.xml` para a tabela `Sales.Currency` no banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . O exemplo presume que você esteja usando a Autenticação do Windows e tenha uma conexão confiável com a instância do servidor na qual está executando o comando **bcp** .  
  
 No prompt de comando do Windows, digite:  
  
```  
bcp AdventureWorks2012.Sales.Currency format nul -T -c -x -f Currency.xml  
```  
  
> [!NOTE]  
>  Para usar a opção **-x** , é necessário estar usando um cliente **bcp** 9.0. Para obter informações sobre como usar o cliente **bcp** 9,0, consulte "Comentários".  
  
 Para obter mais informações, veja [Arquivos de formato XML &#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md).  
  
### <a name="i-using-a-format-file-to-bulk-import-with-bcp"></a>I. Usando um arquivo de formato para importação em massa com bcp  
 Para usar um arquivo de formato criado anteriormente ao importar dados para uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use a opção **-f** com a opção **in** . Por exemplo, o comando a seguir copia em massa os conteúdos de um arquivo de dados, `Currency.dat`, em uma cópia da tabela `Sales.Currency` (`Sales.Currency2`) usando o arquivo de formato criado anteriormente (`Currency.xml`). O exemplo presume que você esteja usando a Autenticação do Windows e tenha uma conexão confiável com a instância do servidor na qual está executando o comando **bcp** .  
  
 No prompt de comando do Windows, digite:  
  
```  
bcp AdventureWorks2012.Sales.Currency2 in Currency.dat -T -f Currency.xml  
```  
  
> [!NOTE]  
>  Os arquivos de formato são úteis quando os campos do arquivo de dados são diferentes das colunas da tabela, por exemplo, em seu número, classificação ou tipos de dados. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="additional-examples"></a>Exemplos adicionais  
 Os tópicos a seguir contêm exemplos sobre como usar o **bcp**:  
  
-   [Criar um arquivo de formato &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Preparar dados para exportação ou importação em massa &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [DEFINIR QUOTED_IDENTIFIER &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-quoted-identifier-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql)   
 [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
