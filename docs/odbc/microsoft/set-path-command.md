---
title: Comando SET PATH | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57685731bc5eb86381816d0cbb91a4942b5bfeff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063644"
---
# <a name="set-path-command"></a>Comando SET PATH
Especifica um caminho para pesquisas de arquivo. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>Argumentos  
 A [ *caminho*]  
 Especifica os diretórios que você deseja que o Visual FoxPro para pesquisar. Use vírgulas ou ponto e vírgula para separar os diretórios.  
  
## <a name="remarks"></a>Comentários  
 Definir caminho permite que você especifique caminhos de pesquisa para outros programas do Visual FoxPro que podem ser chamados dentro de procedimentos armazenados. Defina o caminho não será alterado para o caminho da fonte de dados que você especificou para a conexão.  
  
 Emitir Definir caminho para sem *caminho* para restaurar o caminho para o diretório ou pasta padrão.  
  
## <a name="driver-remarks"></a>Comentários de driver  
 Se você emitir o caminho definido em um procedimento armazenado, ele será ignorado pelos comandos e funções a seguir:  
  
-   Funções de catálogo, como [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) e [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ignorará o novo caminho e continuar referenciar o caminho especificado pela fonte de dados no [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) ou [ SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
-   Ignorará o novo caminho e continuar referenciar o caminho especificado pela fonte de dados em comandos como SELECT, INSERT, UPDATE, DELETE e CREATE TABLE **SQLPrepare** ou **SQLExecDirect**.  
  
 Se você emite o caminho definido em um procedimento armazenado e, posteriormente, não defina o caminho para seu estado original, outras conexões com o banco de dados usará o novo caminho (porque o caminho definido não é vinculado a sessões de dados).  
  
 Se você quiser criar, selecionar ou atualizar tabelas em um diretório diferente daquele especificado pela fonte de dados, especifique o caminho completo do arquivo com o comando.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de instalação do ODBC do Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Driver ODBC do Visual FoxPro)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Driver ODBC do Visual FoxPro)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Driver ODBC do Visual FoxPro)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
