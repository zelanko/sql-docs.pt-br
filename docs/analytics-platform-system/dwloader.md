---
title: Carregador de linha de comando dwloader
description: dwloader é uma ferramenta de linha de comando de data warehouse paralelo (PDW) que carrega linhas de tabela em massa em uma tabela existente.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 7dd0ccf960b53b3cd1b474f61c60a58ff9b0a2c6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767045"
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>Carregador de linha de comando dwloader para data warehouse paralelos
**dwloader** é uma ferramenta de linha de comando de data warehouse paralelo (PDW) que carrega linhas de tabela em massa em uma tabela existente. Ao carregar linhas, você pode adicionar todas as linhas ao final da tabela (modo de*acréscimo* ou *modo fastappend*), acrescentar novas linhas e atualizar as linhas existentes (*modo Upsert*) ou excluir todas as linhas existentes antes do carregamento e, em seguida, inserir todas as linhas em uma tabela vazia (*modo de recarregamento*).  
  
**Processo para carregar dados**  
  
1.  Prepare os dados de origem.  
  
    Use seu próprio processo de ETL para criar os dados de origem que você deseja carregar. Os dados de origem devem ser formatados para corresponder ao esquema da tabela de destino. Armazene os dados de origem em um ou mais arquivos de texto e copie os arquivos de texto para o mesmo diretório no servidor de carregamento. Para obter informações sobre o servidor de carregamento, consulte [adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md)  
  
2.  Prepare as opções de carregamento.  
  
    Decida quais opções de carregamento serão usadas. Armazene as opções de carregamento em um arquivo de configuração. Copie o arquivo de configuração para um local local no servidor de carregamento. As opções de configuração do **dwloader** são descritas neste tópico.  
  
3.  Prepare as opções de falha de carregamento.  
  
    Decida como você deseja que o **dwloader** manipule linhas que falham ao carregar. Para executar a carga, o **dwloader** primeiro carrega os dados em uma tabela de preparo e, em seguida, transfere os dados para a tabela de destino. À medida que o carregador carrega dados na tabela de preparo, ele rastreia o número de linhas que falham ao carregar. Por exemplo, as linhas que não estiverem formatadas corretamente não serão carregadas. As linhas com falha são copiadas para um arquivo de rejeição. Por padrão, a carga é anulada após a primeira rejeição, a menos que você especifique um limite de rejeição diferente.  
  
4.  Instale o **dwloader**.  
  
    Instale o dwloader no servidor de carregamento se ele ainda não estiver instalado. 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  Execute **dwloader**.  
  
    Entre no servidor de carregamento e execute o executável **dwloader.exe** com as opções de linha de comando apropriadas.  
  
6.  Verifique os resultados.  
  
    Você pode verificar o arquivo de linhas com falha (especificado com-R) para ver se alguma linha falhou ao ser carregada. Se esse arquivo estiver vazio, todas as linhas serão carregadas com êxito. **dwloader** é transacional, portanto, se qualquer etapa falhar (diferente de linhas rejeitadas), todas as etapas serão revertidas para seu estado inicial.  
  
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
Exibe informações de ajuda simples sobre o uso do carregador. A ajuda só será exibida se nenhum outro parâmetro de linha de comando for especificado.  
  
**-U** *login_name*  
Um logon de autenticação SQL Server válido com as permissões apropriadas para executar a carga.  
  
**-P** *password*  
A senha para um *login_name*de autenticação SQL Server.  
  
**-W**  
Use a Autenticação do Windows. (Nenhum *login_name* ou *senha* é necessário.) 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
Use um arquivo de parâmetro, *parameter_file_name*, no lugar de parâmetros de linha de comando. *parameter_file_name* pode conter qualquer parâmetro de linha de comando, exceto *user_name* e *senha*. Se um parâmetro for especificado na linha de comando e no arquivo de parâmetro, a linha de comando substituirá o parâmetro file.  
  
O arquivo de parâmetro contém um parâmetro, sem o **-** prefixo, por linha.  
  
Exemplos:  
  
`rt=percentage`  
  
`rv=25`  
  
**-S** *target_appliance*  
Especifica o dispositivo SQL Server PDW que receberá os dados carregados.  
  
