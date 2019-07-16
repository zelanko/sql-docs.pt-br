---
title: dwloader carregador de linha de comando - Parallel Data Warehouse | Microsoft Docs
description: dwloader é uma ferramenta de linha de comando do Parallel Data Warehouse (PDW) que carrega linhas da tabela em massa em uma tabela existente.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: dd3f005346c5faae9e02513a144d04d80857b770
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961024"
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>Carregador de linha de comando para Parallel Data Warehouse de dwloader
**dwloader** é uma ferramenta de linha de comando do Parallel Data Warehouse (PDW) que carrega linhas da tabela em massa em uma tabela existente. Quando o carregamento de linhas, você pode adicionar todas as linhas ao final da tabela (*modo de acréscimo* ou *modo fastappend*), acrescentar novas linhas e atualizar as linhas existentes (*modo upsert*), ou excluir todos linhas antes do carregamento de existente e, em seguida, inserir todas as linhas em uma tabela vazia (*recarregar modo*).  
  
**Processo de carregamento de dados**  
  
1.  Prepare os dados de origem.  
  
    Use seu próprio processo ETL para criar a fonte de dados que deseja carregar. Os dados de origem devem ser formatados de acordo com o esquema da tabela de destino. Store a fonte de dados em um ou mais arquivos de texto e copie os arquivos de texto no mesmo diretório em seu servidor de carregamento. Para obter informações sobre o servidor de carregamento, consulte [adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md)  
  
2.  Prepare-se as opções de carregamento.  
  
    Decida quais opções de carregamento que será usado. Store as opções de carregamento em um arquivo de configuração. Copie o arquivo de configuração para uma localização local no seu servidor de carregamento. O **dwloader** opções de configuração são descritas neste tópico.  
  
3.  Prepare-se a carga de opções de falha.  
  
    Decidir como deseja **dwloader** para lidar com linhas com Falha ao carregar. Para executar o carregamento **dwloader** primeiro carrega os dados em uma tabela de preparo e, em seguida, transfere os dados para a tabela de destino. Como o carregador carrega dados na tabela de preparo, ele controla o número de linhas que falham ao carregar. Por exemplo, linhas que não estão formatadas corretamente falhará ao carregar. Linhas com falha são copiadas para um arquivo de rejeição. Por padrão, a carga será anulada após a rejeição primeiro, a menos que você especifica um limite de rejeição diferentes.  
  
4.  Instale **dwloader**.  
  
    Se já não estiver instalado, instale dwloader no servidor de carregamento. 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  Execute **dwloader**.  
  
    Entre servidor de carregamento e execute o executável **dwloader.exe** com as opções de linha de comando apropriadas.  
  
6.  Verifique se os resultados.  
  
    Você pode verificar as linhas do arquivo (especificado com -R) para ver se todas as linhas não pôde ser carregado. Se esse arquivo estiver vazio, todas as linhas carregado com êxito. **dwloader** é transacional, portanto, se qualquer etapa falhar (em vez de linhas rejeitadas), todas as etapas reverterá ao estado inicial.  
  
<!-- 
![Topic link icon](media/topic-link.gif "Topic_Link")[Syntax Conventions](syntax-conventions-sql-server-pdw.md)  
-->  


## <a name="syntax"></a>Sintaxe  
  
```  
dwloader.exe { -h }  
  
dwloader.exe   
    {  
        { -U login_name  -P password  }  
        | -W  
    }  
    [ -f parameter_file ]  
    [ -S target_appliance ]  
    { -T target_database_name . [ schema ] . table_name }   
    { -i source_data_location } [ <source_data_options> ]  
    { -R load_failure_file_name } [ <load_failure_options> ]  
    [ <loading_options> ]  
}  
  
<source_data_options> ::=  
{  
    [ -fh number_header_rows ]  
    [ < variable_length_column_options > | < fixed_width_column_options > ]  
    [ -D { mdy | myd | ymd | ydm | dmy | dym | custom_date_format } ]  
    [ -dt datetime_format_file ]  
}  
  
<variable_length_column_options> ::=  
{  
    [ -e character_encoding ]  
    -r row_delimiter   
    [ -s string_delimiter ]  
    -t field_delimiter   
}  
  
<fixed_width_column_options> ::=  
{  
    -w fixed_width_config_file   
    [ -e character_encoding ]   
    -r row_delimiter   
}  
  
<load_failure_options> ::=  
{  
    [ -rt { value | percentage } ]  
    [ -rv reject_value ]  
    [ -rs reject_sample_value ]  
}  
  
<loading_options> ::=  
{  
    [ -d staging_database_name ]  
    [ -M { append | fastappend | upsert -K merge_column [ ,...n ] | reload } ]  
    [ -b batchsize ]   
    [ -c ]  
    [ -E ]  
    [ -m ]  
    [ -N ]  
    [ -se ]
    [ -l ]   
}  
```  
  
