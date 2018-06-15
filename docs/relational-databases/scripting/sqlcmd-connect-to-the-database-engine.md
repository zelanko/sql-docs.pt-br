---
title: Conectar-se ao Mecanismo de Banco de Dados com sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd utility, Database Engine connections
- Named Pipes [SQL Server], sqlcmd utility
- TCP/IP [SQL Server], client protocols
- network protocols [SQL Server], sqlcmd utility
- protocols [SQL Server], sqlcmd utility
- VIA
- client protocols [SQL Server]
ms.assetid: 74b0fb71-7f8e-4171-9431-d07528532524
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8bfba438ec6160b5431dfdd133c37eb4bcd85d7e
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34333707"
---
# <a name="sqlcmd---connect-to-the-database-engine"></a>sqlcmd – Conectar ao Mecanismo de Banco de Dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à comunicação de cliente com o protocolo de rede TCP/IP (padrão) e o protocolo de pipes nomeados. O protocolo de memória compartilhada também estará disponível se o cliente estiver se conectando a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no mesmo computador. Há três métodos comuns de selecionar o protocolo. O protocolo usado pelo utilitário **sqlcmd** é determinado na seguinte ordem:  
  
-   O**sqlcmd** usa o protocolo especificado como parte da cadeia de conexão, conforme a descrição abaixo.  
  
-   Se nenhum protocolo for especificado como parte da cadeia de conexão, o **sqlcmd** usará o protocolo definido como parte do alias ao qual ele está se conectando. Para configurar **sqlcmd** para usar um protocolo de rede específico criando um alias, veja [Criar ou excluir um alias de servidor para ser usado por um cliente &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
-   Se o protocolo não for especificado de outra forma, o **sqlcmd** usará o protocolo de rede determinado pela ordem de protocolos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
 Os exemplos a seguir mostram várias formas de fazer a conexão com a instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] na porta 1433, presumindo-se que as instâncias nomeadas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] estejam escutando na porta 1691. Alguns dos exemplos usam o endereço IP do adaptador de loopback (127.0.0.1). Experimente usar o endereço IP da placa de interface de rede de seu computador.  
  
 Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] especificando o nome da instância:  
  
```  
sqlcmd -S ComputerA  
sqlcmd -S ComputerA\instanceB  
```  
  
 Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] especificando o endereço IP:  
  
```  
sqlcmd -S 127.0.0.1  
sqlcmd -S 127.0.0.1\instanceB  
```  
  
 Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] especificando o número da porta de TCP\IP:  
  
```  
sqlcmd -S ComputerA,1433  
sqlcmd -S ComputerA,1691  
sqlcmd -S 127.0.0.1,1433  
sqlcmd -S 127.0.0.1,1691  
```  
  
### <a name="to-connect-using-tcpip"></a>Para fazer a conexão usando TCP/IP  
  
-   Conecte-se usando a seguinte sintaxe geral:  
  
    ```  
    sqlcmd -S tcp:<computer name>,<port number>  
    ```  
  
-   Conecte-se à instância padrão:  
  
    ```  
    sqlcmd -S tcp:ComputerA,1433  
    sqlcmd -S tcp:127.0.0.1,1433  
    ```  
  
-   Conecte-se a uma instância nomeada:  
  
    ```  
    sqlcmd -S tcp:ComputerA,1691  
    sqlcmd -S tcp:127.0.0.1,1691  
    ```  
  
### <a name="to-connect-using-named-pipes"></a>Para fazer a conexão usando pipes nomeados  
  
-   Conecte-se usando uma das seguintes sintaxes gerais:  
  
    ```  
    sqlcmd -S np:\\<computer name>\<pipe name>  
    ```  
  
-   Conecte-se à instância padrão:  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\sql\query  
    ```  
  
-   Conecte-se a uma instância nomeada:  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\MSSQL$<instancename>\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\MSSQL$<instancename>\sql\query  
    ```  
  
### <a name="to-connect-using-shared-memory-a-local-procedure-call-from-a-client-on-the-server"></a>Para fazer a conexão usando memória compartilhada (uma chamada de procedimento local) a partir de um cliente no servidor  
  
-   Conecte-se usando uma das seguintes sintaxes gerais:  
  
    ```  
    sqlcmd -S lpc:<computer name>  
    ```  
  
-   Conecte-se à instância padrão:  
  
    ```  
    sqlcmd -S lpc:ComputerA  
    ```  
  
-   Conecte-se a uma instância nomeada:  
  
    ```  
    sqlcmd -S lpc:ComputerA\<instancename>  
    ```  
  
  
