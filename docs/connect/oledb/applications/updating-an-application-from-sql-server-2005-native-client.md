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
ms.openlocfilehash: 7915b9fb74f05057e05eef022d7f9b0e4ccdd21f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989253"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Atualizando um aplicativo no SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este tópico discute as alterações significativas no driver OLE DB para SQL Server desde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client no. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]  

 Ao atualizar do MDAC (Microsoft Data Access Components) para o OLE DB Driver for SQL Server, você também poderá observar algumas diferenças de comportamento. Para obter mais informações, consulte [atualizando um aplicativo para OLE DB driver para SQL Server do MDAC](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 fornecido com o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 fornecido com o [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 fornecido com o [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 fornecido com o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  

|Comportamento alterado no driver OLE DB para SQL Server em comparação [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] com o Native Client|Descrição|  
|------------------------------------------------------------------------------------|-----------------|  
|O OLE DB preenche apenas até a escala definida.|Para conversões em que os dados convertidos são enviados para o servidor, OLE DB driver para SQL Server painéis com zeros à direita nos dados até o comprimento máximo dos valores de **data e hora** . O SQL Server Native Client 9.0 e preenchia até nove dígitos.|  
|Valide DBTYPE_DBTIMESTAMP para ICommandWithParameter:: SetParameterInfo.|OLE DB driver para SQL Server implementa o requisito de OLE DB para *bScale* em ICommandWithParameter:: SetParameterInfo para ser definido como a precisão de segundos fracionários para DBTYPE_DBTIMESTAMP.|  
|O procedimento armazenado **sp_columns** agora retorna **"no"** em vez de **"no"** para a coluna IS_NULLABLE.|No driver OLE DB para SQL Server, o procedimento armazenado **sp_columns** agora retorna **"no"** em vez de **"no** " para uma coluna IS_NULLABLE.|  
|Erro diferente retornado quando a data está fora do intervalo.|Para o tipo **DateTime** , um número de erro diferente será retornado pelo driver OLE DB para SQL Server para uma data fora do intervalo que foi retornada em versões anteriores.<br /><br /> Especificamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client 9,0 retornou 22007 para todos os valores de ano fora do intervalo nas conversões de cadeia de caracteres em **DateTime**, e OLE DB driver para SQL Server retorna 22008 quando a data está dentro do intervalo suportado por **datetime2** , mas fora o intervalo com suporte de **DateTime** ou **smalldatetime**.|  
|O valor **datetime** trunca segundos fracionários e não será arredondado se o arredondamento alterar o dia.|Antes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, o comportamento do cliente para valores **datetime** enviados ao servidor era arredondá-los para o 1/300º de segundo mais próximo. No driver OLE DB para SQL Server, esse cenário causará um truncamento de segundos fracionários se o arredondamento for alterado no dia.|  
|Possível truncamento de segundos para o valor **DateTime** .|Um aplicativo compilado com o OLE DB Driver for SQL Server que se conecta a um servidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 truncará segundos e segundos fracionários na parte de hora dos dados enviados ao servidor se for feita uma associação de uma coluna datetime a um identificador de tipo DBTYPE_DBTIMESTAMP (OLE DB) ou SQL_TIMESTAMP (ODBC) e uma escala de 0.<br /><br /> Por exemplo:<br /><br /> Dados de entrada: 1994-08-21 21:21:36.000<br /><br /> Dados inseridos: 1994-08-21 21:21:00.000|  
|A conversão de dados OLE DB de DBTYPE_DBTIME em DBTYPE_DATE não faz mais com que o dia seja alterado.|Antes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, se a parte de hora de DBTYPE_DATE estivesse dentro de meio segundo de meia-noite, o código de conversão OLE DB fazia com que o dia fosse alterado. No driver OLE DB para SQL Server, o dia não será alterado (os segundos fracionários são truncados e não arredondados).|  
|Alterações de conversão IBCPSession:: BCColFmt.|No driver OLE DB para SQL Server, quando você usa IBCPSession:: BCOColFmt para converter SQLDATETIME ou SQLDATETIME em um tipo de cadeia de caracteres, um valor fracionário é exportado. Por exemplo, na conversão do tipo SQLDATETIME no tipo SQLNVARCHARMAX, as versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 retornavam<br /> 1989-02-01 00:00:00.<br />Retornos do OLE DB Driver for SQL Server <br />1989-02-01 00:00:00.0000000.|  
|Os aplicativos personalizados que usam a API BCP agora podem ver um aviso.|A API BCP gerará uma mensagem de aviso se o comprimento dos dados for maior do que o comprimento especificado para um campo para todos os tipos. Anteriormente, esse aviso era fornecido apenas para tipos de caracteres, mas não será emitido para todos os tipos.|  
|A inserção de uma cadeia de caracteres vazia em uma associação **sql_variant** como um tipo de data/hora gera um erro.|No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, a inserção de uma cadeia de caracteres vazia em uma associação **sql_variant** como um tipo de data/hora não gerava um erro. OLE DB driver para SQL Server gera um erro corretamente nessa situação.|  
|O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode retornar resultados diferentes quando um gatilho é executado.|As alterações introduzidas no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] podem fazer com que um aplicativo retorne resultados diferentes de uma instrução que causou a execução de um gatilho quando **NOCOUNT OFF** estava em vigor. Nessa situação, o aplicativo pode gerar um erro. Para resolver esse erro, defina **NOCOUNT ON** no gatilho.|  

## <a name="see-also"></a>Consulte Também   
 [Driver do OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server.md)
