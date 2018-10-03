---
title: Atualizando um aplicativo no SQL Server 2005 Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2d4eda4a677cc371ea2c15114809b3272ffe24a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640184"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>Atualizando um aplicativo no SQL Server 2005 Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Este tópico aborda as últimas alterações no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client desde o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Ao atualizar do MDAC (Microsoft Data Access Components) para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, você também poderá observar algumas diferenças de comportamento. Para obter mais informações, consulte [atualizando um aplicativo para o SQL Server Native Client do MDAC](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 fornecido com o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 fornecido com o [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 fornecido com o [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 fornecido com o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)].  
  
|Comportamento alterado no SQL Server Native Client desde o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|O OLE DB preenche apenas até a escala definida.|Para conversões onde os dados convertidos são enviados para o servidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (a partir do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) preenche zeros à direita em dados apenas até o comprimento máximo de **datetime** valores. O SQL Server Native Client 9.0 e preenchia até nove dígitos.|  
|Valide DBTYPE_DBTIMESTAMP para ICommandWithParameter::SetParameterInfo.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (a partir [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) implementa o requisito OLE DB de *bScale* em ICommandWithParameter::SetParameterInfo a ser definido com precisão os segundos fracionários para DBTYPE_DBTIMESTAMP.|  
|O **sp_columns** procedimento armazenado agora retorna **"Não"** em vez de **"Não"** para a coluna IS_NULLABLE.|A partir [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]), **sp_columns** procedimento armazenado agora retorna **"Não"** , em vez de **"Não"** para uma coluna IS_NULLABLE .|  
|SQLBindCol, SQLBindParameter e SQLSetDescRec agora realizam a verificação de consistência.|Antes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, a configuração de SQL_DESC_DATA_PTR não causou uma verificação de consistência para qualquer tipo de descritor no SQLBindCol, SQLBindParameter ou SQLSetDescRec.|  
|Agora, SQLCopyDesc faz a verificação de consistência do descritor.|Antes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, SQLCopyDesc não fez uma verificação de consistência quando o campo SQL_DESC_DATA_PTR estava definido em um registro específico.|  
|SQLGetDescRec não é mais uma descritor verificação de consistência.|Antes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, SQLGetDescRec realizada uma verificação de consistência do descritor quando o campo SQL_DESC_DATA_PTR estava definido. Isso não era exigido pela especificação ODBC e, no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) e em versões posteriores, essa verificação de consistência não é mais executada.|  
|Erro diferente retornado quando a data está fora do intervalo.|Para o **datetime** tipo, um número de erro diferente será retornado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (a partir do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) para uma fora do intervalo de datas que era retornado em versões anteriores.<br /><br /> Especificamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 retornava 22007 para todos os valores de ano de intervalo em conversões de cadeia de caracteres para fora **datetime**, e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a partir versão 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) retorna 22008 quando a data está dentro do intervalo com suporte pelo **datetime2** , mas fora do intervalo aceito por **datetime** ou **smalldatetime**.|  
|O valor **datetime** trunca segundos fracionários e não será arredondado se o arredondamento alterar o dia.|Antes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, o comportamento do cliente para valores **datetime** enviados ao servidor era arredondá-los para o 1/300º de segundo mais próximo. A partir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, esse cenário provocará um truncamento de segundos fracionários, se o arredondamento alterar o dia.|  
|Possível truncamento de segundos para **datetime** valor.|Um aplicativo compilado com o [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (ou posterior) que se conecta a um servidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 truncará segundos e segundos fracionários na parte de hora dos dados enviados ao servidor, se for feita uma associação com uma coluna datetime com um identificador de tipo DBTYPE_DBTIMESTAMP (OLE DB) ou SQL_TIMESTAMP (ODBC) e uma escala de 0.<br /><br /> Por exemplo:<br /><br /> Dados de entrada: 1994-08-21 21:21:36.000<br /><br /> Dados inseridos: 1994-08-21 21:21:00.000|  
|A conversão de dados OLE DB de DBTYPE_DBTIME em DBTYPE_DATE não faz mais com que o dia seja alterado.|Antes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, se a parte de hora de DBTYPE_DATE estivesse dentro de meio segundo de meia-noite, o código de conversão OLE DB fazia com que o dia fosse alterado. A partir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, o dia não será alterado (segundos fracionários são truncados e não são arredondados).|  
|Alterações de conversão IBCPSession::BCColFmt.|A partir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, quando você usa IBCPSession::BCOColFmt para converter SQLDATETIME ou SQLDATETIME em um tipo de cadeia de caracteres, um valor fracionário será exportado. Por exemplo, na conversão do tipo SQLDATETIME no tipo SQLNVARCHARMAX, versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client retornavam<br /><br /> 1989-02-01 00:00:00. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 e versões posteriores retornam 1989-02-01 00:00:00.0000000.|  
|O tamanho dos dados enviados deve corresponder ao comprimento especificado em SQL_LEN_DATA_AT_EXEC.|Quando SQL_LEN_DATA_AT_EXEC for usado, o tamanho dos dados deverá corresponder ao comprimento especificado com SQL_LEN_DATA_AT_EXEC. Você pode usar SQL_DATA_AT_EXEC, mas existem benefícios de desempenho potenciais em usar SQL_LEN_DATA_AT_EXEC.|  
|Os aplicativos personalizados que usam a API BCP agora podem ver um aviso.|A API BCP gerará uma mensagem de aviso se o comprimento dos dados for maior do que o comprimento especificado para um campo para todos os tipos. Anteriormente, esse aviso era fornecido apenas para tipos de caracteres, mas não será emitido para todos os tipos.|  
|A inserção de uma cadeia de caracteres vazia em uma associação **sql_variant** como um tipo de data/hora gera um erro.|No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0, a inserção de uma cadeia de caracteres vazia em uma associação **sql_variant** como um tipo de data/hora não gerava um erro. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 (e posterior) gera corretamente um erro nessa situação.|  
|Validação mais rígida dos parâmetros SQL_C_TYPE _TIMESTAMP e DBTYPE_DBTIMESTAMP.|Anteriores ao [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client, **datetime** valores foram arredondados para se ajustar a escala dos **datetime** e **smalldatetime** colunas por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client (bem como as versões posteriores) aplica as regras de validação mais rígidas que são definidas na especificação ODBC principal para segundos fracionários. Se não for possível converter um valor de parâmetro no tipo SQL usando a escala especificada ou implícita pela associação de cliente sem truncamento de dígitos à direita, será retornado um erro.|  
|O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode retornar resultados diferentes quando um gatilho é executado.|As alterações introduzidas no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] podem fazer com que um aplicativo retorne resultados diferentes de uma instrução que causou a execução de um gatilho quando **NOCOUNT OFF** estava em vigor. Nessa situação, o aplicativo pode gerar um erro. Para resolver esse erro, defina **NOCOUNT ON** no gatilho ou chame SQLMoreResults para Avançar para o próximo resultado.|  
  
## <a name="see-also"></a>Consulte também  
 [Programação do SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
