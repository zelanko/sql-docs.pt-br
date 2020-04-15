---
title: Adicionar uma Fonte de Dados (ODBC) | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55ae4f357aa850f6b3ff4ba9cca0b59a2ccbc570
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298308"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>Configurar o Driver ODBC do SQL Server – Adicionar uma fonte de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Antes de usar os aplicativos ODBC com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior, você deve saber como atualizar a versão dos procedimentos armazenados de catálogo em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e adicionar, excluir e testar as fontes de dados.  
  
  Você pode adicionar uma fonte de dados usando o Administrador ODBC, programáticamente (usando [SQLConfigDataSource),](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)ou criando um arquivo.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Para adicionar uma fonte de dados usando o Administrador ODBC  
  
1.  A partir do **Painel de Controle,** acesse **Ferramentas Administrativas** e, em seguida, **as fontes de dados oDBC (64 bits)** ou **as fontes de dados da ODBC (32 bits)**. Como alternativa, você pode invocar odbcad32.exe.  
  
2.  Clique na guia **DSN**do **usuário, DSN do sistema**ou **arquivo DSN** e clique em **Adicionar**.  
  
3.  Clique em **SQL Server**e clique **em Concluir**.  
  
4.  Complete as etapas no **Criar uma nova fonte de dados para o Assistente do Servidor SQL.**  
  
### <a name="to-add-a-data-source-programmatically"></a>Para adicionar uma fonte de dados via programação  
  
1.  Ligue para [sqlconfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) com o segundo parâmetro definido para ODBC_ADD_DSN ou ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Para adicionar uma fonte de dados de arquivo  
  
1.  Ligue para [o SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) com um parâmetro SAVEFILE=file_name na seqüência de conexão. Se a conexão for bem-sucedida, o driver ODBC criará uma fonte de dados de arquivo com os parâmetros de conexão no local apontado pelo parâmetro SAVEFILE.  
  
## <a name="see-also"></a>Consulte Também  
[Exclua uma fonte de dados &#40;o&#41;Da Fonte ODBC](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