*Para conexões InfiniBand*, *target_appliance* é especificado como <nome-do-dispositivo>-SQLCTL01. Para configurar essa conexão nomeada, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).  
  
Para conexões Ethernet, *target_appliance* é o endereço IP para o cluster do nó de controle.  
  
Se omitido, dwloader usa como padrão o valor que foi especificado quando dwloader foi instalado. 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.* [*esquema*]. *table_name*  
O nome de três partes da tabela de destino.  
  
**-I** *source_data_location*  
O local de um ou mais arquivos de origem a serem carregados. Cada arquivo de origem deve ser um arquivo de texto ou um arquivo de texto que é compactado com gzip. Somente um arquivo de origem pode ser compactado em cada arquivo gzip.  
  
Para formatar um arquivo de origem:  
  
-   O arquivo de origem deve ser formatado de acordo com as opções de carregamento.  
  
-   Cada linha em um arquivo de origem contém os dados para uma linha de tabela. Os dados de origem devem corresponder ao esquema da tabela de destino. A ordem das colunas e os tipos de dados também devem corresponder. Cada campo na linha representa uma coluna na tabela de destino.  
  
-   Por padrão, os campos são de comprimento variável e separados por um delimitador. Para especificar o tipo de delimitador, use o <variable_length_column_options> opções de linha de comando. Para especificar campos de comprimento fixo, use o <fixed_width_column_options> opções de linha de comando.  
  
Para especificar o local dos dados de origem:  
  
-   O local dos dados de origem pode ser um caminho de rede ou um caminho local para um diretório no servidor de carregamento.  
  
-   Para especificar todos os arquivos em um diretório, insira o caminho do diretório seguido pelo caractere curinga *.  O carregador não carrega arquivos de nenhum subdiretório que esteja no local de dados de origem. O carregador ocorre quando um diretório existe em um arquivo gzip.  
  
-   Para especificar alguns dos arquivos em um diretório, use uma combinação de caracteres e o curinga *.  
  
Para carregar vários arquivos com um comando:  
  
-   Todos os arquivos devem existir no mesmo diretório.  
  
-   Os arquivos devem ser todos os arquivos de texto, todos os arquivos gzip ou uma combinação de arquivos de texto e gzip.  
  
-   Nenhum dos arquivos pode conter informações de cabeçalho.  
  
-   Todos os arquivos devem usar o mesmo tipo de codificação de caractere. Consulte a opção-e.  
  
-   Todos os arquivos devem ser carregados na mesma tabela.  
  
-   Todos os arquivos serão concatenados e carregados como se fossem um arquivo, e as linhas rejeitadas vão para um único arquivo de rejeição.  
  
Exemplos:  
  
-   -i \\ \loadserver\loads\daily \\ *. gz  
  
-   -i \\ \loadserver\loads\daily \\ *. txt  
  
-   -i \\ \loadserver\loads\daily\monday. *  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\ \loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
Se houver falhas de carregamento, o **dwloader** armazena a linha que falhou ao carregar e a descrição de falha as informações de falha em um arquivo chamado *load_failure_file_name*. Se esse arquivo já existir, o dwloader substituirá o arquivo existente. *load_failure_file_name* é criado quando a primeira falha ocorre. Se todas as linhas forem carregadas com êxito, *load_failure_file_name* não será criado.  
  
**-fh** *number_header_rows*  
O número de linhas (linhas) a serem ignoradas no início de *source_data_file_name*. O padrão é 0.  
  
<variable_length_column_options>  
As opções para um *source_data_file_name* que tem colunas de comprimento variável delimitadas por caractere. Por padrão, *source_data_file_name* contém caracteres ASCII em colunas de comprimento variável.  
  
Para arquivos ASCII, os nulos são representados colocando-se delimitadores consecutivamente. Por exemplo, em um arquivo delimitado por pipe ("|"), um NULL é indicado por "| |". Em um arquivo delimitado por vírgula, um NULL é indicado por ",,". Além disso, a opção **-E** (--emptyStringAsNull) deve ser especificada. Para obter mais informações sobre-E, consulte abaixo.  
  
**-e** *character_encoding*  
Especifica um tipo de codificação de caracteres para os dados a serem carregados do arquivo de dados. As opções são ASCII (padrão), UTF8, UTF16 ou UTF16BE, em que UTF16 é little endian e UTF16BE é big endian. Essas opções não diferenciam maiúsculas de minúsculas.  
  