## <a name="arguments"></a>Argumentos  
**-h**  
Exibe informações de Ajuda simples sobre como usar o carregador. Ajuda exibe somente se nenhum outro parâmetro de linha de comando forem especificado.  
  
**-U** *login_name*  
Um logon válido de autenticação do SQL Server com permissões apropriadas para executar a carga.  
  
**-P** *password*  
A senha para autenticação do SQL Server *login_name*.  
  
**-W**  
Use a Autenticação do Windows. (Não *login_name* ou *senha* necessária.) 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
Usar um arquivo de parâmetro *parameter_file_name*, no lugar de parâmetros de linha de comando. *parameter_file_name* pode conter qualquer parâmetro de linha de comando, exceto *user_name* e *senha*. Se um parâmetro for especificado na linha de comando e no arquivo de parâmetros, a linha de comando substitui o parâmetro de arquivo.  
  
O arquivo de parâmetros contém um parâmetro, sem a **-** prefixo, por linha.  
  
Exemplos:  
  
`rt=percentage`  
  
`rv=25`  
  
* *-S***target_appliance*  
Especifica o dispositivo de PDW do SQL Server que receberá os dados carregados.  
  
*Para conexões do Infiniband*, *target_appliance* é especificado como o < nome do dispositivo >-SQLCTL01. Para configurar isso é chamado de conexão, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).  
  
Para conexões de Ethernet *target_appliance* é o endereço IP para o cluster de nó de controle.  
  
Se omitido, dwloader padrão será o valor que foi especificado quando dwloader foi instalado. 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.* [*schema*].*table_name*  
O nome de três partes para a tabela de destino.  
  
* *-I***source_data_location*  
O local dos arquivos de origem de um ou mais para carregar. Cada arquivo de origem deve ser um arquivo de texto ou um arquivo de texto compactados com gzip. Apenas um arquivo de origem pode ser compactado em cada arquivo gzip.  
  
Para formatar um arquivo de origem:  
  
-   O arquivo de origem deve ser formatado de acordo com as opções de carregamento.  
  
-   Cada linha em um arquivo de origem contém os dados de linha de uma tabela. Os dados de origem devem corresponder ao esquema da tabela de destino. Tipos de dados e a ordem de coluna também devem corresponder. Cada campo na linha representa uma coluna na tabela de destino.  
  
-   Por padrão, os campos são de comprimento variável e separados por um delimitador. Para especificar o tipo de delimitador, use as opções de linha de comando < variable_length_column_options >. Para especificar os campos de comprimento fixo, use as opções de linha de comando < fixed_width_column_options >.  
  
Para especificar o local de dados de origem:  
  
-   O local de dados de origem pode ser um caminho de rede ou um caminho local para um diretório no servidor de carregamento.  
  
-   Para especificar todos os arquivos em um diretório, digite o caminho do diretório seguido de * caractere curinga.  O carregador não carrega arquivos de todos os subdiretórios que estão no local de dados de origem. Os erros de carregador quando existe um diretório em um arquivo gzip.  
  
-   Para especificar alguns dos arquivos em um diretório, use uma combinação de caracteres e o * curinga.  
  
Para carregar vários arquivos com um único comando:  
  
-   Todos os arquivos devem existir no mesmo diretório.  
  
-   Os arquivos devem ser todos os arquivos de texto, todos os arquivos gzip ou uma combinação de arquivos de texto e gzip.  
  
-   Nenhum dos arquivos pode conter informações de cabeçalho.  
  
-   Todos os arquivos devem usar o mesmo tipo de codificação de caractere. Consulte a opção -e.  
  
-   Todos os arquivos devem ser carregados na mesma tabela.  
  
-   Todos os arquivos serão concatenados e carregados como se eles são um arquivo, e as linhas rejeitadas entrará em um arquivo único de rejeição.  
  
Exemplos:  
  
-   -i \\\loadserver\loads\daily\\*.gz  
  
-   -i \\\loadserver\loads\daily\\*. txt  
  
-   -i \\\loadserver\loads\daily\monday.*  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
Se houver falhas de carregamento **dwloader** armazena a linha que falhou, a carga e a descrição de falha, as informações de falha em um arquivo chamado *load_failure_file_name*. Se esse arquivo já existir, dwloader substituirá o arquivo existente. *load_failure_file_name* é criado quando a primeira falha ocorre. Se todas as linhas com êxito, carregam *load_failure_file_name* não é criado.  
  
**-fh** *number_header_rows*  
O número de linhas (linhas) para ignorar no início da *source_data_file_name*. O padrão é 0.  
  
