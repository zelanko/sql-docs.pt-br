---
title: Chamando um procedimento armazenado (OLE DB) | Microsoft Docs
description: Chamando um procedimento armazenado (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- RPC escape sequence
- OLE DB, stored procedures
- parameters [OLE DB Driver for SQL Server], OLE DB
- ODBC CALL escape sequence
- stored procedures [OLE DB], calling
- OLE DB Driver for SQL Server, stored procedures
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 26e97354d54cb65578bcbb35d2c96fb6914270d6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015202"
---
# <a name="stored-procedures---calling"></a>Procedimentos armazenados – Chamando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Um procedimento armazenado pode ter zero ou mais parâmetros. Também pode retornar um valor. Ao usar o Driver do OLE DB para SQL Server, os parâmetros para um procedimento armazenado podem ser transmitidos da seguinte forma:  
  
-   Hard-coding o valor de dados.  
  
-   Usando um marcador de parâmetro (?) para especificar parâmetros, associar uma variável de programa ao marcador de parâmetro e, em seguida, inserir o valor dos dados na variável de programa.  
  
> [!NOTE]  
>  Ao chamar procedimentos armazenados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que usam parâmetros denominados com o OLE DB, os nomes de parâmetros devem começar com o caractere '\@'. Esta é uma restrição específica do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O Driver do OLE DB para SQL Server impõe esta restrição mais estritamente que o MDAC.  
  
 Para dar suporte aos parâmetros, a interface **ICommandWithParameters** é exposta no objeto de comando. Para usar parâmetros, o consumidor primeiro descreve os parâmetros para o provedor, chamando o método **ICommandWithParameters::SetParameterInfo** (ou, como opção, prepara uma instrução de chamada que chama o método **GetParameterInfo**). O consumidor cria um acessador que especifica a estrutura de um buffer e coloca os valores dos parâmetros nesse buffer. Finalmente, ele transmite o identificador do acessador e um ponteiro ao buffer para **Executar**. Em chamadas posteriores para **Executar**, o consumidor coloca novos valores de parâmetros no buffer e chama **Executar** com o identificador do acessador e o ponteiro do buffer.  
  
 Um comando que chama um procedimento armazenado temporário usando parâmetros deve primeiro chamar **ICommandWithParameters::SetParameterInfo** para definir as informações do parâmetro, para que o comando possa ser preparado com êxito. Isto ocorre porque o nome interno de um procedimento armazenado temporário difere do nome externo usado por um cliente e MSOLEDBSQL não pode consultar as tabelas do sistema para determinar as informações dos parâmetros para um procedimento armazenado temporário.  
  
 Estas são as etapas no processo de associação de parâmetros:  
  
1.  Preencha as informações dos parâmetros em uma matriz de estruturas DBPARAMBINDINFO; isto é, nome do parâmetro, nome específico do provedor para o tipo de dados do parâmetro ou um nome de tipo de dados padrão, e assim por diante. Cada estrutura na matriz descreve um parâmetro. Em seguida, essa matriz é transmitida ao método **SetParameterInfo**.  
  
2.  Chame o método **ICommandWithParameters::SetParameterInfo** para descrever parâmetros ao provedor. **SetParameterInfo** especifica o tipo de dados nativo de cada parâmetro. Os argumentos de **SetParameterInfo** são:  
  
    -   O número de parâmetros para o qual definir informações de tipo.  
  
    -   Uma matriz de ordinais de parâmetro para a qual definir informações de tipo.  
  
    -   Uma matriz de estruturas DBPARAMBINDINFO.  
  
3.  Crie um acessador de parâmetro usando o comando **IAccessor::CreateAccessor**. O acessador especifica a estrutura de um buffer e coloca valores dos parâmetros no buffer. O comando **CreateAccessor** cria um acessador de um conjunto de associações. Essas associações são descritas pelo consumidor usando uma matriz de estruturas DBBINDING. Cada associação liga um único parâmetro ao buffer do consumidor e contém informações como:  
  
    -   O ordinal do parâmetro ao qual a associação se aplica.  
  
    -   O que é associado (o valor de dados, seu comprimento e seu status).  
  
    -   O deslocamento no buffer para cada uma destas partes.  
  
    -   O comprimento e o tipo do valor de dados, como existe no buffer do consumidor.  
  
     Um acessador é reconhecido por seu identificador, que é do tipo HACCESSOR. Esse identificador é retornado pelo método **CreateAccessor**. Sempre que o consumidor termina de usar um acessador, o consumidor deve chamar o método **ReleaseAccessor** para liberar a memória que ele detém.  
  
     Quando o consumidor chama um método, como **ICommand::Execute**, transmite o identificador a um acessador e um ponteiro para um buffer propriamente dito. O provedor usa esse acessador para determinar como transferir os dados contidos no buffer.  
  
4.  Preencha a estrutura DBPARAMS. As variáveis do consumidor das quais os valores dos parâmetros são obtidos e nas quais os valores dos parâmetros de saída são gravados são transmitidas em tempo de execução para **ICommand::Execute** na estrutura DBPARAMS. A estrutura DBPARAMS inclui três elementos:  
  
    -   Um ponteiro para o buffer do qual o provedor recupera dados de parâmetro de entrada e para o qual o provedor retorna dados de parâmetro de saída, de acordo com as associações especificadas pelo identificador do acessador.  
  
    -   O número de conjuntos de parâmetros no buffer.  
  
    -   O identificador do acessador criado na Etapa 3.  
  
5.  Execute o comando usando **ICommand::Execute**.  
  
## <a name="methods-of-calling-a-stored-procedure"></a>Métodos de chamar um procedimento armazenado  
 Ao executar um procedimento armazenado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o Driver do OLE DB para SQL Server dá suporte para:  
  
-   Sequência de escape CALL do ODBC.  
  
-   Sequência de escape RPC (Chamada de Procedimento Remoto).  
  
-   Instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE.  
  
### <a name="odbc-call-escape-sequence"></a>Sequência de escape ODBC CALL  
 Se você souber informações de parâmetro, chame o método **ICommandWithParameters::SetParameterInfo** para descrever os parâmetros ao provedor. Caso contrário, quando a sintaxe ODBC CALL for usada na chamada de um procedimento armazenado, o provedor chamará uma função auxiliar para localizar as informações de parâmetros do procedimento armazenado.  
  
 Se você não tiver certeza sobre as informações de parâmetro (metadados de parâmetro), a sintaxe do ODBC CALL será recomendada.  
  
 A sintaxe geral para chamar um procedimento usando a sequência de escape ODBC CALL é:  
  
 {[ **? =** ]**chamar**_procedimento\_nome_[ **(** [*parâmetro*] [ **,** [_parâmetro_]]... **)** ]}  
  
 Por exemplo:  
  
```  
{call SalesByCategory('Produce', '1995')}  
```  
  
### <a name="rpc-escape-sequence"></a>Sequência de escape RPC  
 A sequência de escape RPC é semelhante à sintaxe ODBC CALL de chamar um procedimento armazenado. Se você for chamar o procedimento várias vezes, a sequência de escape RPC proporcionará o melhor desempenho possível entre os três métodos de chamada de um procedimento armazenado.  
  
 Quando a sequência de escape RPC é usada para executar um procedimento armazenado, o provedor não chama nenhuma função auxiliar para determinar as informações dos parâmetros (como ela faz no caso da sintaxe de ODBC CALL). A sintaxe de RPC é mais simples que a sintaxe de ODBC CALL, assim o comando é analisado mais rápido, melhorando o desempenho. Neste caso, você precisa fornecer as informações de parâmetro executando **ICommandWithParameters::SetParameterInfo**.  
  
 A sequência de escape RPC exige que você tenha um valor de retorno. Se o procedimento armazenado não retornar um valor, o servidor retornará um 0 por padrão. Além disso, você não pode abrir um cursor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no procedimento armazenado. O procedimento armazenado é implicitamente preparado e a chamada a **ICommandPrepare::Prepare** falhará. Devido à impossibilidade de preparar uma chamada RPC, você não pode consultar metadados de coluna; IColumnsInfo::GetColumnInfo e IColumnsRowset::GetColumnsRowset retornarão DB_E_NOTPREPARED.  
  
 Se você souber todos os metadados de parâmetro, a sequência de escape RPC será o modo recomendado para executar procedimentos armazenados.  
  
 Este é um exemplo de sequência de escape RPC para chamar um procedimento armazenado:  
  
```  
{rpc SalesByCategory}  
```  
  
 Para um aplicativo de exemplo que demonstra uma sequência de escape RPC, confira [Executar um procedimento armazenado &#40;usando a sintaxe RPC&#41; e processar códigos de retorno e parâmetros de saída &#40;OLE DB&#41;](../../oledb/ole-db-how-to/results/execute-stored-procedure-with-rpc-and-process-output.md).  
  
### <a name="transact-sql-execute-statement"></a>Instrução Transact-SQL EXECUTE  
 A sequência de escape ODBC CALL e a sequência de escape RPC são os métodos preferidos para chamar um procedimento armazenado no lugar da instrução [EXECUTE](../../../t-sql/language-elements/execute-transact-sql.md). O Driver do OLE DB para SQL Server usa o mecanismo de RPC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para otimizar o processamento do comando. Este protocolo de RPC aumenta o desempenho, eliminando grande parte do processamento de parâmetros e da análise da instrução feita no servidor.  
  
 Este é um exemplo da instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]EXECUTE**do**:  
  
```  
EXECUTE SalesByCategory 'Produce', '1995'  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados](../../oledb/ole-db/stored-procedures.md)  
  
  
