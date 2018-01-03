---
title: Carregador de linha de comando para Parallel Data Warehouse de dwloader
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "**dwloader** é uma ferramenta de linha de comando do Parallel Data Warehouse (PDW) que carrega linhas da tabela em massa em uma tabela existente."
ms.date: 11/04/2016
ms.topic: article
ms.assetid: f79b8354-fca5-41f7-81da-031fc2570a7c
caps.latest.revision: "90"
ms.openlocfilehash: 4050df3fa69a823ebb36076367c2e8d7344ac1a2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="dwloader-command-line-loader"></a>Carregador de linha de comando de dwloader
**dwloader** é uma ferramenta de linha de comando do Parallel Data Warehouse (PDW) que carrega linhas da tabela em massa em uma tabela existente. Quando o carregamento de linhas, você pode adicionar todas as linhas ao final da tabela (*modo de acréscimo* ou *modo fastappend*), acrescentar novas linhas e atualizar as linhas existentes (*modo upsert*), ou excluir todos os linhas antes do carregamento de existente e, em seguida, inserir todas as linhas em uma tabela vazia (*recarregar modo*).  
  
**Processo de carregamento de dados**  
  
1.  Prepare os dados de origem.  
  
    Use seu próprio processo ETL para criar a fonte de dados que você deseja carregar. Os dados de origem devem ser formatados para corresponder ao esquema da tabela de destino. Armazenar os dados de origem em um ou mais arquivos de texto e copie os arquivos de texto no mesmo diretório em seu servidor de carregamento. Para obter informações sobre o servidor de carregamento, consulte [adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md)  
  
2.  Prepare as opções de carregamento.  
  
    Decida quais opções de carregamento será usado. Armazene as opções de carregamento em um arquivo de configuração. Copie o arquivo de configuração para um local no servidor de carregamento. O **dwloader** opções de configuração são descritas neste tópico.  
  
3.  Prepare a carga de opções de falha.  
  
    Decida como deseja **dwloader** para lidar com linhas com Falha ao carregar. Para executar o carregamento, **dwloader** primeiro carrega os dados em uma tabela de preparo e, em seguida, transfere os dados para a tabela de destino. Como o carregador carrega dados na tabela de preparo, ele rastreia o número de linhas que falha ao carregar. Por exemplo, linhas que não estão formatadas corretamente falhará ao carregar. Linhas com falha são copiadas para um arquivo de rejeição. Por padrão, a carga será anulada após a primeira rejeição, a menos que você especificar um limite de rejeição diferentes.  
  
4.  Instalar **dwloader**.  
  
    Se já não estiver instalado, instale dwloader no servidor de carregamento. 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  Executar **dwloader**.  
  
    Faça logon servidor de carregamento e o executável **dwloader.exe** com as opções de linha de comando apropriadas.  
  
