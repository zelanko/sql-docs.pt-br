---
title: Problemas conhecidos nesta versão do Driver para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25ebc4837eb37604a45e98112fa5fc24bdb3e69b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742994"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>Problemas conhecidos nesta versão do driver

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artigo contém uma lista de problemas conhecidos com o Microsoft ODBC Driver 13, 13.1 e 17 for SQL Server no Linux e macOS.

Problemas adicionais serão postados no [blog da equipe do driver ODBC da Microsoft](http://blogs.msdn.com/b/sqlnativeclient/).  

- Windows, Linux e macOS convertem caracteres da PUA (Área de Uso Particular) ou EUDC (Caracteres Definidos pelo Usuário Final ) de maneira diferente. Conversões executadas no servidor no [!INCLUDE[tsql](../../../includes/tsql-md.md)] usam a biblioteca de conversão do Windows. Conversões no driver usam as bibliotecas de conversão do Windows, Linux ou macOS. Cada biblioteca pode produzir resultados diferentes ao executar as conversões. Para obter mais informações, consulte [End-User-Defined and Private Use Area Characters](/windows/desktop/Intl/end-user-defined-characters).

- Se o cliente a codificação UTF-8, o Gerenciador de driver não corretamente sempre converter de UTF-8 em UTF-16. Atualmente, a corrupção de dados ocorre quando um ou mais caracteres na cadeia de caracteres não são caracteres de UTF-8 válidos. Caracteres ASCII são mapeados corretamente. O gerenciador de driver tentará fazer essa conversão ao chamar as versões SQLCHAR da API do ODBC (por exemplo, SQLDriverConnectA). O gerenciador de driver não tentará fazer essa conversão ao chamar as versões SQLWCHAR da API do ODBC (por exemplo, SQLDriverConnectW).  

- O *ColumnSize* parâmetro do **SQLBindParameter** refere-se ao número de caracteres no tipo de SQL, enquanto *BufferLength* é o número de bytes na caixa de diálogo buffer. No entanto, se o tipo de dados SQL for `varchar(n)` ou `char(n)`, o aplicativo associar o parâmetro como SQL_C_CHAR ou SQL_C_VARCHAR e a codificação de caracteres do cliente for UTF-8, você poderá receber um erro do tipo "Dados da cadeia de caracteres, truncamento à direita" do driver, mesmo se o valor de *ColumnSize* estiver alinhado com o tamanho do tipo de dados no servidor. Esse erro ocorre, pois as conversões entre codificações de caracteres podem mudar o comprimento dos dados. Por exemplo, um apóstrofo reto caractere (U + 2019) é codificado em CP-1252 como 0x92 de byte único, mas em UTF-8 como a sequência de 3 bytes 0xe2 0x80 0x99.

Por exemplo, se sua codificação é UTF-8 e você especificar 1 para ambos *BufferLength* e *ColumnSize* na **SQLBindParameter** para um parâmetro de saída e, em seguida, tentar recuperar o caractere precedente armazenado em um `char(1)` coluna no servidor (usando CP-1252), o driver tenta convertê-lo para a codificação de 3 bytes UTF-8, mas não é possível ajustar o resultado em um buffer de 1 byte. Na outra direção, ele compara *ColumnSize* com o *BufferLength* no **SQLBindParameter** antes de fazer a conversão entre as páginas de código diferentes sobre o cliente e servidor. Como um *ColumnSize* de valor 1 é menor que um *BufferLength* de valor 3 (por exemplo), o driver gerará um erro. Para evitar esse erro, verifique se o comprimento dos dados após a conversão se adapta a coluna ou o buffer especificado. Observe que *ColumnSize* não pode ser maior que 8000 para o `varchar(n)` tipo.

## <a name="see-also"></a>Consulte Também  
[Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[Notas de versão](../../../connect/odbc/linux-mac/release-notes.md)  