**-t** *field_delimiter*  
O delimitador para cada campo (coluna) na linha. O delimitador de campo é um ou mais desses caracteres ASCII de escape ou valores hexadecimais ASCII.  
  
|Nome|Caractere de escape|Caractere hex|  
|--------|--------------------|-----------------|  
|Tab|\t|0x09|  
|Retorno de carro (CR)|\r|0x0D|  
|Alimentação de linha (LF)|\n|0x0A|  
|CRLF|\r\n|0x0d0x0a|  
|Vírgula|','|0x2c|  
|Aspas duplas|\\"|0x22|  
|Aspas simples|\\'|0x27|  
  
Para especificar o caractere de pipe na linha de comando, coloque-o entre aspas duplas, "|". Isso evitará a interpretação inalterada pelo analisador de linha de comando. Outros caracteres são colocados entre aspas simples.  
  
Exemplos:  
  
-t "|"  
  
-t ' '  
  
-t 0x0A  
  
-t \t  
  
-t ' ~ | ~ '  
  
**-r** *row_delimiter*  
O delimitador para cada linha do arquivo de dados de origem. O delimitador de linha é um ou mais valores ASCII.  
  
Para especificar um retorno de carro (CR), alimentação de linha (LF) ou caractere de tabulação como um delimitador, você pode usar os caracteres de escape (\r, \n, \t) ou seus valores hexadecimais (0x, 0d, 09). Para especificar quaisquer outros caracteres especiais como delimitadores, use seu valor hex.  
  
Exemplos de CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Exemplos de CR:  
  
-r \r  
  
-r 0x0D  
  
Exemplos de LF:  
  
-r \n  
  
-r 0x0A  
  
Um LF é necessário para UNIX. Uma CR é necessária para o Windows.  
  
**-s** *string_delimiter*  
O delimitador do campo de tipo de dados de cadeia de caracteres de um arquivo de entrada delimitado por texto. O delimitador de cadeia de caracteres é um ou mais valores ASCII.  Ele pode ser especificado como um caractere (por exemplo,-s *) ou como um valor hex (por exemplo,-s 0x22 para aspas duplas).  
  
Exemplos:  
  
&  
  
-s 0x22  
  
< fixed_width_column_options>  
As opções para um arquivo de dados de origem que tem colunas de comprimento fixo. Por padrão, *source_data_file_name* contém caracteres ASCII em colunas de comprimento variável.  
  
Não há suporte para colunas de largura fixa quando-e é UTF8.  
  
**-w** *fixed_width_config_file*  
Caminho e nome do arquivo de configuração que especifica o número de caracteres em cada coluna. Cada campo deve ser especificado.  
  
Esse arquivo deve residir no servidor de carregamento. O caminho pode ser um caminho UNC, relativo ou absoluto. Cada linha em *fixed_width_config_file* contém o nome de uma coluna e o número de caracteres para essa coluna. Há uma linha por coluna, da seguinte maneira, e a ordem no arquivo deve corresponder à ordem na tabela de destino:  
  
*column_name* = *num_chars*  
  
*column_name* = *num_chars*  
  
Arquivo de configuração de largura fixa de exemplo:  
  
SalesCode = 3  
  
Saleid = 10  
  
Linhas de exemplo no *source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
No exemplo anterior, a primeira linha carregada terá SalesCode = ' 230 ' e Saleid = ' Shirts0056 '. A segunda linha carregada terá SalesCode = ' 320 ' e Saleid = ' Towels1356 '.  
  
Para obter informações sobre como lidar com espaços à esquerda e à direita ou conversão de tipo de dados no modo de largura fixa, consulte [regras de conversão de tipo de dados para dwloader](dwloader-data-type-conversion-rules.md).  
  
**-e** *character_encoding*  
Especifica um tipo de codificação de caracteres para os dados a serem carregados do arquivo de dados. As opções são ASCII (padrão), UTF8, UTF16 ou UTF16BE, em que UTF16 é little endian e UTF16BE é big endian. Essas opções não diferenciam maiúsculas de minúsculas.  
  
Não há suporte para colunas de largura fixa quando-e é UTF8.  
  
