---
title: Atualizando um aplicativo no SQL Server 2005 Native Client | Microsoft Docs
description: Atualizando um aplicativo no SQL Server 2005 Native Client
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 17280079f493d8abbad2f8ffb76d25c2a0ba868f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66771067"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Atualizando um aplicativo no SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este tópico discute as alterações significativas no Driver do OLE DB para SQL Server desde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

 Ao atualizar do MDAC (Microsoft Data Access Components) para o OLE DB Driver for SQL Server, você também poderá observar algumas diferenças de comportamento. Para obter mais informações, consulte [atualizando um aplicativo para o Driver do OLE DB para SQL Server no MDAC](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 fornecido com o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 fornecido com o [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 fornecido com o [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 fornecido com o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  

|Alterado o comportamento no Driver do OLE DB para SQL Server em comparação com [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client|Descrição|  
|------------------------------------------------------------------------------------|-----------------|  
|O OLE DB preenche apenas até a escala definida.|Para conversões onde os dados convertidos são enviados ao servidor, o Driver do OLE DB para SQL Server preenche zeros à direita nos dados apenas até o comprimento máximo de **datetime** valores. O SQL Server Native Client 9.0 e preenchia até nove dígitos.|  
|Valide DBTYPE_DBTIMESTAMP para ICommandWithParameter::SetParameterInfo.|Driver do OLE DB para SQL Server implementa o requisito OLE DB para *bScale* em ICommandWithParameter::SetParameterInfo a ser definido com precisão os segundos fracionários para DBTYPE_DBTIMESTAMP.|  
|O **sp_columns** procedimento armazenado agora retorna **"Não"** em vez de **"Não"** para a coluna IS_NULLABLE.|No Driver do OLE DB para SQL Server **sp_columns** procedimento armazenado agora retorna **"Não"** em vez de **"Não"** para uma coluna IS_NULLABLE.|  
|Erro diferente retornado quando a data está fora do intervalo.|Para o **datetime** tipo, um número de erro diferente será retornado pelo Driver do OLE DB para SQL Server para uma data fora do intervalo que era retornado em versões anteriores.<br /><br /> Especificamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 retornava 22007 para todos os valores de ano de intervalo em conversões de cadeia de caracteres para fora **datetime**, e o Driver do OLE DB para SQL Server retorna 22008 quando a data está dentro do intervalo aceito por **datetime2** , mas fora do intervalo aceito por **datetime** ou **smalldatetime**.|  
|O valor **datetime** trunca segundos fracionários e não será arredondado se o arredondamento alterar o dia.|Antes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, o comportamento do cliente para valores **datetime** enviados ao servidor era arredondá-los para o 1/300º de segundo mais próximo. No Driver do OLE DB para SQL Server, esse cenário provocará um truncamento de segundos fracionários se o arredondamento alterar o dia.|  
|Possível truncamento de segundos para **datetime** valor.|Um aplicativo compilado com o OLE DB Driver for SQL Server que se conecta a um servidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 truncará segundos e segundos fracionários na parte de hora dos dados enviados ao servidor se for feita uma associação de uma coluna datetime a um identificador de tipo DBTYPE_DBTIMESTAMP (OLE DB) ou SQL_TIMESTAMP (ODBC) e uma escala de 0.<br /><br /> Por exemplo:<br /><br /> Dados de entrada: 1994-08-21 21:21:36.000<br /><br /> Dados inseridos: 1994-08-21 21:21:00.000|  
|A conversão de dados OLE DB de DBTYPE_DBTIME em DBTYPE_DATE não faz mais com que o dia seja alterado.|Antes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, se a parte de hora de DBTYPE_DATE estivesse dentro de meio segundo de meia-noite, o código de conversão OLE DB fazia com que o dia fosse alterado. No Driver do OLE DB para SQL Server, o dia não será alterado (segundos fracionários são truncados e não arredondados).|  
|Alterações de conversão IBCPSession::BCColFmt.|No Driver do OLE DB para SQL Server, quando você usa IBCPSession::BCOColFmt para converter SQLDATETIME ou SQLDATETIME em um tipo de cadeia de caracteres, um valor fracionário será exportado. Por exemplo, na conversão do tipo SQLDATETIME no tipo SQLNVARCHARMAX, as versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 retornavam<br /> 1989-02-01 00:00:00.<br />Retornos do OLE DB Driver for SQL Server <br />1989-02-01 00:00:00.0000000.|  
|Os aplicativos personalizados que usam a API BCP agora podem ver um aviso.|A API BCP gerará uma mensagem de aviso se o comprimento dos dados for maior do que o comprimento especificado para um campo para todos os tipos. Anteriormente, esse aviso era fornecido apenas para tipos de caracteres, mas não será emitido para todos os tipos.|  
|A inserção de uma cadeia de caracteres vazia em uma associação **sql_variant** como um tipo de data/hora gera um erro.|No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, a inserção de uma cadeia de caracteres vazia em uma associação **sql_variant** como um tipo de data/hora não gerava um erro. Driver do OLE DB para SQL Server gera um erro corretamente nessa situação.|  
|O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode retornar resultados diferentes quando um gatilho é executado.|As alterações introduzidas no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] podem fazer com que um aplicativo retorne resultados diferentes de uma instrução que causou a execução de um gatilho quando **NOCOUNT OFF** estava em vigor. Nessa situação, o aplicativo pode gerar um erro. Para resolver esse erro, defina **NOCOUNT ON** no gatilho.|  

## <a name="see-also"></a>Consulte Também   
 [Driver do OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server.md)