6.  Verifique se os resultados.  
  
    Você pode verificar a linhas de arquivo (especificado com -R) para ver se todas as linhas não pôde ser carregado. Se esse arquivo estiver vazio, todas as linhas carregado com êxito. **dwloader** é transacional, portanto, se qualquer etapa falhar (diferente de linhas rejeitadas), todas as etapas reverterá ao estado inicial.  
  
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
}  
```  
  
## <a name="arguments"></a>Argumentos  
**-h**  
Exibe informações de Ajuda simples sobre como usar o carregador. Ajuda exibe somente se nenhum outro parâmetro de linha de comando é especificado.  
  
**-U** *login_name*  
Um logon de autenticação do SQL Server válido com permissões apropriadas para executar a carga.  
  
**-P** *password*  
A senha para autenticação do SQL Server *login_name*.  
  
**-W**  
Use a Autenticação do Windows. (Nenhum *login_name* ou *senha* necessária.) 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
Usar um arquivo de parâmetro, *parameter_file_name*, em vez de parâmetros de linha de comando. *parameter_file_name* pode conter qualquer parâmetro de linha de comando, exceto *user_name* e *senha*. Se um parâmetro for especificado na linha de comando e no arquivo de parâmetro, a linha de comando substitui o parâmetro de arquivo.  
  
O arquivo de parâmetros contém um parâmetro, sem o  **-**  prefixo por linha.  
  
Exemplos:  
  
`rt=percentage`  
  
`rv=25`  
  
**-S***target_appliance*  
Especifica o dispositivo de PDW do SQL Server que receberá os dados carregados.  
  
*Para conexões do Infiniband*, *target_appliance* é especificado como < nome do dispositivo >-SQLCTL01. Para configurar essa conexão, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).  
  
Para conexões Ethernet, *target_appliance* é o endereço IP para o cluster de nó de controle.  
  
Se omitido, dwloader padrão é o valor que foi especificado quando dwloader foi instalado. 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.* [*esquema*]. *table_name*  
O nome de três partes da tabela de destino.  
  
**-I***source_data_location*  
O local de um ou mais arquivos de origem para carregar. Cada arquivo de origem deve ser um arquivo de texto ou um arquivo de texto que é compactado com gzip. Somente um arquivo de origem pode ser compactado em cada arquivo gzip.  
  
Para formatar um arquivo de origem:  
  
-   O arquivo de origem deve ser formatado de acordo com as opções de carregamento.  
  
-   Cada linha em um arquivo de origem contém os dados de linha de uma tabela. Os dados de origem devem corresponder ao esquema da tabela de destino. Tipos de dados e a ordem de coluna também devem corresponder. Cada campo na linha representa uma coluna na tabela de destino.  
  
-   Por padrão, os campos são de comprimento variável e separados por um delimitador. Para especificar o tipo de delimitador, use as opções de linha de comando < variable_length_column_options >. Para especificar os campos de comprimento fixo, use as opções de linha de comando < fixed_width_column_options >.  
  
Para especificar o local de dados de origem:  
  
-   O local de dados de origem pode ser um caminho de rede ou um caminho local para um diretório no servidor de carregamento.  
  
-   Para especificar todos os arquivos em um diretório, digite o caminho do diretório seguido de * caractere curinga.  O carregador não carregar arquivos de todas as subpastas que estão no local de dados de origem. Os erros de carregador quando existe um diretório em um arquivo gzip.  
  
-   Para especificar alguns dos arquivos em um diretório, use uma combinação de caracteres e o * curinga.  
  
Para carregar vários arquivos com um único comando:  
  
-   Todos os arquivos devem existir no mesmo diretório.  
  
-   Os arquivos devem ser todos os arquivos de texto, todos os arquivos gzip ou uma combinação de arquivos de texto e gzip.  
  
-   Nenhum dos arquivos podem conter informações de cabeçalho.  
  
-   Todos os arquivos devem usar o mesmo tipo de codificação de caractere. Consulte a opção – e.  
  
-   Todos os arquivos devem ser carregados na mesma tabela.  
  
-   Todos os arquivos serão ser concatenados e carregados da maneira como eles são um arquivo e as linhas rejeitadas irá para um arquivo único rejeitar.  
  
Exemplos:  
  
-   -i \\\loadserver\loads\daily\\*.gz  
  
-   -i \\\loadserver\loads\daily\\*. txt  
  
-   -i \\\loadserver\loads\daily\monday.*  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
Se houver falhas de carregamento, **dwloader** armazena a linha que falhou para o carregamento e a descrição da falha, as informações de falha em um arquivo chamado *load_failure_file_name*. Se esse arquivo já existir, dwloader substituirá o arquivo existente. *load_failure_file_name* é criado quando ocorre a primeira falha. Se todas as linhas com êxito, carregam *load_failure_file_name* não é criado.  
  
**-fh** *number_header_rows*  
O número de linhas (linhas) para ignorar no início do *source_data_file_name*. O padrão é 0.  
  
< variable_length_column_options >  
As opções para um *source_data_file_name* que tem colunas delimitada por caracteres de comprimento variável. Por padrão, *source_data_file_name* contém caracteres ASCII em colunas de comprimento variável.  
  
Para arquivos ASCII, valores nulos são representados colocando delimitadores consecutivamente. Por exemplo, em um arquivo delimitado por pipe ("|"), um valor nulo é indicado por "| |". Em um arquivo delimitado por vírgula, um valor nulo é indicado por ",". Além disso, o **-E** (-emptyStringAsNull) a opção deve ser especificada. Para obter mais informações sobre -E, consulte abaixo.  
  
**-e** *character_encoding*  
Especifica um tipo de codificação de caracteres para os dados a serem carregadas do arquivo de dados. Opções são ASCII (padrão), UTF8, UTF16 ou UTF16BE, onde UTF16 é pouco endian e UTF16BE é big endian. Essas opções diferenciam maiusculas de minúsculas.  
  
**-t** *field_delimiter*  
O delimitador para cada campo (coluna) na linha. O delimitador de campo é um ou mais desses caracteres ASCII ou os valores hexadecimais ASCII.  
  
|Nome|Caractere de escape|Caractere hexadecimal|  
|--------|--------------------|-----------------|  
|Tab|\t|0x09|  
|Retorno de carro (CR)|\r|0x0D|  
|Alimentação de linha (LF)|\n|0x0A|  
|CRLF|\r\n|0x0d0x0a|  
|Vírgula|','|0x2c|  
|Aspas duplas|\\"|0x22|  
|Aspas simples|\\'|0x27|  
  
Para especificar o caractere de pipe na linha de comando, coloque-o entre aspas duplas, "|". Isso evitará uma interpretação incorreta pelo analisador de linha de comando. Outros caracteres são colocados entre aspas simples.  
  
Exemplos:  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t ' ~ | ~'  
  
**-r** *row_delimiter*  
O delimitador para cada linha do arquivo de dados de origem. O delimitador de linha é um ou mais valores ASCII.  
  
Para especificar um retorno de carro (CR), alimentação de linha (LF) ou caractere de tabulação como um delimitador, você pode usar os caracteres de escape (\r, \n, \t) ou seus valores hexadecimais (0 x, 0d 09). Para especificar outros caracteres especiais como delimitadores, use o valor hexadecimal.  
  
Exemplos de CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Exemplos de CR:  
  
-r \r  
  
-r 0x0d  
  
Exemplos de LF:  
  
\n - r  
  
-r 0x0a  
  
Um LF é necessária para Unix. Uma CR é necessária para o Windows.  
  
**-s** *string_delimiter*  
O delimitador para dados de cadeia de caracteres de tipo de campo de um arquivo delimitado por texto de entrada. O delimitador de cadeia de caracteres é um ou mais valores ASCII.  Ele pode ser especificado como um caractere (por exemplo, -s *) ou como um valor hexadecimal (por exemplo, -s 0x22 para aspas duplas).  
  
Exemplos:  
  
-s *  
  
-s 0x22  
  
< fixed_width_column_options >  
As opções para um arquivo de dados de origem que tem colunas de comprimento fixo. Por padrão, *source_data_file_name* contém caracteres ASCII em colunas de comprimento variável.  
  
Não há suporte para colunas de largura fixa quando – e é UTF8.  
  
**-w** *fixed_width_config_file*  
Caminho e nome do arquivo de configuração que especifica o número de caracteres em cada coluna. Cada campo deve ser especificado.  
  
Esse arquivo deve residir no servidor de carregamento. O caminho pode ser um caminho UNC, relativo ou absoluto. Cada linha no *fixed_width_config_file* contém o nome de uma coluna e o número de caracteres para a coluna. Há uma linha por coluna, da seguinte maneira e a ordem em que o arquivo deve corresponder à ordem na tabela de destino:  
  
*nome da coluna*=*num_chars*  
  
*nome da coluna*=*num_chars*  
  
Exemplo de arquivo de configuração de largura foram corrigidos:  
  
SalesCode = 3  
  
SalesID = 10  
  
Exemplo de linhas no *source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
No exemplo anterior, a primeira linha carregada terá SalesCode = '230' e SalesID = 'Shirts0056'. A segundo carregada linha terá SalesCode = '320' e SaleID = 'Towels1356'.  
  
Para obter informações sobre como lidar com à esquerda e à direita de conversão de tipo de dados ou espaços no modo de largura fixa, consulte [para dwloader as regras de conversão de tipo de dados](dwloader-data-type-conversion-rules.md).  
  
**-e** *character_encoding*  
Especifica um tipo de codificação de caracteres para os dados a serem carregadas do arquivo de dados. Opções são ASCII (padrão), UTF8, UTF16 ou UTF16BE, onde UTF16 é pouco endian e UTF16BE é big endian. Essas opções diferenciam maiusculas de minúsculas.  
  
Não há suporte para colunas de largura fixa quando – e é UTF8.  
  
**-r** *row_delimiter*  
O delimitador para cada linha do arquivo de dados de origem. O delimitador de linha é um ou mais valores ASCII.  
  
Para especificar um retorno de carro (CR), alimentação de linha (LF) ou caractere de tabulação como um delimitador, você pode usar os caracteres de escape (\r, \n, \t) ou seus valores hexadecimais (0 x, 0d 09). Para especificar outros caracteres especiais como delimitadores, use o valor hexadecimal.  
  
Exemplos de CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Exemplos de CR:  
  
-r \r  
  
-r 0x0d  
  
Exemplos de LF:  
  
\n - r  
  
-r 0x0a  
  
Um LF é necessária para Unix. Uma CR é necessária para o Windows.  
  
**-D** { **ymd** | ydm | MDA | myd |  DMA | dym | *custom_date_format* }  
Especifica a ordem de dia (d), mês (m) e ano (y) para todos os campos de data/hora no arquivo de entrada. A ordem padrão é ymd. Para especificar vários formatos de ordem para o mesmo arquivo de origem, use a opção – dt.  
  
YMD | DMA  
ydm e DMA permitem que os mesmos formatos de entrada. Permitem que o ano a ser no início ou no final da data. Por exemplo, para ambos **ydm** e **DMA** data formatos, você poderia ter 2013-02-03 ou 02-03-2013 no arquivo de entrada.  
  
ydm  
Você só pode carregar entrada formatada como ydm em colunas de dados tipo datetime e smalldatetime. Você não pode carregar ydm valores em uma coluna do tipo de dados datetimeoffset, data ou datetime2.  
  
mda  
MDA permite <month> <space> <day> <comma> <year>.  
  
Exemplos de dados de entrada de MDA para 1 de janeiro de 1975:  
  
-   1 de janeiro de 1975  
  
-   01 de janeiro de 75  
  
-   1/Jan/75  
  
-   01011975  
  
mad  
Exemplos de arquivos de entrada para março 04,2010: 2010-03-04, 2010/3/4  
  
dam  
Exemplos de arquivos de entrada para 04 de março de 2010: 2010-04-03, 2010/4/3  
  
*custom_date_format*  
*custom_date_format* é um formato de data personalizada (por exemplo, dd/MM/AAAA) e incluído para fins de compatibilidade com versões anteriores. dwloader não enfoce não o formato de data personalizada. Em vez disso, quando você especifica um formato de data personalizada, **dwloader** converterá a configuração correspondente de ymd, ydm, mda, myd, dym ou DMA.  
  
Por exemplo, se você especificar – D dd/MM/AAAA, dwloader espera que todos os data de entrada sejam ordenados pela primeira vez, com o mês e dia e ano (DMA). Ele não impõe 2 meses de caractere, 2 dias dígito e anos de 4 dígitos conforme especificado pelo formato de data personalizada. Aqui estão alguns exemplos de como as datas podem ser formatadas no arquivo de entrada quando o formato de data é – D dd/MM/AAAA: 01/02/2013, Jan.02.2013, 1/2/2013  
  
Para obter informações mais abrangentes de formatação, consulte [para dwloader as regras de conversão de tipo de dados](dwloader-data-type-conversion-rules.md).  
  
**-dt** *datetime_format_file*  
Cada formato de data e hora é especificado em um arquivo chamado *datetime_format_file*. Ao contrário dos parâmetros de linha de comando, parâmetros de arquivo que incluem espaços não devem ser entre aspas duplas. Você não pode alterar o formato de data e hora como carregar dados. O arquivo de dados de origem e sua coluna correspondente na tabela de destino devem ter o mesmo formato.  
  
Cada linha contém o nome de uma coluna na tabela de destino e seu formato de data e hora.  
  
Exemplos:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
O nome do banco de dados que contém a tabela de preparo. O padrão é o banco de dados especificado com a opção -T, que é o banco de dados da tabela de destino. Para obter mais informações sobre como usar um banco de dados de preparo, consulte [criar o banco de dados de preparo](staging-database.md).  
  
**-M** *load_mode_option*  
Especifica se deve acrescentar upsert, ou recarregar os dados. O modo padrão é anexar.  
  
Acrescentar  
O carregador insere linhas ao final de linhas existentes na tabela de destino.  
  
fastappend  
O carregador insere linhas diretamente, sem usar uma tabela temporária, ao final de linhas existentes na tabela de destino. fastappend requer que a transação de vários (– m) opção. Um banco de dados de preparo não pode ser especificado ao usar fastappend. Não há nenhuma reversão com fastappend, o que significa que a recuperação de uma falha ou anulada carga deve ser tratada pelo seu próprio processo de carregamento.  
  
upsert **-K***merge_column* [,... *n* ]  
O carregador usa a instrução de mesclagem do SQL Server para atualizar as linhas existentes e inserir novas linhas.  
  
A opção -K Especifica a coluna ou colunas a base de dados de mesclagem. Essas colunas formam uma chave de mesclagem, que deve representar uma linha exclusiva. Se a chave de mesclagem existir na tabela de destino, a linha é atualizada. Se a chave de mesclagem não existe na tabela de destino, a linha será acrescentada.  
  
Para tabelas de hash distribuída, a chave de mesclagem deve ser ou incluir a coluna de distribuição.  
  
Para tabelas replicadas, a chave de mesclagem é a combinação de uma ou mais colunas. Essas colunas são especificadas de acordo com as necessidades do aplicativo.  
  
Várias colunas devem ser separados por vírgula, sem espaços ou separados por vírgula com espaços e colocadas entre aspas simples.  
  
Se duas linhas na tabela de origem tiverem valores de chave de mesclagem correspondente, suas respectivas linhas devem ser idênticas.  
  
Recarregar  
O carregador trunca a tabela de destino antes que ela insira os dados de origem.  
  
**-b** *batchsize*  
Recomendado apenas para uso pelo Microsoft Support *batchsize* é o tamanho do lote do SQL Server para a cópia em massa que DMS executa em instâncias do SQL Server em nós de computação.  Quando *batchsize* for especificado, SQL Server PDW substituirá o tamanho de carregamento do lote é calculado dinamicamente para cada carga.  
  
A partir do SQL Server 2012 PDW, o nó de controle calcula dinamicamente um tamanho de lote para cada carga por padrão. Esse cálculo automático baseia-se em vários parâmetros, como o tamanho da memória, tipo de tabela de destino, esquema de tabela de destino, tipo de carga, tamanho do arquivo e classe de recurso do usuário.  
  
Por exemplo, se o modo de carga é FASTAPPEND e a tabela tem um índice columnstore clusterizado, SQL Server PDW será pela tentativa de padrão para usar um tamanho de lote de 1.048.576 para que os rowgroups irá se tornar FECHADOS e carga diretamente para o columnstore sem passar pelo repositório delta. Se a memória não permite que o tamanho do lote de 1.048.576, dwloader escolherá um tamanho de lote menor.  
  
Se o tipo de carga for FASTAPPEND, o *batchsize* se aplica a carregar dados para a tabela, caso contrário, *batchsize* se aplica a carregar dados para a tabela de preparo.  
  
< reject_options >  
Especifica opções para determinar o número de falhas de carregamento que permitirá que o carregador. Se as falhas de carga excederem o limite, o carregador será interrompida e não confirmar todas as linhas.  
  
**-rt** { **valor** | porcentagem}  
Especifica se-*reject_value* no **-rv** *reject_value* opção é um literal número de linhas (valor) ou uma taxa de falha (porcentagem). O padrão é o valor.  
  
A opção de porcentagem é um cálculo em tempo real que ocorre em intervalos de acordo com a opção - rs.  
  
Por exemplo, se o carregador tenta carregar 100 linhas e 25 falha e 75 bem-sucedida, a taxa de falha é 25%.  
  
**-rv** *reject_value*  
Especifica o número ou porcentagem de rejeições da linha permitidas antes de interromper a carga. O **-rt** opção determina se *reject_value* refere-se ao número de linhas ou a porcentagem de linhas.  
  
O padrão *reject_value* é 0.  
  
Quando usado com o valor de -rt, o carregador interrompe a carga quando a contagem de linhas rejeitadas excede reject_value.  
  
Quando usar com a porcentagem de -rt, o carregador calcula a porcentagem de intervalos (-opção de rs). Portanto, a porcentagem de linhas com falha pode exceder *reject_value*.  
  
**-rs** *reject_sample_size*  
Usado com o `-rt percentage` opção para especificar as verificações de porcentagem incremental. Por exemplo, se reject_sample_size é 1000, o carregador calcula a porcentagem de linhas com falha depois que ele tentou carregar 1000 linhas. Recalcular a porcentagem de linhas com falha depois que ele tenta carregar cada 1000 linhas adicionais.  
  
**-c**  
Remove os caracteres de espaço em branco à esquerda e direita de char, nchar, varchar e nvarchar campos. Converte cada campo que contém somente caracteres de espaço em branco para a cadeia de caracteres vazia.  
  
Exemplos:  
  
' ' será truncado para '  
  
'abc' será truncado para 'abc'  
  
Quando a c é usada com -E, a operação – E ocorre pela primeira vez. Os campos que contêm apenas caracteres de espaço em branco são convertidos para cadeia de caracteres vazia e não nulo.  
  
**-E**  
Converta cadeias de caracteres vazias em NULL. O padrão é não realizar estas conversões.  
  
**-m**  
Use o modo de várias transações para a segunda fase de carregamento; Quando o carregamento de dados da tabela de preparo para uma tabela distribuída.  
  
Com **– m**, SQL Server PDW executa e confirma o carrega em paralelo. Isso executa muito mais rapidamente do que o padrão de modo de carregamento, mas não é segura para a transação.  
  
Sem **– m**, SQL Server PDW executa e confirma o carrega em série entre as distribuições em cada nó de computação e, simultaneamente, entre os nós de computação. Esse método é mais lento que o modo de transação várias, mas é segura para a transação.  
  
**-m** é opcional para *acrescentar*, *recarregar*, e *upsert*.  
  
**-m** é necessária para fastappend.  
  
**-m** não pode ser usado com tabelas replicadas.  
  
**-m** aplica-se somente a segunda fase de carregamento. Não é aplicável para a primeira fase de carregamento; Carregando dados na tabela de preparo.  
  
Não há nenhuma reversão com o modo de várias transações, o que significa que a recuperação de uma falha ou anulada carga deve ser tratada pelo seu próprio processo de carregamento.  
  
É recomendável usar **– m** apenas ao carregar em uma tabela vazia, para que você possa recuperar sem perda de dados. Para se recuperar de uma falha de carregamento: descartar a tabela de destino, resolva o problema de carga, recrie a tabela de destino e execute a carga novamente.  
  
**-N**  
Verifique se que o dispositivo de destino tem um certificado válido do SQL Server PDW de uma autoridade confiável. Use isso para ajudar a garantir que seus dados não está sendo roubados por um invasor e enviadas para um local não autorizado. O certificado já deve estar instalado no dispositivo. É a única maneira com suporte para instalar o certificado para o administrador do aplicativo para instalá-lo usando a ferramenta Gerenciador de configuração. Peça ao administrador do dispositivo se você não estiver certo se o dispositivo tem um certificado instalado.  
  
**-se**  
Ignorar carregamento de arquivos vazios. Isso também ignora descompactando arquivos gzip vazio.  
  
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
Requer permissão de carga e permissões aplicáveis (INSERT, UPDATE, DELETE) na tabela de destino. Requer a permissão de criar (para criar uma tabela temporária) do banco de dados de preparo. Se um banco de dados de preparo não for usado, a permissão Criar é necessário no banco de dados de destino. 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>Comentários gerais  
Para obter informações sobre conversões de tipos de dados ao carregar com dwloader, consulte [para dwloader as regras de conversão de tipo de dados](dwloader-data-type-conversion-rules.md).  
  
Se um parâmetro inclui um ou mais espaços, coloque o parâmetro com aspas duplas.  
  
Você deve executar o carregador de seu local de instalação. O executável de dwloader pré-instalado com o dispositivo e está localizado no diretório C:\Program Files\Microsoft SQL Server dados Warehouse\DWLoader.  
  
Você pode substituir um parâmetro que é especificado no arquivo de parâmetro (-opção f) especificando-o como um parâmetro de linha de comando.  
  
Você pode executar várias instâncias do carregador de simultaneamente. O número máximo de instâncias de carregador é pré-configurado e não pode ser alterado. 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
Dados carregados podem exigir mais ou menos espaço no dispositivo que no local de origem. Você pode executar importações de teste com subconjuntos de dados para estimar o consumo de disco.  
  
Embora **dwloader** é um processo de transação e reverterá normalmente em caso de falha, ele não poderá ser revertido quando o carregamento em massa foi concluído com êxito. Para cancelar um ativo **dwloader** processo, digite CTRL + C.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
O tamanho total de todas as cargas ocorram simultaneamente deve ser menor do que LOG_SIZE para o banco de dados, e é recomendável que o tamanho total de todas as cargas simultâneas é menos de 50% a LOG_SIZE. Para obter essa limitação de tamanho, você pode dividir grandes cargas em vários lotes. Para obter mais informações sobre LOG_SIZE, consulte [criar banco de dados](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
Ao carregar vários arquivos com um comando, todas as linhas rejeitadas são gravadas no mesmo arquivo de rejeição. O arquivo de rejeição não mostra qual arquivo de entrada contém cada linha rejeitada.  
  
A cadeia de caracteres vazia não deve ser usada como um delimitador. Quando uma cadeia de caracteres vazia é usada como um delimitador de linha, o carregamento falhará. Quando usado como o delimitador de coluna, a carga ignora o delimitador e continua a usar o padrão "|" como o delimitador de coluna. Quando usado como o delimitador de cadeia de caracteres, a cadeia de caracteres vazia é ignorada e o comportamento padrão é aplicado.  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
**dwloader** comportamento de bloqueio varia dependendo do *load_mode_option*.  
  
-   **acrescentar** – anexar é recomendada e a opção mais comum. Acrescente carrega dados em uma tabela de preparo. O bloqueio é descrito em detalhes abaixo.  
  
-   **Acrescentar rápido** – acrescentar Fast carrega diretamente para a tabela final colocar um bloqueio de tabela ExclusiveUpdate e é o único modo que não usa uma tabela de preparo.  
  
-   **Recarregar** – recarregar carrega dados em uma tabela de preparo e requer um bloqueio exclusivo na tabela de preparo e a tabela final. Recarregar não é recomendado para as operações simultâneas.  
  
-   **upsert** – Upsert carrega dados em uma tabela de preparo e, em seguida, executa uma operação de mesclagem da tabela de preparo para a tabela final. Upsert não requerem bloqueios exclusivos na tabela final. O desempenho pode variar quando usando upsert. Teste o comportamento em seu ambiente.  
  
### <a name="locking-behavior"></a>Comportamento de bloqueio  
**Um bloqueio de modo de acréscimo**  
  
Acrescentar pode ser executado no modo multi-transacional (usando o argumento – m), mas não é seguro de transação. Acrescentar, portanto, deve ser usado como uma operação transacional (sem usar o argumento – m). Infelizmente, durante a operação INSERT SELECT final, o modo transacional é atualmente aproximadamente seis vezes mais lento do que o modo de várias transações.  
  
O modo de acréscimo carrega dados em duas fases. A fase um carrega dados do arquivo de origem em uma tabela de preparo simultaneamente (poderá ocorrer fragmentação). Fase dois carrega os dados da tabela de preparo para a tabela final. A segunda fase executa um **INSERT INTO... Selecione WITH (TABLOCK)** operação. A tabela a seguir mostra o comportamento de bloqueio na tabela final e o comportamento de log ao usar o modo de acréscimo:  
  
|Tipo de tabela|Transações múltiplas<br />Modo (-m)|Tabela estiver vazia|Suportada de simultaneidade|Log|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|Pilha|Sim|Sim|Sim|mínimo|  
|Pilha|Sim|não|Sim|mínimo|  
|Pilha|não|Sim|não|mínimo|  
|Pilha|não|não|não|mínimo|  
|Cl|Sim|Sim|não|mínimo|  
|Cl|Sim|não|Sim|Completo|  
|Cl|não|Sim|não|mínimo|  
|Cl|não|não|Sim|Completo|  
  
Mostra a tabela acima **dwloader** usando o modo de acréscimo carregar em um heap ou uma tabela de índice clusterizado (CI), com ou sem o sinalizador várias transacional e carregar em uma tabela vazia ou uma tabela não vazia. O bloqueio e registro em log o comportamento de cada essa combinação de carga é exibido na tabela. Por exemplo, carregando fase (2) com o modo de acréscimo em um índice clusterizado sem modo multi transacional e em vazio tabela terão PDW criar um bloqueio exclusivo na tabela e registro em log é mínimo. Isso significa que um cliente não poderá carregar (2º) fase e consulta simultaneamente em uma tabela vazia. No entanto, ao carregar com a mesma configuração em uma tabela não vazia, PDW não emitirá um bloqueio exclusivo na tabela e simultaneidade é possível. Infelizmente, registro em log completo ocorre, diminuindo o processo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-dwloader-example"></a>A. Exemplo de dwloader simples  
O exemplo a seguir mostra a iniciação do **carregador** com apenas as opções necessárias selecionadas. Outras opções são extraídas do arquivo de configuração global, *loadparamfile.txt*.  
  
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
  
Exemplo de uso de argumentos para um arquivo de origem e o arquivo de erro.  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. Carregar dados em uma tabela da AdventureWorks  
O exemplo a seguir faz parte de um script em lotes que carrega dados em **AdventureWorksPDW2012**.  Para exibir o script completo, abra o arquivo de aw_create.bat que acompanha o **AdventureWorksPDW2012** pacote de instalação. 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

O trecho de script a seguir usa dwloader para carregar dados nas tabelas DimAccount e DimCurrency. Esse script está usando um endereço Ethernet. Se ele estava usando InfiniBand, servidor seria *< appliance_name >*`-SQLCTL01`.  
  
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
  
A seguir está o DDL para a tabela DimAccount.  
  
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
  
Este é um exemplo do arquivo de dados, DimAccount.txt, que contém dados a serem carregados na tabela DimAccount.  
  
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
  
### <a name="c-load-data-from-the-command-line"></a>C. Carregar dados de linha de comando  
O script no exemplo B pode ser substituído por inserir todos os parâmetros na linha de comando, conforme mostrado no exemplo a seguir.  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe –S <Control node IP> -E –M reload –e UTF16 -i .\DimAccount.txt –T AdventureWorksPDW2012.dbo.DimAccount –R DimAccount.bad –t "|" –r \r\n –U <login> -P <password>  
```  
  