<variable_length_column_options>  
As opções para um *source_data_file_name* que tem colunas delimitada por caracteres de comprimento variável. Por padrão, *source_data_file_name* contém caracteres ASCII em colunas de comprimento variável.  
  
Para arquivos ASCII, valores nulos são representados por colocar delimitadores consecutivamente. Por exemplo, em um arquivo delimitado por pipe ("|"), um valor nulo é indicado por "| |". Em um arquivo delimitado por vírgula, um valor nulo é indicado por ",". Além disso, o **-E** (– emptyStringAsNull) opção deve ser especificada. Para obter mais informações sobre -E, consulte abaixo.  
  
**-e** *character_encoding*  
Especifica um tipo de codificação de caracteres para os dados a serem carregadas do arquivo de dados. As opções são ASCII (padrão), UTF8, UTF16 ou UTF16BE, onde UTF16 é pouco endian e UTF16BE for big endian. Essas opções diferenciam maiusculas de minúsculas.  
  
**-t** *field_delimiter*  
O delimitador para cada campo (coluna) na linha. O delimitador de campo é um ou mais desses caracteres de escape de ASCII ou valores de hex ASCII.  
  
|Nome|Caractere de escape|Caractere hexadecimal|  
|--------|--------------------|-----------------|  
|Tabulação|\t|0x09|  
|Retorno de carro (CR)|\r|0x0D|  
|Alimentação de linha (LF)|\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|Vírgula|','|0x2c|  
|Aspas duplas|\\"|0x22|  
|Aspas simples|\\'|0x27|  
  
Para especificar o caractere de barra vertical na linha de comando, coloque-o entre aspas duplas, com "|". Isso evitará a interpretação errônea pelo analisador de linha de comando. Outros caracteres são colocados entre aspas simples.  
  
Exemplos:  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t ' ~ | ~'  
  
**-r** *row_delimiter*  
O delimitador para cada linha do arquivo de dados de origem. O delimitador de linha é um ou mais valores ASCII.  
  
Para especificar um retorno de carro (CR), a linha (LF) ou o caractere de tabulação como um delimitador, você pode usar os caracteres de escape (\r, \n, \t) ou seus valores hexadecimais (0 x, 0d 09). Para especificar outros caracteres especiais como delimitadores, use seu valor hexadecimal.  
  
Exemplos de CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Exemplos de CR:  
  
-r \r  
  
-r 0x0d  
  
Exemplos de LF:  
  
\n - r  
  
-r 0x0a  
  
Um LF é necessário para Unix. Uma CR é necessária para Windows.  
  
**-s** *string_delimiter*  
O delimitador para dados de cadeia de tipo de campo de um arquivo de entrada de texto delimitado. O delimitador de cadeia de caracteres é um ou mais valores ASCII.  Ele pode ser especificado como um caractere (por exemplo, -s *) ou como um valor hexadecimal (por exemplo, -s 0x22 para aspas duplas).  
  
Exemplos:  
  
-s *  
  
-s 0x22  
  
< fixed_width_column_options>  
As opções para um arquivo de dados de origem que tem colunas de comprimento fixo. Por padrão, *source_data_file_name* contém caracteres ASCII em colunas de comprimento variável.  
  
Não há suporte para colunas de largura fixa quando -e é UTF8.  
  
**-w** *fixed_width_config_file*  
Caminho e nome do arquivo de configuração que especifica o número de caracteres em cada coluna. Cada campo deve ser especificado.  
  
Esse arquivo deve residir no servidor de carregamento. O caminho pode ser um caminho UNC, relativo ou absoluto. Cada linha na *fixed_width_config_file* contém o nome de uma coluna e o número de caracteres para aquela coluna. Há uma linha por coluna, da seguinte maneira e a ordem em que o arquivo deve corresponder à ordem na tabela de destino:  
  
*column_name*=*num_chars*  
  
*column_name*=*num_chars*  
  
Corrigido o arquivo de configuração de largura de exemplo:  
  
SalesCode=3  
  
SalesID=10  
  
Exemplo de linhas no *source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
No exemplo anterior, a primeira linha carregada terá SalesCode = '230' e SalesID = 'Shirts0056'. A linha carregada em segundo lugar terá SalesCode = '320' e SaleID = 'Towels1356'.  
  
Para obter informações sobre como lidar com a esquerda e à direita de conversão de tipo de dados ou espaços no modo de largura fixa, consulte [tipo de dados de regras de conversão para dwloader](dwloader-data-type-conversion-rules.md).  
  
**-e** *character_encoding*  
Especifica um tipo de codificação de caracteres para os dados a serem carregadas do arquivo de dados. As opções são ASCII (padrão), UTF8, UTF16 ou UTF16BE, onde UTF16 é pouco endian e UTF16BE for big endian. Essas opções diferenciam maiusculas de minúsculas.  
  
