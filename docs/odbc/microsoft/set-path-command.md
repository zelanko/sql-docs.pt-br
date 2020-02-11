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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063644"
---
# <a name="set-path-command"></a>Comando SET PATH
Especifica um caminho para pesquisas de arquivo. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>Argumentos  
 PARA [ *caminho*]  
 Especifica os diretórios que você deseja que o Visual FoxPro pesquise. Use vírgulas ou ponto e vírgula para separar os diretórios.  
  
## <a name="remarks"></a>Comentários  
 SET PATH permite especificar caminhos de pesquisa para outros programas do Visual FoxPro que podem ser chamados em procedimentos armazenados. SET PATH não alterará o caminho da fonte de dados que você especificou para a conexão.  
  
 Problema defina o caminho para sem *caminho* para restaurar o caminho para o diretório ou pasta padrão.  
  
## <a name="driver-remarks"></a>Comentários do driver  
 Se você emitir o caminho definido em um procedimento armazenado, ele será ignorado pelas seguintes funções e comandos:  
  
-   As funções de catálogo, como [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) e [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) , ignorarão o novo caminho e continuarão referenciando o caminho especificado pela fonte de dados em [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) ou [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
-   Comandos como selecionar, inserir, atualizar, excluir e CREATE TABLE ignorarão o novo caminho e continuarão referenciando o caminho especificado pela fonte de dados em **SQLPrepare** ou **SQLExecDirect**.  
  
 Se você emitir o caminho definido em um procedimento armazenado e não, subsequentemente, definir o caminho de volta para seu estado original, outras conexões com o banco de dados usarão o novo caminho (porque SET PATH não tem o escopo de sessões de data).  
  
 Se você quiser criar, selecionar ou atualizar tabelas em um diretório diferente daquele especificado pela fonte de dados, especifique o caminho completo do arquivo com o comando.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo configuração do ODBC do Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (driver ODBC do Visual FoxPro)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (driver ODBC do Visual FoxPro)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Driver ODBC do Visual FoxPro)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
