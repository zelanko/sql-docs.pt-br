---
title: Problemas conhecidos nesta Versão do Driver para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3508277502ad7e3eb3b0e7ff048301c8ed1efdd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008785"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>Problemas conhecidos nesta versão do driver

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artigo contém uma lista de problemas conhecidos com o Microsoft ODBC 13, 13.1 e 17 para SQL Server em Linux e macOS.

Problemas adicionais serão postados no [blog da equipe do driver ODBC da Microsoft](https://blogs.msdn.com/b/sqlnativeclient/).  

- Windows, Linux e macOS convertem caracteres da PUA (Área de Uso Particular) ou EUDC (Caracteres Definidos pelo Usuário Final ) de maneira diferente. Conversões executadas no servidor no [!INCLUDE[tsql](../../../includes/tsql-md.md)] usam a biblioteca de conversão do Windows. Conversões no driver usam as bibliotecas de conversão do Windows, do Linux ou do macOS. Cada biblioteca pode produzir resultados diferentes ao executar as conversões. Para obter mais informações, confira [End-User-Defined and Private Use Area Characters](/windows/desktop/Intl/end-user-defined-characters) (Caracteres de área de uso privado e definidos pelo usuário final).

- Se a codificação cliente for UTF-8, o gerenciador de driver nem sempre converterá corretamente de UTF-8 em UTF-16. Atualmente, dados corrompidos ocorrem quando um ou mais caracteres na cadeia de caracteres não são caracteres de UTF-8 válidos. Caracteres ASCII são mapeados corretamente. O gerenciador de driver tentará fazer essa conversão ao chamar as versões SQLCHAR da API do ODBC (por exemplo, SQLDriverConnectA). O gerenciador de driver não tentará fazer essa conversão ao chamar as versões SQLWCHAR da API do ODBC (por exemplo, SQLDriverConnectW).  

- O parâmetro *ColumnSize* do **SQLBindParameter** refere-se ao número de caracteres no tipo SQL, enquanto *BufferLength* é o número bytes no buffer do aplicativo. No entanto, se o tipo de dados SQL for `varchar(n)` ou `char(n)`, o aplicativo associar o parâmetro como SQL_C_CHAR ou SQL_C_VARCHAR e a codificação de caracteres do cliente for UTF-8, você poderá receber um erro do tipo "Dados da cadeia de caracteres, truncamento à direita" do driver, mesmo se o valor de *ColumnSize* estiver alinhado com o tamanho do tipo de dados no servidor. Esse erro ocorre porque as conversões entre codificações de caracteres podem mudar o comprimento dos dados. Por exemplo, um caractere de apóstrofo reto (U+2019) é codificado em CP-1252 como o byte único 0x92, mas, em UTF-8, como a sequência de 3 bytes 0xe2 0x80 0x99.

Por exemplo, se sua codificação for UTF-8 e você especificar 1 para *BufferLength* e para *ColumnSize* no **SQLBindParameter** para um parâmetro de saída e então tentar recuperar o caractere precedente armazenado em uma coluna `char(1)` no servidor (usando CP-1252), o driver tentará convertê-lo na codificação de 3 bytes UTF-8, mas não conseguirá colocar o resultado em um buffer de 1 byte. Na outra direção, ele compara *ColumnSize* com o *BufferLength* no **SQLBindParameter** antes de fazer a conversão entre as diferentes páginas de código no cliente e no servidor. Como um *ColumnSize* de valor 1 é menor que um *BufferLength* de valor 3 (por exemplo), o driver gerará um erro. Para evitar esse erro, verifique se o comprimento dos dados após a conversão se adapta à coluna ou ao buffer especificado. Observe que *ColumnSize* não pode ser maior que 8000 para o tipo `varchar(n)`.

## <a name="see-also"></a>Consulte Também  
[Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[Notas de versão](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  

