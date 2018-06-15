---
title: Atualizando um aplicativo do SQL Server 2005 Native Client | Microsoft Docs
description: Atualizando um aplicativo do SQL Server 2005 Native Client
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 60a03e3ec34c29821a6b29d3174b11c5376511e6
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612061"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Atualizando um aplicativo no SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este tópico discute as últimas alterações no Driver do OLE DB para SQL Server desde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

 Quando você atualiza do Microsoft Data Access Components (MDAC) para o Driver do OLE DB para SQL Server, você também poderá ver algumas diferenças de comportamento. Para obter mais informações, consulte [atualizando um aplicativo para o Driver do OLE DB para SQL Server do MDAC](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 acompanha [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 acompanha [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 fornecido com o [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 fornecido com o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  

|Alterado o comportamento no Driver do OLE DB para SQL Server em comparação com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|O OLE DB preenche apenas até a escala definida.|Para conversões onde os dados convertidos são enviados ao servidor, o OLE DB Driver para SQL Server preenche zeros à direita nos dados apenas até o comprimento máximo de **datetime** valores. O SQL Server Native Client 9.0 e preenchia até nove dígitos.|  
|Valide DBTYPE_DBTIMESTAMP para ICommandWithParameter::SetParameterInfo.|OLE DB Driver para SQL Server implementa o requisito OLE DB de *bScale* em ICommandWithParameter::SetParameterInfo a ser definido com precisão os segundos fracionários para DBTYPE_DBTIMESTAMP.|  
|O **sp_columns** procedimento armazenado agora retorna **"Não"** em vez de **"Não"** para a coluna IS_NULLABLE.|No OLE DB Driver para SQL Server, **sp_columns** procedimento armazenado agora retorna **"Não"** em vez de **"Não"** para uma coluna IS_NULLABLE.|  
|Erro diferente retornado quando a data está fora do intervalo.|Para o **datetime** tipo, um número de erro diferente será retornado pelo Driver do OLE DB para SQL Server para uma data fora do intervalo que foi retornado em versões anteriores.<br /><br /> Especificamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 retornava 22007 para todos os valores de ano de intervalo em conversões de cadeia de caracteres para fora **datetime**, e o OLE DB Driver para SQL Server retorna 22008 quando a data está dentro do intervalo aceito por **datetime2** , mas fora do intervalo aceito por **datetime** ou **smalldatetime**.|  
|**DateTime** valor trunca segundos fracionários e não redondo se o arredondamento alterar o dia.|Antes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, o comportamento do cliente para **datetime** valores enviados ao servidor era arredondá-los mais próximo 1/300 de segundo. No OLE DB Driver para SQL Server, esse cenário provocará um truncamento de frações de segundo se o arredondamento alterar o dia.|  
|Trunction possíveis de segundos para **datetime** valor.|Um aplicativo compilado com o Driver do OLE DB para SQL Server que se conecta a um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] server 2005 truncará segundos e segundos fracionários na parte de hora dos dados enviados para o servidor se vincular a uma coluna de data e hora com um identificador de tipo de DBTYPE_DBTIMESTAMP ( OLE DB) ou SQL_TIMESTAMP (ODBC) e uma escala de 0.<br /><br /> Por exemplo:<br /><br /> Dados de entrada: 1994-08-21 21:21:36.000<br /><br /> Dados inseridos: 1994-08-21 21:21:00.000|  
|A conversão de dados OLE DB de DBTYPE_DBTIME em DBTYPE_DATE não faz mais com que o dia seja alterado.|Antes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, se a parte de hora de DBTYPE_DATE estivesse dentro de meio segundo de meia-noite, o código de conversão OLE DB fazia com que o dia fosse alterado. No OLE DB Driver para SQL Server, o dia não será alterado (segundos fracionários são truncados e não são arredondados).|  
|Alterações de conversão de IBCPSession::BCColFmt.|No OLE DB Driver para SQL Server, quando você usar IBCPSession::BCOColFmt para converter SQLDATETIME ou SQLDATETIME em um tipo de cadeia de caracteres, um valor fracionário será exportado. Por exemplo, na conversão do tipo SQLDATETIME no tipo SQLNVARCHARMAX, versões anteriores ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 retornado<br /> 1989-02-01 00:00:00.<br />Retorna de OLE DB Driver para SQL Server <br />1989-02-01 00:00:00.0000000.|  
|Os aplicativos personalizados que usam a API BCP agora podem ver um aviso.|A API BCP gerará uma mensagem de aviso se o comprimento dos dados for maior do que o comprimento especificado para um campo para todos os tipos. Anteriormente, esse aviso era fornecido apenas para tipos de caracteres, mas não será emitido para todos os tipos.|  
|Inserir uma cadeia de caracteres vazia em uma **sql_variant** associado como um tipo de data/hora gera um erro.|Em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, inserindo uma cadeia de caracteres vazia em uma **sql_variant** associado como um tipo de data/hora não gerava um erro. OLE DB Driver para SQL Server gera um erro corretamente nessa situação.|  
|O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode retornar resultados diferentes quando um gatilho é executado.|Alterações introduzidas no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] pode fazer com que um aplicativo retorne diferentes resultados de uma instrução que causou um gatilho a ser executada quando **NOCOUNT OFF** estava em vigor. Nessa situação, o aplicativo pode gerar um erro. Para resolver esse erro, defina **NOCOUNT ON** no gatilho.|  

## <a name="see-also"></a>Consulte também   
 [Driver do OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server.md)
