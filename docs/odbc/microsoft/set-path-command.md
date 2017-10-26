---
title: Comando DEMARCADOR do conjunto | Microsoft Docs
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
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 490fefba9286a970b21014c66d681426703978fc
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="set-path-command"></a>Comando DEMARCADOR do conjunto
Especifica um caminho para pesquisas de arquivos. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>Argumentos  
 A [ *caminho*]  
 Especifica os diretórios que você deseja do Visual FoxPro para pesquisar. Use vírgulas ou ponto e vírgula para separar os diretórios.  
  
## <a name="remarks"></a>Comentários  
 Definir caminho permite que você especifique os caminhos de pesquisa para outros programas do Visual FoxPro que podem ser chamados dentro de procedimentos armazenados. DEFINIR o caminho não alterará o caminho da fonte de dados que você especificou para a conexão.  
  
 Emitir Definir caminho para sem *caminho* para restaurar o caminho para o diretório padrão ou pasta.  
  
## <a name="driver-remarks"></a>Comentários de driver  
 Se você emitir o caminho definido em um procedimento armazenado, ele será ignorado pelos comandos e funções a seguir:  
  
-   Funções de catálogo como [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) e [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ignorará o novo caminho e continuar a referência ao caminho especificado pela fonte de dados em [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) ou [ SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
-   Comandos como SELECT, INSERT, UPDATE, DELETE e CREATE TABLE ignorará o novo caminho e continuar a referência ao caminho especificado pela fonte de dados em **SQLPrepare** ou **SQLExecDirect**.  
  
 Se você emite o caminho definido em um procedimento armazenado e, posteriormente, não defina o caminho para seu estado original, outras conexões com o banco de dados usará o novo caminho (como definir o caminho não é delimitado para sessões de dados).  
  
 Se você deseja criar, selecionar ou atualizar tabelas em um diretório diferente do especificado pela fonte de dados, especifique o caminho completo do arquivo com o comando.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de configuração do ODBC do Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Driver ODBC do Visual FoxPro)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Driver ODBC do Visual FoxPro)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Driver ODBC do Visual FoxPro)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)

