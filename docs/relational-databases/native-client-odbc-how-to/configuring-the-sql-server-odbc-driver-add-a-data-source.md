---
title: Adicionar uma fonte de dados (ODBC) | Microsoft Docs
description: Saiba como SQL Server driver ODBC chama procedimentos armazenados como procedimentos armazenados remotos no SQL Server usando o mecanismo de chamada de procedimento armazenado remoto.
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: da691dab0513ccd472459e2ad6ecaa4c446b9828
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467767"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>Configurar o Driver ODBC do SQL Server – Adicionar uma fonte de dados
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Antes de usar os aplicativos ODBC com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior, você deve saber como atualizar a versão dos procedimentos armazenados de catálogo em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e adicionar, excluir e testar as fontes de dados.  
  
  Você pode adicionar uma fonte de dados usando o Administrador ODBC, programaticamente (usando [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)) ou criando um arquivo.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Para adicionar uma fonte de dados usando o Administrador ODBC  
  
1.  No **painel de controle**, acesse **Ferramentas administrativas** e, em seguida, **fontes de dados ODBC (64 bits)** ou **fontes de dados ODBC (32 bits)**. Como alternativa, você pode invocar odbcad32.exe.  
  
2.  Clique na **guia DSN do usuário**, DSN do **sistema** ou **DSN de arquivo** e, em seguida, clique em **Adicionar**.  
  
3.  Clique em **SQL Server** e em **concluir**.  
  
4.  Conclua as etapas no assistente **para criar uma nova fonte de dados para SQL Server** .  
  
### <a name="to-add-a-data-source-programmatically"></a>Para adicionar uma fonte de dados via programação  
  
1.  Chame [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) com o segundo parâmetro definido como ODBC_ADD_DSN ou ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Para adicionar uma fonte de dados de arquivo  
  
1.  Chame [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) com um parâmetro SAVEFILE = file_name na cadeia de conexão. Se a conexão for bem-sucedida, o driver ODBC criará uma fonte de dados de arquivo com os parâmetros de conexão no local apontado pelo parâmetro SAVEFILE.  
  
## <a name="see-also"></a>Consulte Também  
[Excluir uma fonte de dados &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