Não há suporte para colunas de largura fixa quando -e é UTF8.  
  
**-r** *row_delimiter*  
O delimitador para cada linha do arquivo de dados de origem. O delimitador de linha é um ou mais valores ASCII.  
  
Para especificar um retorno de carro (CR), a linha (LF) ou o caractere de tabulação como um delimitador, você pode usar os caracteres de escape (\r, \n, \t) ou seus valores hexadecimais (0 x, 0d 09). Para especificar outros caracteres especiais como delimitadores, use seu valor hexadecimal.  
  
Exemplos de CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Exemplos de CR:  
  
-r \r  
  
-r 0x0d  
  
Exemplos de LF:  
  
\n - r  
  
-r 0x0a  
  
Um LF é necessário para Unix. Uma CR é necessária para Windows.  
  
**-D** { **ymd** | ydm | mdy | myd |  DMY | dym | *custom_date_format* }  
Especifica a ordem de mês (m), (d) do dia e ano (y) para todos os campos de data e hora no arquivo de entrada. A ordem padrão é ymd. Para especificar vários formatos de ordem para o mesmo arquivo de origem, use a opção -dt.  
  
YMD | DMY  
ydm e dmy permitem que os mesmos formatos de entrada. Ambos permitem que o ano a ser no início ou no fim da data. Por exemplo, para ambos **ydm** e **dmy** data formatos, você poderia ter 2013-02-03 ou 02-03-2013 no arquivo de entrada.  
  
ydm  
Você pode carregar apenas entrada formatada como ydm em colunas de dados tipo datetime e smalldatetime. Você não pode carregar ydm valores em uma coluna do tipo de dados datetimeoffset, data ou datetime2.  
  
mda  
permite MDY <month> <space> <day> <comma> <year>.  
  
Exemplos de dados de entrada do MDA para 1 de janeiro de 1975:  
  
-   1 de janeiro de 1975  
  
-   01 de janeiro de 75  
  
-   Jan/1/75  
  
-   01011975  
  
mad  
Exemplos de arquivos de entrada para março 04,2010: 03-2010-04, 3/2010/4  
  
dam  
Exemplos de arquivo de entrada para 04 de março de 2010: 04-2010-03, 4/2010/3  
  
*custom_date_format*  
*custom_date_format* é um formato de data personalizada (por exemplo, MM/dd/aaaa) e incluído para compatibilidade com versões anteriores. dwloader não impõe o formato de data personalizado. Em vez disso, quando você especifica um formato de data personalizado **dwloader** irá convertê-lo para a configuração correspondente de ymd, ydm, mdy, myd, dym ou dmy.  
  
Por exemplo, se você especificar -D MM/dd/aaaa, dwloader espera que todas as data de entrada para serem ordenados em primeiro lugar, com mês e em seguida, dia e ano (DMA). Ele não impõe caracteres de 2 meses, dias de 2 dígitos e anos de 4 dígitos conforme especificado pelo formato de data personalizada. Aqui estão alguns exemplos de como as datas podem ser formatadas no arquivo de entrada quando o formato de data for -D MM/dd/aaaa: 02/01/2013, Jan.02.2013, 2/1/2013  
  
Para obter informações de formatação mais abrangentes, consulte [tipo de dados de regras de conversão para dwloader](dwloader-data-type-conversion-rules.md).  
  
**-dt** *datetime_format_file*  
Cada formato de data e hora é especificado em um arquivo chamado *datetime_format_file*. Ao contrário de parâmetros de linha de comando, parâmetros do arquivo que inclua espaços não devem ser colocados entre aspas duplas. Você não pode alterar o formato de data e hora conforme você carregar dados. O arquivo de dados de origem e sua coluna correspondente na tabela de destino devem ter o mesmo formato.  
  
Cada linha contém o nome de uma coluna na tabela de destino e seu formato de data e hora.  
  
Exemplos:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
O nome do banco de dados que contém a tabela de preparo. O padrão é o banco de dados especificado com a opção -T, que é o banco de dados para a tabela de destino. Para obter mais informações sobre como usar um banco de dados de preparo, consulte [criar o banco de dados de preparo](staging-database.md).  
  
**-M** *load_mode_option*  
Especifica se deve ser acrescentada, upsert, ou recarregar os dados. O modo padrão é acrescentar.  
  
Acrescentar  
O carregador insere linhas no final de linhas existentes na tabela de destino.  
  
fastappend  
O carregador insere linhas diretamente, sem usar uma tabela temporária, até o final de linhas existentes na tabela de destino. fastappend requer que a transação várias (-m) opção. Um banco de dados de preparo não pode ser especificado ao usar fastappend. Não há nenhuma reversão com fastappend, o que significa que a recuperação de uma carga anulada ou com falha deve ser tratada pelo seu próprio processo de carregamento.  
  