**-r** *row_delimiter*  
O delimitador para cada linha do arquivo de dados de origem. O delimitador de linha é um ou mais valores ASCII.  
  
Para especificar um retorno de carro (CR), alimentação de linha (LF) ou caractere de tabulação como um delimitador, você pode usar os caracteres de escape (\r, \n, \t) ou seus valores hexadecimais (0x, 0d, 09). Para especificar quaisquer outros caracteres especiais como delimitadores, use seu valor hex.  
  
Exemplos de CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Exemplos de CR:  
  
-r \r  
  
-r 0x0D  
  
Exemplos de LF:  
  
-r \n  
  
-r 0x0A  
  
Um LF é necessário para UNIX. Uma CR é necessária para o Windows.  
  
**-D** { **ymd** \| ydm \| MDY \| MYD \| dmy \| DYM \| *custom_date_format* }  
Especifica a ordem de mês (m), dia (d) e ano (y) para todos os campos de data e hora no arquivo de entrada. A ordem padrão é ymd. Para especificar vários formatos de ordem para o mesmo arquivo de origem, use a opção-DT.  
  
ymd \| dmy  
YDM e dmy permitem os mesmos formatos de entrada. Ambos permitem que o ano esteja no início ou no final da data. Por exemplo, para os formatos de data **ydm** e **dmy** , você poderia ter 2013-02-03 ou 02-03-2013 no arquivo de entrada.  
  
YDM  
Você só pode carregar a entrada formatada como ydm em colunas do tipo de dados DateTime e smalldatetime. Não é possível carregar valores ydm em uma coluna do tipo de dados datetime2, Date ou DateTimeOffset.  
  
mda  
MDY permite \<month> \<space> \<day> \<comma> \<year> .  
  
Exemplos de dados de entrada MDY para 1º de janeiro de 1975:  
  
-   1º de janeiro de 1975  
  
-   01 de janeiro de 75  
  
-   Jan/1/75  
  
-   01011975  
  
mad  
Exemplos de arquivo de entrada para 04 de março de 2010:03-2010-04, 3/2010/4  
  
dam  
Exemplos de arquivo de entrada para 04 de março de 2010:04-2010-03, 4/2010/3  
  
*custom_date_format*  
*custom_date_format* é um formato de data personalizado (por exemplo, mm/dd/aaaa) e incluído somente para compatibilidade com versões anteriores. dwloader não impõe o formato de data personalizado. Em vez disso, quando você especificar um formato de data personalizado, o **dwloader** o converterá para a configuração correspondente de ymd, ydm, MDY, MYD, DYM ou dmy.  
  
Por exemplo, se você especificar-D MM/dd/yyyy, dwloader espera que todas as entradas de data sejam ordenadas com month First, Day e Year (MDY). Ele não impõe dois meses de caractere, dias de 2 dígitos e anos de 4 dígitos, conforme especificado pelo formato de data personalizado. Aqui estão alguns exemplos de como as datas podem ser formatadas no arquivo de entrada quando o formato de data é-D MM/dd/aaaa: 01/02/2013, Jan. 02.2013, 1/2/2013  
  
Para obter informações de formatação mais abrangentes, consulte [regras de conversão de tipo de dados para dwloader](dwloader-data-type-conversion-rules.md).  
  
**-dt** *datetime_format_file*  
Cada formato DateTime é especificado em um arquivo chamado *datetime_format_file*. Ao contrário dos parâmetros de linha de comando, os parâmetros de arquivo que incluem espaços não devem ser colocados entre aspas duplas. Você não pode alterar o formato DateTime ao carregar dados. O arquivo de dados de origem e sua coluna correspondente na tabela de destino devem ter o mesmo formato.  
  
Cada linha contém o nome de uma coluna na tabela de destino e seu formato de data e hora.  
  
Exemplos:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
O nome do banco de dados que conterá a tabela de preparo. O padrão é o banco de dados especificado com a opção-T, que é o banco de dados para a tabela de destino. Para obter mais informações sobre como usar um banco de dados de preparo, consulte [criar o banco de dados de preparo](staging-database.md).  
  
**-M** *load_mode_option*  
Especifica se os dados devem ser acrescentados, Upsert ou recarregados. O modo padrão é Append.  
  
