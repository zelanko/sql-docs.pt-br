---
title: Adicionar uma fonte de dados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 822ac0f5d2e228a982368849ed1c409ef63765ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117879"
---
# <a name="add-a-data-source-odbc"></a>Adicionar uma fonte de dados (ODBC)
  Você pode adicionar uma fonte de dados usando o administrador de ODBC, programaticamente (usando [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)), ou criando um arquivo.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Para adicionar uma fonte de dados usando o Administrador ODBC  
  
1.  Do **painel de controle**, acesso **ferramentas administrativas** e **fontes de dados (ODBC)**. Como alternativa, você pode invocar odbcad32.exe.  
  
2.  Clique o **DSN do usuário**, **DSN de sistema**, ou **DSN de arquivo** guia e, em seguida, clique em **adicionar**.  
  
3.  Clique em **do SQL Server**e, em seguida, clique em **concluir**.  
  
4.  Conclua as etapas no Assistente para Criação de Nova Fonte de Dados no SQL Server.  
  
### <a name="to-add-a-data-source-programmatically"></a>Para adicionar uma fonte de dados via programação  
  
1.  Chamar [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md) com o segundo parâmetro definido como ODBC_ADD_DSN ou ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Para adicionar uma fonte de dados de arquivo  
  
1.  Chamar [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) com um SAVEFILE = file_name parâmetro na cadeia de conexão. Se a conexão for bem-sucedida, o driver ODBC criará uma fonte de dados de arquivo com os parâmetros de conexão no local apontado pelo parâmetro SAVEFILE.  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos de instrução sobre a configuração do driver ODBC do SQL Server](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  