upsert **-K**  *merge_column* [ ,...*n* ]  
O carregador usa a instrução de mesclagem do SQL Server para atualizar as linhas existentes e inserir novas linhas.  
  
A opção -K Especifica a coluna ou colunas para basear a mesclagem. Essas colunas formam uma chave de mesclagem, que deve representar uma linha exclusiva. Se a chave de mesclagem existir na tabela de destino, a linha é atualizada. Se a chave de mesclagem não existe na tabela de destino, a linha é acrescentada.  
  
Para tabelas distribuídas por hash, a chave de mesclagem deve ser ou incluir a coluna de distribuição.  
  
Para tabelas replicadas, a chave de mesclagem é a combinação de uma ou mais colunas. Essas colunas são especificadas de acordo com as necessidades do aplicativo.  
  
Várias colunas devem ser separados por vírgulas, sem espaços ou separados por vírgula com os espaços e colocado entre aspas simples.  
  
Se duas linhas na tabela de origem tiverem valores de chave de mesclagem correspondente, suas respectivas linhas devem ser idênticas.  
  
Recarregar  
O carregador trunca a tabela de destino antes de inserir os dados de origem.  
  
**-b** *batchsize*  
Recomendado somente para uso pelo Microsoft Support *batchsize* é o tamanho de lote do SQL Server para a cópia em massa que DMS executa em instâncias do SQL Server em nós de computação.  Quando *batchsize* for especificado, SQL Server PDW substituirá o tamanho de carga de lote é calculado dinamicamente para cada carga.  
  
Começando com o SQL Server 2012 PDW, o nó de controle calcula dinamicamente um tamanho de lote para cada tipo de carga por padrão. Esse cálculo automático baseia-se em vários parâmetros, como o tamanho da memória, tipo de tabela de destino, esquema de tabela de destino, tipo de carga, tamanho do arquivo e classe de recurso do usuário.  
  
Por exemplo, se o modo de carga é FASTAPPEND e a tabela tem um índice columnstore clusterizado, SQL Server PDW será pela tentativa de padrão de usar um tamanho de lote de 1.048.576 para que os rowgroups serão se tornam FECHADOS e carregar diretamente para o columnstore sem passar pelo repositório delta. Se a memória não permite que o tamanho do lote de 1.048.576, dwloader escolherá um tamanho de lote menor.  
  
Se o tipo de carga for FASTAPPEND, o *batchsize* aplica-se a carregar dados para a tabela, caso contrário *batchsize* se aplica a carregar dados para a tabela de preparo.  
  
<reject_options>  
Especifica opções para determinar o número de falhas de carregamento que permitirá que o carregador. Se as falhas de carga excederam o limite, o carregador será interrompida e não confirmar todas as linhas.  
  
**-rt** { **valor** | porcentagem}  
Especifica se o -*reject_value* na **-rv** *reject_value* opção é um literal número de linhas (valor) ou uma taxa de falha (porcentagem). O padrão é o valor.  
  
A opção de porcentagem é um cálculo em tempo real que ocorre em intervalos de acordo com a opção - rs.  
  
Por exemplo, se o carregador tenta carregar 100 linhas e 25 falha e 75 tenha êxito, a taxa de falha é 25%.  
  
**-rv** *reject_value*  
Especifica o número ou percentual de rejeições de linha para permitir que antes de interromper a carga. O **-rt** opção determina se *reject_value* refere-se ao número de linhas ou a porcentagem de linhas.  
  
O padrão *reject_value* é 0.  
  
Quando usado com o valor de -rt, o carregador interrompe a carga quando a contagem de linhas rejeitadas excede reject_value.  
  
Quando usar com a porcentagem -rt, o carregador calcula a porcentagem em intervalos (-opção de rs). Portanto, o percentual de linhas com falha pode exceder *reject_value*.  
  
**-rs** *reject_sample_size*  
Usado com o `-rt percentage` opção para especificar as verificações de porcentagem incremental. Por exemplo, se reject_sample_size é 1000, o carregador calculará o percentual de linhas com falha depois que ele tentou carregar 1000 linhas. Recalcular o percentual de linhas com falha depois de tentar carregar a cada 1.000 linhas adicionais.  
  
**-c**  
Remove caracteres de espaço em branco da esquerda e direita do char, nchar, varchar e nvarchar campos. Converte cada campo que contém somente caracteres de espaço em branco na cadeia de caracteres vazia.  
  
Exemplos:  
  
' ' será truncado para '  
  
'abc' será truncado para 'abc'  
  