acrescentar  
O carregador insere linhas no final das linhas existentes na tabela de destino.  
  
fastappend  
O carregador insere linhas diretamente, sem usar uma tabela temporária, até o final das linhas existentes na tabela de destino. fastappend requer a opção de várias transações (-m). Um banco de dados de preparo não pode ser especificado ao usar fastappend. Não há nenhuma reversão com fastappend, o que significa que a recuperação de uma carga com falha ou anulada deve ser tratada pelo seu próprio processo de carregamento.  
  
*merge_column* Upsert **-K**[,... *n* ]    
O carregador usa a instrução SQL Server Merge para atualizar as linhas existentes e inserir novas linhas.  
  
A opção-K especifica a coluna ou colunas na qual basear a mesclagem. Essas colunas formam uma chave de mesclagem, que deve representar uma linha exclusiva. Se a chave de mesclagem existir na tabela de destino, a linha será atualizada. Se a chave de mesclagem não existir na tabela de destino, a linha será anexada.  
  
Para tabelas distribuídas por hash, a chave de mesclagem deve ser ou incluir a coluna de distribuição.  
  
Para tabelas replicadas, a chave de mesclagem é a combinação de uma ou mais colunas. Essas colunas são especificadas de acordo com as necessidades do aplicativo.  
  
Várias colunas devem ser separadas por vírgulas sem espaços ou separados por vírgula com espaços e entre aspas simples.  
  
Se duas linhas na tabela de origem tiverem valores de chave de mesclagem correspondentes, suas respectivas linhas deverão ser idênticas.  
  
recarregar  
O carregador trunca a tabela de destino antes de inserir os dados de origem.  
  
**-b** *BatchSize*  
Recomendado somente para uso por Suporte da Microsoft, *BatchSize* é o tamanho do lote de SQL Server para a cópia em massa que o DMS realiza em SQL Server instâncias nos nós de computação.  Quando *BatchSize* é especificado, SQL Server PDW substituirá o tamanho de carga do lote que é calculado dinamicamente para cada carga.  
  
A partir do SQL Server PDW 2012, o nó de controle computa dinamicamente um tamanho de lote para cada carga por padrão. Esse cálculo automático se baseia em vários parâmetros, como o tamanho da memória, o tipo de tabela de destino, o esquema da tabela de destino, o tipo de carga, o tamanho do arquivo e a classe de recurso do usuário.  
  
Por exemplo, se o modo de carga for FASTAPPEND e a tabela tiver um índice columnstore clusterizado, SQL Server PDW, por padrão, tentará usar um tamanho de lote de 1.048.576 para que os RowGroups sejam fechados e sejam carregados diretamente no columnstore sem passar pelo armazenamento Delta. Se a memória não permitir o tamanho do lote de 1.048.576, dwloader escolherá um BatchSize menor.  
  
Se o tipo de carga for FASTAPPEND, o *BatchSize* se aplicará ao carregamento de dados na tabela; caso contrário, o *BatchSize* se aplicará ao carregamento de dados na tabela de preparo.  
  
<reject_options>  
Especifica opções para determinar o número de falhas de carregamento que o carregador permitirá. Se as falhas de carga excederem o limite, o carregador será interrompido e não confirmará nenhuma linha.  
  
**-RT** { **valor** | percentual}  
Especifica se o-*reject_value* na opção **-RV** *reject_value* é um número literal de linhas (valor) ou uma taxa de falha (percentual). O padrão é value.  
  
A opção percentual é um cálculo em tempo real que ocorre em intervalos de acordo com a opção-RS.  
  
Por exemplo, se o carregador tentar carregar 100 linhas e 25 falhas e 75 for bem-sucedida, a taxa de falha será de 25%.  
  
**-rv** *reject_value*  
Especifica o número ou o percentual de rejeições de linha a permitir antes de parar a carga. A opção **-RT** determina se *reject_value* se refere ao número de linhas ou à porcentagem de linhas.  
  
O *reject_value* padrão é 0.  
  
Quando usado com o valor-RT, o carregador interrompe a carga quando a contagem de linhas rejeitadas excede reject_value.  
  
Ao usar a porcentagem com-RT, o carregador computa a porcentagem em intervalos (opção-RS). Portanto, a porcentagem de linhas com falha pode exceder *reject_value*.  
  
