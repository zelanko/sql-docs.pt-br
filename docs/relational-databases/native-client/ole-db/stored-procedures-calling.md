---
title: Chamar um procedimento armazenado (OLE DB) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- RPC escape sequence
- OLE DB, stored procedures
- parameters [SQL Server Native Client], OLE DB
- ODBC CALL escape sequence
- stored procedures [OLE DB], calling
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: 8e5738e5-4bbe-4f34-bd69-0c0633290bdd
caps.latest.revision: "39"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: caf634af86e7338d25ae18a2101cffabb9f5f762
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="stored-procedures---calling"></a>Procedimentos armazenados - chamar
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Um procedimento armazenado pode ter zero ou mais parâmetros. Também pode retornar um valor. Ao usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor Native Client OLE DB, parâmetros para um procedimento armazenado podem ser transmitidos por:  
  
-   Hard-coding o valor de dados.  
  
-   Usando um marcador de parâmetro (?) para especificar parâmetros, associar uma variável de programa ao marcador de parâmetro e, em seguida, inserir o valor dos dados na variável de programa.  
  
> [!NOTE]  
>  Ao chamar procedimentos armazenados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que usam parâmetros denominados com o OLE DB, os nomes de parâmetros devem começar com o caractere '@'. Esta é uma restrição específica do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client impõe esta restrição mais estritamente que o MDAC.  
  
 Para dar suporte a parâmetros, o **ICommandWithParameters** interface é exposta no objeto de comando. Para usar parâmetros, o consumidor primeiro descreve os parâmetros para o provedor, chamando o **ICommandWithParameters:: SetParameterInfo** método (ou, opcionalmente, prepara uma instrução de chamada que chama o **GetParameterInfo** método). O consumidor cria um acessador que especifica a estrutura de um buffer e coloca os valores dos parâmetros nesse buffer. Finalmente, ele passa o identificador do acessador e um ponteiro para o buffer de **Execute**. Em chamadas posteriores para **Execute**, o consumidor coloca novos valores de parâmetro no buffer e chama **Execute** com o ponteiro de buffer e o identificador do acessador.  
  
 Um comando que chama um procedimento armazenado temporário usando parâmetros deve primeiro chamar **ICommandWithParameters:: SetParameterInfo** para definir as informações de parâmetro antes do comando pode ser preparado com êxito. Isto ocorre porque o nome interno de um procedimento armazenado temporário difere do nome externo usado por um cliente e SQLOLEDB não pode consultar as tabelas do sistema para determinar as informações dos parâmetros para um procedimento armazenado temporário.  
  
 Estas são as etapas no processo de associação de parâmetros:  
  
1.  Preencha as informações dos parâmetros em uma matriz de estruturas DBPARAMBINDINFO; isto é, nome do parâmetro, nome específico do provedor para o tipo de dados do parâmetro ou um nome de tipo de dados padrão, e assim por diante. Cada estrutura na matriz descreve um parâmetro. Esta matriz é então passada para o **SetParameterInfo** método.  
  
2.  Chamar o **ICommandWithParameters:: SetParameterInfo** método para descrever parâmetros ao provedor. **SetParameterInfo** Especifica o tipo de dados nativo de cada parâmetro. **SetParameterInfo** argumentos são:  
  
    -   O número de parâmetros para o qual definir informações de tipo.  
  
    -   Uma matriz de ordinais de parâmetro para a qual definir informações de tipo.  
  
    -   Uma matriz de estruturas DBPARAMBINDINFO.  
  
3.  Criar um acessador de parâmetro usando o **IAccessor:: CreateAccessor** comando. O acessador especifica a estrutura de um buffer e coloca valores dos parâmetros no buffer. O **CreateAccessor** comando cria um acessador de um conjunto de associações. Essas associações são descritas pelo consumidor usando uma matriz de estruturas DBBINDING. Cada associação liga um único parâmetro ao buffer do consumidor e contém informações como:  
  
    -   O ordinal do parâmetro ao qual a associação se aplica.  
  
    -   O que é associado (o valor de dados, seu comprimento e seu status).  
  
    -   O deslocamento no buffer para cada uma destas partes.  
  
    -   O comprimento e o tipo do valor de dados, como existe no buffer do consumidor.  
  
     Um acessador é reconhecido por seu identificador, que é do tipo HACCESSOR. Esse identificador é retornado pelo **CreateAccessor** método. Sempre que o consumidor termina de usar um acessador, o consumidor deve chamar o **ReleaseAccessor** método para liberar a memória que ele contém.  
  
     Quando o consumidor chama um método, como **ICommand:: execute**, ele passa o identificador para um acessador e um ponteiro para um buffer propriamente dito. O provedor usa esse acessador para determinar como transferir os dados contidos no buffer.  
  
