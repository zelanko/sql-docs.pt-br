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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e44093c3ea18bc995264a8974726f5af0abe3b3a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300816"
---
# <a name="set-path-command"></a>Comando SET PATH
Especifica um caminho para pesquisas de arquivos. Para obter informações específicas do motorista, consulte as observações.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>Argumentos  
 PARA [ *Caminho*]  
 Especifica os diretórios que você deseja que o Visual FoxPro pesquise. Use vírgulas ou ponto e vírgula para separar os diretórios.  
  
## <a name="remarks"></a>Comentários  
 SET PATH permite especificar caminhos de pesquisa para outros programas Visual FoxPro que podem ser chamados dentro de procedimentos armazenados. SET PATH não mudará o caminho da fonte de dados especificada para a conexão.  
  
 ''DEFINIR CAMINHO DE DESERDASSo sem *Caminho'* para restaurar o caminho para o diretório ou pasta padrão.  
  
## <a name="driver-remarks"></a>Observações do motorista  
 Se você emitir SET PATH em um procedimento armazenado, ele será ignorado pelas seguintes funções e comandos:  
  
-   Funções de catálogo como [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md) e [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ignorarão o novo caminho e continuarão a referenciar o caminho especificado pela fonte de dados no [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md) ou [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
-   Comandos como SELECT, INSERT, UPDATE, DELETE e CREATE TABLE ignorarão o novo caminho e continuarão a referenciar o caminho especificado pela fonte de dados no **SQLPrepare** ou **No SQLExecDirect**.  
  
 Se você emitir SET PATH em um procedimento armazenado e não definir posteriormente o caminho de volta ao seu estado original, outras conexões ao banco de dados usarão o novo caminho (porque set PATH não está escopo para sessões de dados).  
  
 Se você quiser criar, selecionar ou atualizar tabelas em um diretório diferente do especificado pela fonte de dados, especifique o caminho completo do arquivo com o seu comando.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo de configuração Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [Colunas SQL (Driver Visual FoxPro ODBC)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (driver Visual FoxPro ODBC)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Driver ODBC do Visual FoxPro)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