**-rs** *reject_sample_size*  
Usado com a `-rt percentage` opção para especificar as verificações de percentual incremental. Por exemplo, se reject_sample_size for 1000, o carregador calculará a porcentagem de linhas com falha depois de tentar carregar 1000 linhas. Ele recalcula a porcentagem de linhas com falha depois de tentar carregar cada 1000 linhas adicionais.  
  
**-c**  
Remove os caracteres de espaço em branco do lado esquerdo e direito dos campos Char, nchar, varchar e nvarchar. Converte cada campo que contém somente caracteres de espaço em branco na cadeia de caracteres vazia.  
  
Exemplos:  
  
' ' é truncado para ' '  
  
' abc ' é truncado para ' abc '  
  
Quando-c é usado com-E, a operação-E ocorre primeiro. Os campos que contêm apenas caracteres de espaço em branco são convertidos na cadeia de caracteres vazia e não em nulo.  
  
**-E**  
Converta cadeias de caracteres vazias em NULL. O padrão é não executar essas conversões.  
  
**-m**  
Usar o modo de várias transações para a segunda fase de carregamento; ao carregar dados da tabela de preparo em uma tabela distribuída.  
  
Com **-m**, SQL Server PDW executa e confirma as cargas em paralelo. Isso é executado muito mais rapidamente do que o modo de carregamento padrão, mas não é seguro para transações.  
  
Sem **-m**, SQL Server PDW executa e confirma as cargas em série em todas as distribuições dentro de cada nó de computação e simultaneamente nos nós de computação. Esse método é mais lento do que o modo de várias transações, mas é seguro para transações.  
  
**-m** é opcional para *anexar*, *recarregar*e *Upsert*.  
  
**-m** é necessário para fastappend.  
  
**-m** não pode ser usado com tabelas replicadas.  
  
**-m** aplica-se somente à segunda fase de carregamento. Ele não se aplica à primeira fase de carregamento; carregando dados na tabela de preparo.  
  
Não há reversão com o modo de várias transações, o que significa que a recuperação de uma carga com falha ou anulada deve ser tratada pelo seu próprio processo de carregamento.  
  
É recomendável usar **-m** somente ao carregar em uma tabela vazia, para que você possa recuperar sem perda de dados. Para se recuperar de uma falha de carregamento: Remova a tabela de destino, resolva o problema de carregamento, recrie a tabela de destino e execute a carga novamente.  
  
**-N**  
Verifique se o dispositivo de destino tem um certificado de SQL Server PDW válido de uma autoridade confiável. Use isso para ajudar a garantir que seus dados não sejam seqüestrados por um invasor e enviados a um local não autorizado. O certificado já deve estar instalado no dispositivo. A única maneira com suporte para instalar o certificado é o administrador do dispositivo instalá-lo usando a ferramenta de Configuration Manager. Pergunte ao administrador do dispositivo se você não tem certeza se o dispositivo tem um certificado confiável instalado.  
  
**-se**  
Ignorar carregamento de arquivos vazios. Isso também ignora a descompactação de arquivos gzip vazios.

**-l**  
Disponível com a atualização do CU 7.4, especifica o tamanho máximo da linha (em bytes) que pode ser carregado. Os valores válidos são inteiros entre 32768 e 33554432. Use apenas quando necessário para carregar linhas grandes (maiores que 32 KB), pois isso alocará mais memória no cliente e no servidor.
  
## <a name="return-code-values"></a>Valores do código de retorno  
0 (êxito) ou outro valor inteiro (falha)  
  
Em uma janela de comando ou arquivo em lotes, use `errorlevel` para exibir o código de retorno. Por exemplo:  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
Ao usar o PowerShell, use `$LastExitCode` .  
  
## <a name="permissions"></a>Permissões  
Requer permissão de carregamento e permissões aplicáveis (inserir, atualizar, excluir) na tabela de destino. Requer a permissão CREATE (para criar uma tabela temporária) no banco de dados de preparo. Se um banco de dados de preparo não for usado, a permissão CREATE será necessária no banco de dados de destino. 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>Comentários gerais  
Para obter informações sobre conversões de tipo de dados ao carregar com dwloader, consulte [regras de conversão de tipo de dados para dwloader](dwloader-data-type-conversion-rules.md).  
  