Quando -c é usado com -E, a operação de E - ocorre pela primeira vez. Os campos que contêm apenas caracteres de espaço em branco são convertidos para a cadeia de caracteres vazia e não NULL.  
  
**-E**  
Converta cadeias de caracteres vazias em NULL. O padrão é não executar essas conversões.  
  
**-m**  
Use o modo de várias transações para a segunda fase de carregamento; ao carregar os dados da tabela de preparo em uma tabela distribuída.  
  
Com o **-m**, SQL Server PDW executa e confirma os carregamentos em paralelo. Executado muito mais rapidamente do que o padrão ao carregar modo, mas não é seguro de transação.  
  
Sem **-m**, SQL Server PDW executa e confirma o carrega em série entre as distribuições em cada nó de computação e, ao mesmo tempo em todos os nós de computação. Esse método é mais lento do que o modo de transação de várias, mas é seguro de transação.  
  
**-m** é opcional para o *acrescentar*, *recarregar*, e *upsert*.  
  
**-m** é necessária para fastappend.  
  
**-m** não pode ser usado com tabelas replicadas.  
  
**-m** se aplica somente a segunda fase de carregamento. Não é aplicável para a primeira fase de carregamento; Carregando dados na tabela de preparo.  
  
Não há nenhuma reversão com o modo de várias transações, o que significa que a recuperação de uma carga anulada ou com falha deve ser tratada pelo seu próprio processo de carregamento.  
  
É recomendável usar **-m** somente quando o carregamento em uma tabela vazia, para que você possa recuperar sem perda de dados. Para se recuperar de uma falha de carregamento: descarte a tabela de destino, resolva o problema de carga, recriar a tabela de destino e execute a carga novamente.  
  
**-N**  
Verifique se que o dispositivo de destino tem um certificado válido do SQL Server PDW de uma autoridade confiável. Use isso para ajudar a garantir que os dados não estão sendo roubados por um invasor e enviados para um local não autorizado. O certificado já deve estar instalado no dispositivo. A única maneira com suporte para instalar o certificado é para o administrador do dispositivo para instalá-lo usando a ferramenta Configuration Manager. Peça ao seu administrador do dispositivo se você não estiver certo se o dispositivo tem um certificado confiável instalado.  
  
**-se**  
Ignorar carregamento de arquivos vazios. Isso também ignora descompactando arquivos gzip vazio.

**-l**  
Disponível com a atualização CU7.4, especifica o comprimento máximo da linha (em bytes) que pode ser carregado. Os valores válidos são números inteiros entre 32768 e 33554432. Use somente quando necessário para carregar linhas grandes (maiores que 32KB), pois isso será alocar mais memória no cliente e servidor.
  
## <a name="return-code-values"></a>Valores do código de retorno  
0 (êxito) ou outro valor de inteiro (falha)  
  
Em um arquivo de lote ou de janela de comando, use `errorlevel` para exibir o código de retorno. Por exemplo:  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
Ao usar o PowerShell, use `$LastExitCode`.  
  
## <a name="permissions"></a>Permissões  
Requer a permissão de carga e de permissões aplicáveis (INSERT, UPDATE, DELETE) na tabela de destino. Requer a permissão CREATE (para a criação de uma tabela temporária) banco de dados de preparo. Se um banco de dados de preparo não for usado, a permissão CREATE é necessário no banco de dados de destino. 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>Comentários gerais  
Para obter informações sobre conversões de tipo de dados quando o carregamento de dwloader, consulte [tipo de dados de regras de conversão para dwloader](dwloader-data-type-conversion-rules.md).  
  
Se um parâmetro inclui um ou mais espaços, coloque-o parâmetro com aspas duplas.  
  
Você deve executar o carregador do seu local de instalação. O executável de dwloader pré-instalado com o dispositivo e está localizado no diretório C:\Program Files\Microsoft SQL Server Data Warehouse\DWLoader.  
  
Você pode substituir um parâmetro que é especificado no arquivo de parâmetro (-opção f) especificando-o como um parâmetro de linha de comando.  
  
Você pode executar várias instâncias do carregador simultaneamente. O número máximo de instâncias do carregador está pré-configurado e não pode ser alterado. 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
Os dados carregados podem exigir mais ou menos espaço no dispositivo de que no local de origem. Você pode executar importações de teste com subconjuntos de dados para estimar o consumo de disco.  
  
