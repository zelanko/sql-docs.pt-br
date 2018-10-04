---
title: Adicionar uma fonte de dados (ODBC) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 21ba3a1507588e0110bbcf281f2cbbe9f41742a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787934"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>Configurar o Driver ODBC do SQL Server – Adicionar uma fonte de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Antes de usar os aplicativos ODBC com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior, você deve saber como atualizar a versão dos procedimentos armazenados de catálogo em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e adicionar, excluir e testar as fontes de dados.  
  
  Você pode adicionar uma fonte de dados usando o administrador de ODBC, programaticamente (usando [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)), ou criando um arquivo.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Para adicionar uma fonte de dados usando o Administrador ODBC  
  
1.  Dos **painel de controle**, acesso **ferramentas administrativas** e, em seguida, **fontes de dados ODBC (64 bits)** ou **fontes de dados ODBC (32 bits)**. Como alternativa, você pode invocar odbcad32.exe.  
  
2.  Clique o **DSN de usuário**, **DSN de sistema**, ou **DSN de arquivo** guia e, em seguida, clique em **adicionar**.  
  
3.  Clique em **SQL Server**e, em seguida, clique em **concluir**.  
  
4.  Conclua as etapas a **criar uma nova fonte de dados para o SQL Server** assistente.  
  
### <a name="to-add-a-data-source-programmatically"></a>Para adicionar uma fonte de dados via programação  
  
1.  Chame [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) com o segundo parâmetro definido como ODBC_ADD_DSN ou ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Para adicionar uma fonte de dados de arquivo  
  
1.  Chame [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) com um SAVEFILE = file_name parâmetro na cadeia de conexão. Se a conexão for bem-sucedida, o driver ODBC criará uma fonte de dados de arquivo com os parâmetros de conexão no local apontado pelo parâmetro SAVEFILE.  
  
## <a name="see-also"></a>Consulte também  
[Excluir uma fonte de dados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