Se um parâmetro incluir um ou mais espaços, coloque o parâmetro com aspas duplas.  
  
Você deve executar o carregador de seu local de instalação. O executável dwloader é pré-instalado com o dispositivo e está localizado no diretório C:\Program Files\Microsoft SQL Server Data Warehouse\DWLoader.  
  
Você pode substituir um parâmetro especificado no arquivo de parâmetro (opção-f) especificando-o como um parâmetro de linha de comando.  
  
Você pode executar várias instâncias do carregador simultaneamente. O número máximo de instâncias de carregador é pré-configurado e não pode ser alterado. 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
Os dados carregados podem exigir mais ou menos espaço no dispositivo do que no local de origem. Você pode executar importações de teste com subconjuntos de dados para estimar o consumo de disco.  
  
Embora **dwloader** seja um processo de transação e seja revertido normalmente em caso de falha, ele não poderá ser revertido depois que o carregamento em massa for concluído com êxito. Para cancelar um processo **dwloader** ativo, digite CTRL + C.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
O tamanho total de todas as cargas que ocorrem simultaneamente deve ser menor que LOG_SIZE para o banco de dados e é recomendável que o tamanho total de todas as cargas simultâneas seja menor que 50% do LOG_SIZE. Para obter essa limitação de tamanho, você pode dividir grandes cargas em vários lotes. Para obter mais informações sobre LOG_SIZE, consulte [criar banco de dados](../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016)  
  
Ao carregar vários arquivos com um comando de carregamento, todas as linhas rejeitadas são gravadas no mesmo arquivo de rejeição. O arquivo de rejeição não mostra qual arquivo de entrada contém cada linha rejeitada.  
  
A cadeia de caracteres vazia não deve ser usada como um delimitador. Quando uma cadeia de caracteres vazia for usada como um delimitador de linha, a carga falhará. Quando usado como delimitador de coluna, a carga ignora o delimitador e continua a usar o padrão "|" como o delimitador de coluna. Quando usado como delimitador de cadeia de caracteres, a cadeia de caracteres vazia é ignorada e o comportamento padrão é aplicado.  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
o comportamento de bloqueio de **dwloader** varia dependendo do *load_mode_option*.  
  
-   **Append** – Append é a opção recomendada e mais comum. Append carrega dados em uma tabela de preparo. O bloqueio é descrito em detalhes abaixo.  
  
-   o **acréscimo rápido** -Fast-Append carrega diretamente na tabela final usando um bloqueio de tabela ExclusiveUpdate e é o único modo que não usa uma tabela de preparo.  
  
-   **recarregar-reload carrega** dados em uma tabela de preparo e requer um bloqueio exclusivo na tabela de preparo e na tabela final. O recarregamento não é recomendado para operações simultâneas.  
  
-   o **Upsert** -Upsert carrega dados em uma tabela de preparo e, em seguida, executa uma operação de mesclagem da tabela de preparo para a tabela final. Upsert não requer bloqueios exclusivos na tabela final. O desempenho pode variar ao usar o Upsert. Teste o comportamento em seu ambiente.  
  
### <a name="locking-behavior"></a>Comportamento de bloqueio  
**Bloqueio de modo de acréscimo**  
  
O acréscimo pode ser executado no modo de várias transacionais (usando o argumento-m), mas não é seguro para transações. Portanto, Append deve ser usado como uma operação transacional (sem usar o argumento-m). Infelizmente, durante a operação de inserção-seleção final, no momento, o modo transacional é cerca de seis vezes mais lenta do que o modo de várias transacionais.  
  
O modo de acréscimo carrega dados em duas fases. A fase 1 carrega os dados do arquivo de origem em uma tabela de preparo simultaneamente (a fragmentação pode ocorrer). A fase dois carrega dados da tabela de preparo para a tabela final. A segunda fase executa uma **inserção em... Selecione WITH (TABLOCK)** operação. A tabela a seguir mostra o comportamento de bloqueio na tabela final e o comportamento de log ao usar o modo de acréscimo:  
  