Embora **dwloader** é um processo de transação e reverterá normalmente em caso de falha, ele não poderá ser revertido novamente quando o carregamento em massa foi concluído com êxito. Para cancelar um ativo **dwloader** processar, digite CTRL + C.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
O tamanho total de todos os carregamentos ocorram simultaneamente deve ser menor do que LOG_SIZE para o banco de dados, e recomendamos que o tamanho total de todos os carregamentos simultâneos é menor que 50% a LOG_SIZE. Para obter essa limitação de tamanho, você pode dividir grandes cargas em vários lotes. Para obter mais informações sobre LOG_SIZE, consulte [criar banco de dados](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
Ao carregar vários arquivos com o comando de uma carga, todas as linhas rejeitadas são gravadas no mesmo arquivo de rejeição. O arquivo de rejeição não mostra qual arquivo de entrada contém cada linha rejeitada.  
  
A cadeia de caracteres vazia não deve ser usada como um delimitador. Quando uma cadeia de caracteres vazia é usada como um delimitador de linha, o carregamento falhará. Quando usado como delimitador de coluna, a carga ignora o delimitador e continua a usar o padrão "|" como o delimitador de coluna. Quando usado como delimitador de cadeia de caracteres, cadeia de caracteres vazia será ignorada e o comportamento padrão é aplicado.  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
**dwloader** comportamento de bloqueio varia dependendo do *load_mode_option*.  
  
-   **acrescentar** -anexar é a recomendada e a opção mais comum. Acrescente carrega dados em uma tabela de preparo. O bloqueio é descrito em detalhes abaixo.  
  
-   **Acrescentar Fast** -Fast-acrescentar carrega diretamente na tabela final retirar um bloqueio de tabela ExclusiveUpdate e é o único modo que não usa uma tabela de preparo.  
  
-   **Recarregar** -recarregar carrega dados em uma tabela de preparo e requer um bloqueio exclusivo na tabela de preparo e a tabela final. Recarregar não é recomendado para operações simultâneas.  
  
-   **upsert** -Upsert carrega dados em uma tabela de preparo e, em seguida, executa uma operação de mesclagem da tabela de preparo para a tabela final. Upsert não exige um bloqueio exclusivo na tabela final. O desempenho pode variar ao usar upsert. Teste o comportamento em seu ambiente.  
  
### <a name="locking-behavior"></a>Comportamento de bloqueio  
**Bloqueio de modo de acréscimo**  
  
Acrescentar pode ser executado no modo multi-transacional (usando o argumento -m), mas não é seguro de transação. Acrescentar, portanto, deve ser usado como uma operação transacional (sem usar o argumento -m). Infelizmente, durante a operação INSERT-SELECT final, modo transacional é atualmente aproximadamente seis vezes mais lento do que o modo de vários transacional.  
  
O modo de acréscimo carrega dados em duas fases. A fase um carrega dados do arquivo de origem em uma tabela de preparo simultaneamente (a fragmentação pode ocorrer). Fase dois carrega os dados da tabela de preparo para a tabela final. A segunda fase executa um **INSERT INTO... Selecione WITH (TABLOCK)** operação. A tabela a seguir mostra o comportamento de bloqueio na tabela final e modo de acréscimo ao usar o comportamento de log:  
  
|Tipo de tabela|Transações múltiplas<br />Modo (-m)|Tabela está vazia|Simultaneidade com suporte|Registrando em log|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|Pilha|Sim|Sim|Sim|Mínimo|  
|Pilha|Sim|Não|Sim|Mínimo|  
|Pilha|Não|Sim|Não|Mínimo|  
|Pilha|Não|Não|Não|Mínimo|  
|Cl|Sim|Sim|Não|Mínimo|  
|Cl|Sim|Não|Sim|Completo|  
|Cl|Não|Sim|Não|Mínimo|  
|Cl|Não|Não|Sim|Completo|  
  
Mostra a tabela acima **dwloader** usando o modo de acréscimo carregar em um heap ou uma tabela de índice clusterizado (CI), com ou sem o sinalizador de multi-transacional e carregar em uma tabela vazia ou uma tabela não vazia. O bloqueio e registro em log o comportamento de cada tal combinação de carga é exibido na tabela. Por exemplo, carregando fase (2ª) com o modo de acréscimo em um índice clusterizado sem modo multi-transacional e em um vazio tabela terá PDW criar um bloqueio exclusivo na tabela e registro em log é mínimo. Isso significa que um cliente não poderão carregar (2ª) fase e consulta simultaneamente em uma tabela vazia. No entanto, ao carregar com a mesma configuração em uma tabela não vazia, o PDW não emitirá um bloqueio exclusivo na tabela e a simultaneidade é possível. Infelizmente, registro em log completo ocorre, reduzindo o processo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-dwloader-example"></a>A. Exemplo simples de dwloader  
O exemplo a seguir mostra o início do **carregador** com apenas as opções necessárias selecionadas. Outras opções são retiradas do arquivo de configuração global, *loadparamfile.txt*.  
  
Exemplo usando a autenticação do SQL Server.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
O mesmo exemplo usando a autenticação do Windows.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
Exemplo usando os argumentos para um arquivo de origem e o arquivo de erro.  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. Carregar dados em uma tabela da AdventureWorks  
O exemplo a seguir é parte de um script em lotes que carrega dados em **AdventureWorksPDW2012**.  Para exibir o script completo, abra o arquivo aw_create é fornecido com o **AdventureWorksPDW2012** pacote de instalação. 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

O trecho de script a seguir usa dwloader para carregar dados nas tabelas DimAccount e DimCurrency. Esse script está usando um endereço de Ethernet. Se ele estava usando InfiniBand, servidor seria *< appliance_name >* `-SQLCTL01`.  
  
```  
set server=10.193.63.134  
set user=<MyUser>  
set password=<MyPassword>  
  
set schema=AdventureWorksPDW2012.dbo  
set load="C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe"  
set mode=reload  
  
--Loads data into the AdventureWorksPDW2012.dbo.DimAccount table  
--Source data is stored in the file DimAccount.txt,   
--which is in the current directory.  
  
set t1=DimAccount  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%   
  
--Loads data from the DimCurrency.txt file into  
--AdventureWorksPDW2012.dbo.DimCurrency  
set t1=DimCurrency  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%  
```  
  
A seguir está a DDL da tabela DimAccount.  
  
```  
CREATE TABLE DimAccount(  
AccountKey int NOT NULL,  
ParentAccountKey int,  
AccountCodeAlternateKey int,  
ParentAccountCodeAlternateKey int,  
AccountDescription nvarchar(50),  
AccountType nvarchar(50),  
Operator nvarchar(50),  
CustomMembers nvarchar(300),  
ValueType nvarchar(50),  
CustomMemberOptions nvarchar(200))  
with (CLUSTERED INDEX(AccountKey),  
DISTRIBUTION = REPLICATE);  
```  
  
O exemplo a seguir é um exemplo do arquivo de dados, DimAccount.txt, que contém dados a serem carregados na tabela DimAccount.  
  
```  
--Sample of data in the DimAccount.txt load file.  
  
1||1||Balance Sheet||~||Currency|  
2|1|10|1|Assets|Assets|+||Currency|  
3|2|110|10|Current Assets|Assets|+||Currency|  
4|3|1110|110|Cash|Assets|+||Currency|  
5|3|1120|110|Receivables|Assets|+||Currency|  
6|5|1130|1120|Trade Receivables|Assets|+||Currency|  
7|5|1140|1120|Other Receivables|Assets|+||Currency|  
8|3|1150|110|Allowance for Bad Debt|Assets|+||Currency|  
9|3|1160|110|Inventory|Assets|+||Currency|  
10|9|1162|1160|Raw Materials|Assets|+||Currency|  
11|9|1164|1160|Work in Process|Assets|+||Currency|  
12|9|1166|1160|Finished Goods|Assets|+||Currency|  
13|3|1170|110|Deferred Taxes|Assets|+||Currency|  
```  
  
### <a name="c-load-data-from-the-command-line"></a>C. Carregar dados da linha de comando  
O script no exemplo B pode ser substituído, inserindo todos os parâmetros na linha de comando, conforme mostrado no exemplo a seguir.  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe -S <Control node IP> -E -M reload -e UTF16 -i .\DimAccount.txt -T AdventureWorksPDW2012.dbo.DimAccount -R DimAccount.bad -t "|" -r \r\n -U <login> -P <password>  
```  
  
Descrição dos parâmetros de linha de comando:  
  
-   *C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe* é o local de instalação do dwloader.exe.  
  
-   *-S* é seguido pelo endereço IP do nó de controle.  
  
-   *-E* Especifica a carga de cadeias de caracteres vazias como NULL.  
  
-   *-M recarregar* especifica para truncar a tabela de destino antes de inserir os dados de origem.  
  
-   *-e UTF16* indica o arquivo de origem usa little endian de codificação de caracteres tipo.  
  
-   *-i.\DimAccount.txt* Especifica os dados estão em um arquivo chamado DimAccount.txt que existe no diretório atual.  
  
-   *-T AdventureWorksPDW2012.dbo.DimAccount* Especifica o nome de parte 3 da tabela para receber os dados.  
  
-   *-R DimAccount.bad* Especifica as linhas que não carregarão serão gravadas em um arquivo chamado DimAccount.bad.  
  
-   *-t "|"*  indica os campos no arquivo de entrada, DimAccount.txt, são separados pelo caractere de pipe.  
  
-   *-r \r\n* Especifica cada linha na DimAccount.txt termina com um retorno de carro e o caractere de alimentação de uma linha.  
  
-   *-U < login_name > -P <password>*  Especifica o logon e senha para o logon que tenha permissões para executar o carregamento.  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
