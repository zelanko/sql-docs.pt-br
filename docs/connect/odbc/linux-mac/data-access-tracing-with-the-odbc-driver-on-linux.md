---
title: Rastreamento de acesso a dados com o Driver ODBC no Linux e macOS | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ae175bfa033ba445d9a8235706a2f6fe55690ac
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Rastreamento de acesso a dados com o Driver ODBC no Linux e macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O Gerenciador de Driver unixODBC no macOS e no Linux oferece suporte a rastreamento de entrada de chamada de API de ODBC e sair do Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].

Para rastrear o comportamento do aplicativo ODBC, edite o `odbcinst.ini` do arquivo `[ODBC]` seção para definir os valores `Trace=Yes` e `TraceFile` para o caminho do arquivo que contém o rastreamento de saída; por exemplo:

```  
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```  

(Você também pode usar `/dev/stdout` ou qualquer outro nome de dispositivo para enviar o rastreamento de saída existe em vez de em um arquivo persistente.) Com as configurações acima, sempre que um aplicativo carrega o Gerenciador de Driver unixODBC ele registrará todas as chamadas de API de ODBC que ela executada no arquivo de saída.

Depois de concluir o rastreamento de seu aplicativo, remova `Trace=Yes` do `odbcinst.ini` para evitar a degradação de desempenho de rastreamento e verifique se todos os arquivos desnecessários do rastreamento são removidos.
  
O rastreamento se aplica a todos os aplicativos que usam o driver em `odbcinst.ini`. Para não rastrear todos os aplicativos (por exemplo, para evitar a divulgação de informações confidenciais por usuário), você pode rastrear uma instância de aplicativo individual, fornecendo o local de um particular `odbcinst.ini`, usando o `ODBCSYSINI` variável de ambiente. Por exemplo:  
  
```  
$ ODBCSYSINI=/home/myappuser myapp
```  
  
Nesse caso, você pode adicionar `Trace=Yes` para o `[ODBC Driver 13 for SQL Server]` seção `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Determinando qual arquivo odbc.ini o Driver está usando

Os drivers ODBC do Linux e macOS não sabe qual `odbc.ini` está em uso ou o caminho para o `odbc.ini` arquivo. No entanto, obter informações sobre quais `odbc.ini` arquivo está em uso está disponível a partir de ferramentas unixODBC `odbc_config` e `odbcinst`e a documentação do Gerenciador de Driver unixODBC.  
  
Por exemplo, o comando a seguir imprime (entre outras informações) o local do sistema e usuário `odbc.ini` arquivos que contêm, respectivamente, os DSNs de sistema e usuário:

```
$ odbcinst -j
unixODBC 2.3.1
DRIVERS............: /etc/odbcinst.ini
SYSTEM DATA SOURCES: /etc/odbc.ini
FILE DATA SOURCES..: /etc/ODBCDataSources
USER DATA SOURCES..: /home/odbcuser/.odbc.ini`
SQLULEN Size.......: 8
SQLLEN Size........: 8
SQLSETPOSIROW Size.: 8
```

O [documentação do unixODBC](http://www.unixodbc.org/doc/UserManual/) explica as diferenças entre o usuário e DSNs do sistema. Em Resumo:  

- DSNs do usuário---esses são os DSNs que só estão disponíveis para um usuário específico. Os usuários podem se conectar usando, adicionar, modificar e remover seus próprios DSNs do usuário. DSNs do usuário são armazenados em um arquivo no diretório base do usuário ou um subdiretório dele.
  
- DSNs do sistema---esses DSNs estão disponíveis para cada usuário do sistema conectar-se usá-los, mas podem apenas ser adicionados, modificados e removidos por um administrador de sistema. Se um usuário tiver um DSN de usuário com o mesmo nome como um DSN de sistema, o DSN do usuário será usado em conexões por esse usuário.

## <a name="see-also"></a>Consulte também
[Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)