Descrição dos parâmetros de linha de comando:  
  
-   *C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe* é o local de instalação do dwloader.exe.  
  
-   *-S* é seguido pelo endereço IP do nó de controle.  
  
-   *-E* especifica para carregar as cadeias de caracteres vazias como nulas.  
  
-   *-M recarregar* especifica para truncar a tabela de destino antes que ela insira os dados de origem.  
  
-   *-e UTF16* indica que o arquivo de origem usa o tipo de codificação de caractere endian pouco.  
  
-   *-i.\DimAccount.txt* Especifica os dados em um arquivo chamado DimAccount.txt que existe no diretório atual.  
  
-   *-T AdventureWorksPDW2012.dbo.DimAccount* Especifica o nome de 3 partes da tabela para receber os dados.  
  
-   *-R DimAccount.bad* Especifica as linhas que não carregarão serão gravadas em um arquivo chamado DimAccount.bad.  
  
-   *– t "|"*  indica os campos no arquivo de entrada, DimAccount.txt, são separados com o caractere de pipe.  
  
-   *-r \r\n* Especifica cada linha na DimAccount.txt termina com um retorno de carro e o caractere de alimentação de uma linha.  
  
-   *-U < login_name > -P <password>*  Especifica o logon e a senha para o logon que tenha permissões para executar o carregamento.  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
