---
title: Problemas conhecidos do driver ODBC no Linux e macOS
description: Saiba mais sobre os problemas conhecidos com o Microsoft ODBC Driver for SQL Server em Linux e macOS, além das etapas para solucionar problemas de conectividade.
ms.date: 09/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1057252f896b62a5659b53aa53eb2f5c6d9b17ea
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288018"
---
# <a name="known-issues-for-the-odbc-driver-on-linux-and-macos"></a>Problemas conhecidos do driver ODBC no Linux e macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artigo contém uma lista de problemas conhecidos com o Microsoft ODBC 13, 13.1 e 17 para SQL Server em Linux e macOS. Ele também contém etapas para solucionar problemas de conectividade.

## <a name="known-issues"></a>Problemas conhecidos

Problemas adicionais serão postados no [blog de Drivers do SQL Server](https://techcommunity.microsoft.com/t5/SQL-Server/bg-p/SQLServer/label-name/SQLServerDrivers).  

- Devido às limitações da biblioteca do sistema, o Alpine Linux é compatível com menos codificações e localidades de caracteres. Por exemplo, en_US.UTF-8 não está disponível. Confira [musl libc – diferenças funcionais de glibc](https://wiki.musl-libc.org/functional-differences-from-glibc.html) para obter mais informações.

- Windows, Linux e macOS convertem caracteres da PUA (Área de Uso Particular) ou EUDC (Caracteres Definidos pelo Usuário Final ) de maneira diferente. Conversões executadas no servidor no [!INCLUDE[tsql](../../../includes/tsql-md.md)] usam a biblioteca de conversão do Windows. Conversões no driver usam as bibliotecas de conversão do Windows, do Linux ou do macOS. Cada biblioteca pode produzir resultados diferentes ao executar as conversões. Para obter mais informações, confira [End-User-Defined and Private Use Area Characters](/windows/desktop/Intl/end-user-defined-characters) (Caracteres de área de uso privado e definidos pelo usuário final).

- Se a codificação cliente for UTF-8, o gerenciador de driver nem sempre converterá corretamente de UTF-8 em UTF-16. Atualmente, dados corrompidos ocorrem quando um ou mais caracteres na cadeia de caracteres não são caracteres de UTF-8 válidos. Caracteres ASCII são mapeados corretamente. O gerenciador de driver tentará fazer essa conversão ao chamar as versões SQLCHAR da API do ODBC (por exemplo, SQLDriverConnectA). O gerenciador de driver não tentará fazer essa conversão ao chamar as versões SQLWCHAR da API do ODBC (por exemplo, SQLDriverConnectW).  

- O parâmetro *ColumnSize* do **SQLBindParameter** refere-se ao número de caracteres no tipo SQL, enquanto *BufferLength* é o número bytes no buffer do aplicativo. No entanto, se o tipo de dados SQL for `varchar(n)` ou `char(n)`, o aplicativo associar o parâmetro como SQL_C_CHAR ou SQL_C_VARCHAR e a codificação de caracteres do cliente for UTF-8, você poderá receber um erro do tipo "Dados da cadeia de caracteres, truncamento à direita" do driver, mesmo se o valor de *ColumnSize* estiver alinhado com o tamanho do tipo de dados no servidor. Esse erro ocorre porque as conversões entre codificações de caracteres podem mudar o comprimento dos dados. Por exemplo, um caractere de apóstrofo reto (U+2019) é codificado em CP-1252 como o byte único 0x92, mas, em UTF-8, como a sequência de 3 bytes 0xe2 0x80 0x99.

Por exemplo, se sua codificação for UTF-8 e você especificar 1 para *BufferLength* e para *ColumnSize* no **SQLBindParameter** para um parâmetro de saída e então tentar recuperar o caractere precedente armazenado em uma coluna `char(1)` no servidor (usando CP-1252), o driver tentará convertê-lo na codificação de 3 bytes UTF-8, mas não conseguirá colocar o resultado em um buffer de 1 byte. Na outra direção, ele compara *ColumnSize* com o *BufferLength* no **SQLBindParameter** antes de fazer a conversão entre as diferentes páginas de código no cliente e no servidor. Como um *ColumnSize* de valor 1 é menor que um *BufferLength* de valor 3 (por exemplo), o driver gerará um erro. Para evitar esse erro, verifique se o comprimento dos dados após a conversão se adapta à coluna ou ao buffer especificado. Observe que *ColumnSize* não pode ser maior que 8000 para o tipo `varchar(n)`.

## <a name="troubleshooting-connection-problems"></a><a id="connectivity"></a> Como solucionar problemas de conexão  

Se não for possível estabelecer uma conexão com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o driver ODBC, use as informações a seguir para identificar o problema.  
  
O problema de conexão mais comum é ter duas cópias do Gerenciador de Driver UnixODBC instaladas. Pesquise por libodbc\*.so\*em /usr. Se houver mais de uma versão do arquivo, você (possivelmente) tem mais de um gerenciador de driver instalado. Seu aplicativo pode usar a versão errada.
  
Habilite o log de conexão editando seu arquivo `/etc/odbcinst.ini` para conter a seção a seguir com estes itens:

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
Se você obtiver outra falha de conexão e não vir um arquivo de log, (possivelmente) há duas cópias do Gerenciador de Driver em seu computador. Caso contrário, a saída do log deve ser semelhante ao seguinte:  
  
```
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 17 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
Se a codificação de caracteres ASCII não for UTF-8, por exemplo: 
  
```
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
Há mais de um Gerenciador de Driver instalado e o seu aplicativo está usando o errado ou o Gerenciador de Driver não foi compilado corretamente.  
  
Para obter mais informações sobre como resolver falhas de conexão, consulte:  

- [Etapas para solucionar problemas de conectividade do SQL](https://docs.microsoft.com/archive/blogs/sql_protocols/steps-to-troubleshoot-sql-connectivity-issues)  
  
- [Solução de problema de conectividade do SQL Server 2005 – Parte I](https://techcommunity.microsoft.com/t5/sql-server/sql-server-2005-connectivity-issue-troubleshoot-part-i/ba-p/383034)  
  
- [Solução de problema de conectividade no SQL Server 2008 com o Buffer de Anéis de Conectividade](https://techcommunity.microsoft.com/t5/sql-server/connectivity-troubleshooting-in-sql-server-2008-with-the/ba-p/383393)  
  
- [Solução de problemas de autenticação do SQL Server](/archive/blogs/sqlsecurity/sql-server-authentication-troubleshooter)  

## <a name="next-steps"></a>Próximas etapas

Para obter instruções de instalação do driver ODBC, confira os seguintes artigos:

- [Como instalar o Microsoft ODBC Driver for SQL Server em Linux](installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Como instalar o Microsoft ODBC Driver for SQL Server no macOS](install-microsoft-odbc-driver-sql-server-macos.md)

Para obter mais informações, confira as [Diretrizes de programação](programming-guidelines.md) e as [Notas sobre a versão](release-notes-odbc-sql-server-linux-mac.md).  