4.  Preencha a estrutura DBPARAMS. As variáveis do consumidor do parâmetro de entrada que os valores são obtidos e para o parâmetro de saída, os valores são gravados são passadas em tempo de execução para **ICommand:: execute** na estrutura DBPARAMS. A estrutura DBPARAMS inclui três elementos:  
  
    -   Um ponteiro para o buffer do qual o provedor recupera dados de parâmetro de entrada e para o qual o provedor retorna dados de parâmetro de saída, de acordo com as associações especificadas pelo identificador do acessador.  
  
    -   O número de conjuntos de parâmetros no buffer.  
  
    -   O identificador do acessador criado na Etapa 3.  
  
5.  Execute o comando usando **ICommand:: execute**.  
  
## <a name="methods-of-calling-a-stored-procedure"></a>Métodos de chamar um procedimento armazenado  
 Ao executar um procedimento armazenado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte ao provedor do OLE DB Native Client a:  
  
-   Sequência de escape CALL do ODBC.  
  
-   Sequência de escape RPC (Chamada de Procedimento Remoto).  
  
-   Instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE.  
  
### <a name="odbc-call-escape-sequence"></a>Sequência de Escape ODBC CALL  
 Se você souber informações de parâmetro, chame **ICommandWithParameters:: SetParameterInfo** método para descrever os parâmetros para o provedor. Caso contrário, quando a sintaxe ODBC CALL for usada na chamada de um procedimento armazenado, o provedor chamará uma função auxiliar para localizar as informações de parâmetros do procedimento armazenado.  
  
 Se você não tiver certeza sobre as informações de parâmetro (metadados de parâmetro), a sintaxe do ODBC CALL será recomendada.  
  
 A sintaxe geral para chamar um procedimento usando a sequência de escape ODBC CALL é:  
  
 {[**?=**]**call***procedure_name*[**(**[*parameter*][**,**[*parameter*]]... **)**]}  
  
 Por exemplo:  
  
```  
{call SalesByCategory('Produce', '1995')}  
```  
  
### <a name="rpc-escape-sequence"></a>Sequência de Escape RPC  
 A sequência de escape RPC é semelhante à sintaxe ODBC CALL de chamar um procedimento armazenado. Se você for chamar o procedimento várias vezes, a sequência de escape RPC proporcionará o melhor desempenho possível entre os três métodos de chamada de um procedimento armazenado.  
  
 Quando a sequência de escape RPC é usada para executar um procedimento armazenado, o provedor não chama nenhuma função auxiliar para determinar as informações dos parâmetros (como ela faz no caso da sintaxe de ODBC CALL). A sintaxe de RPC é mais simples que a sintaxe de ODBC CALL, assim o comando é analisado mais rápido, melhorando o desempenho. Nesse caso, você precisa fornecer as informações de parâmetro executando **ICommandWithParameters:: SetParameterInfo**.  
  
 A sequência de escape RPC exige que você tenha um valor de retorno. Se o procedimento armazenado não retornar um valor, o servidor retornará um 0 por padrão. Além disso, você não pode abrir um cursor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no procedimento armazenado. O procedimento armazenado é implicitamente preparado e a chamada para **icommandprepare:: Prepare** falhará. Devido à impossibilidade de preparar uma chamada RPC, você não pode consultar metadados de coluna; Icolumnsinfo:: Getcolumninfo e IColumnsRowset:: Getcolumnsrowset retornarão DB_E_NOTPREPARED.  
  
 Se você souber todos os metadados de parâmetro, a sequência de escape RPC será o modo recomendado para executar procedimentos armazenados.  
  
 Este é um exemplo de sequência de escape RPC para chamar um procedimento armazenado:  
  
```  
{rpc SalesByCategory}  
```  
  
 Para um aplicativo de exemplo que demonstra uma sequência de escape RPC, consulte [executar um procedimento armazenado &#40; Usando a sintaxe de RPC &#41; e processar o retorno códigos e parâmetros de saída &#40; OLE DB &#41; ](../../../relational-databases/native-client-ole-db-how-to/results/execute-stored-procedure-with-rpc-and-process-output.md).  
  
### <a name="transact-sql-execute-statement"></a>Instrução Transact-SQL EXECUTE  
 A sequência de escape ODBC CALL e a sequência de escape RPC são os métodos preferidos para chamar um procedimento armazenado, em vez do [EXECUTE](../../../t-sql/language-elements/execute-transact-sql.md) instrução. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client usa o mecanismo RPC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para otimizar o processamento do comando. Este protocolo de RPC aumenta o desempenho, eliminando grande parte do processamento de parâmetros e da análise da instrução feita no servidor.  
  
 Este é um exemplo de como o [!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE** instrução:  
  
```  
EXECUTE SalesByCategory 'Produce', '1995'  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