|Tipo de tabela|Transações múltiplas<br />Modo (-m)|A tabela está vazia|Simultaneidade com suporte|Registrando em log|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|Pilha|Sim|Sim|Sim|Minimal|  
|Pilha|Sim|Não|Sim|Minimal|  
|Pilha|Não|Sim|Não|Minimal|  
|Pilha|Não|Não|Não|Minimal|  
|L|Sim|Sim|Não|Minimal|  
|L|Sim|Não|Sim|Completo|  
|L|Não|Sim|Não|Minimal|  
|L|Não|Não|Sim|Completo|  
  
A tabela acima mostra **dwloader** usando o modo de acréscimo carregando em um heap ou uma tabela de índice clusterizado (CI), com ou sem o sinalizador de várias transacionais e o carregamento em uma tabela vazia ou em uma tabela não vazia. O comportamento de bloqueio e de log de cada combinação de carga é exibido na tabela. Por exemplo, a fase de carregamento (2ª) com o modo Append em um índice clusterizado sem o modo multifuncional e em uma tabela vazia terá o PDW para criar um bloqueio exclusivo na tabela e o registro em log é mínimo. Isso significa que um cliente não será capaz de carregar (2ª) a fase e a consulta simultaneamente em uma tabela vazia. No entanto, ao carregar com a mesma configuração em uma tabela não vazia, o PDW não emitirá um bloqueio exclusivo na tabela e a simultaneidade será possível. Infelizmente, o log completo ocorre, reduzindo o processo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-dwloader-example"></a>a. Exemplo de dwloader simples  
O exemplo a seguir mostra a inicialização do **carregador** apenas com as opções necessárias selecionadas. Outras opções são obtidas do arquivo de configuração global, *loadparamfile.txt*.  
  
Exemplo usando a autenticação SQL Server.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
O mesmo exemplo usa a autenticação do Windows.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
Exemplo de uso de argumentos para um arquivo de origem e arquivo de erro.  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. Carregar dados em uma tabela do AdventureWorks  
O exemplo a seguir faz parte de um script em lotes que carrega dados no **AdventureWorksPDW2012**.  Para exibir o script completo, abra o arquivo aw_create.bat fornecido com o pacote de instalação do **AdventureWorksPDW2012** . 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

O trecho de script a seguir usa dwloader para carregar dados nas tabelas DimAccount e DimCurrency. Este script está usando um endereço Ethernet. Se ele estava usando InfiniBand, o servidor seria *<appliance_name>* `-SQLCTL01` .  
  
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
  
Este é o DDL para a tabela DimAccount.  
  
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
  
Veja a seguir um exemplo do arquivo de dados, DimAccount.txt, que contém dados a serem carregados na tabela DimAccount.  
  
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
O script no exemplo B pode ser substituído inserindo-se todos os parâmetros na linha de comando, conforme mostrado no exemplo a seguir.  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe -S <Control node IP> -E -M reload -e UTF16 -i .\DimAccount.txt -T AdventureWorksPDW2012.dbo.DimAccount -R DimAccount.bad -t "|" -r \r\n -U <login> -P <password>  
```  
  
Descrição dos parâmetros de linha de comando:  
  
-   *C:\Arquivos de programas\microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe* é o local do dwloader.exe instalado.  
  
-   *-S* é seguido pelo endereço IP do nó de controle.  
  
-   *-E* especifica a carga de cadeias de caracteres vazias como nulas.  
  
-   *-M reload* especifica para truncar a tabela de destino antes de inserir os dados de origem.  
  
-   *-e UTF16* indica que o arquivo de origem usa o tipo de codificação de caractere little endian.  
  
-   *-i .\DimAccount.txt* especifica que os dados estão em um arquivo chamado DimAccount.txt que existe no diretório atual.  
  
-   *-T AdventureWorksPDW2012. dbo. DimAccount* especifica o nome de 3 partes da tabela para receber os dados.  
  
-   *-R DimAccount. Bad* especifica que as linhas que não puderam ser carregadas serão gravadas em um arquivo chamado DimAccount. Bad.  
  
-   *-t "|"* indica que os campos no arquivo de entrada, DimAccount.txt, são separados com o caractere de barra vertical.  
  
-   *-r \r\n* especifica que cada linha em DimAccount.txt termina com um retorno de carro e um caractere de alimentação de linha.  
  
-   *-U <login_name>-P <password> * Especifica o logon e a senha para o logon que tem permissões para executar a carga.  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
