---
description: Método Execute (RDS)
title: Método Execute (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f1c68dc55a4ae57283ce4ca7e6d357fd47030e4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768435"
---
# <a name="execute-method-rds"></a>Método Execute (RDS)
Executa a solicitação e cria um conjunto de registros ADO para uso no ADO 2,5 e posterior.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Uma cadeia de caracteres usada para se conectar ao provedor de OLE DB em que a solicitação será enviada para execução. Se um manipulador for especificado usando *handlerString* , ele poderá editar ou substituir a cadeia de conexão.  
  
 *HandlerString*  
 Uma cadeia de caracteres de duas partes que identifica o manipulador a ser usado com essa execução. A cadeia de caracteres contém duas partes. A primeira parte contém o nome (ProgID) do manipulador a ser usado. A segunda parte contém argumentos a serem passados para o manipulador. Os detalhes de como a cadeia de caracteres de argumentos são interpretados são específicos para cada manipulador. As duas partes são separadas pela primeira instância de uma vírgula na cadeia de caracteres. A cadeia de caracteres de argumentos pode conter vírgulas adicionais. Os argumentos são opcionais.  
  
 *QueryString*  
 Um comando no idioma de comando com suporte do provedor de OLE DB identificado na cadeia de conexão. Para provedores baseados em SQL, o *QueryString* pode conter uma instrução de comando TRANSACT-SQL, mas para provedores não SQL (por exemplo, MSDataShape), isso pode não ser uma [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução de consulta.  
  
 Se um manipulador estiver sendo usado, o manipulador poderá alterar ou substituir o valor especificado aqui. Por exemplo, o manipulador normalmente substitui o *QueryString* por uma cadeia de caracteres de consulta de seu arquivo. ini. Por padrão, o arquivo de Msdfmap.ini é usado.  
  
 *lFetchOptions*  
 Indica o tipo de busca assíncrona.  
  
 Para obter mais informações, consulte [Propriedades de FetchOptions (RDS)](./fetchoptions-property-rds.md).  
  
 *TableID*  
 Uma **variante** do tipo VT_EMPTY ou VT_BSTR. Se esse valor for do tipo VT_EMPTY, ele será ignorado. Se for do tipo VT_BSTR, o conjunto de registros será criado usando **adCmdTableDirect** e o valor especificado aqui e o parâmetro *QueryString* será ignorado.  
  
 *lExecuteOptions*  
 Uma máscara de bits de opções de execução:  
  
 1 =*ReadOnly* o conjunto de registros será aberto usando **adLockReadOnly**.  
  
 2 =*nobatch* , o conjunto de registros será aberto usando **adLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* o chamador garante que as informações de parâmetro para todos os parâmetros sejam fornecidas em *pParameters*.  
  
 8 = as informações de parâmetro*GetInfo* para a consulta serão obtidas do provedor de OLE DB e retornadas no parâmetro *pParameters* . A consulta não é executada e nenhum conjunto de registros é retornado.  
  
 16 =*GetHiddenColumns* o conjunto de registros será aberto usando **adLockBatchOptimistic** e todas as colunas ocultas serão incluídas no conjunto de registros.  
  
 *ReadOnly*, *nobatch* e *GetHiddenColumns* são opções mutuamente exclusivas; no entanto, ele não gera um erro para definir mais de um deles. Se várias opções forem definidas, *GetHiddenColumns* terá precedência sobre todas as outras, seguidas por *ReadOnly*. Se nenhuma opção for especificada, por padrão, o conjunto de registros será aberto usando **adLockBatchOptimistic** e as colunas ocultas não serão incluídas no conjunto de registros.  
  
 *pParameters*  
 Uma **variante** que contém uma matriz segura de definições de parâmetro. Se a opção *GetInfo* tiver sido especificada em *lExecuteOptions*, esse parâmetro será usado para retornar as definições de parâmetro obtidas do provedor de OLE DB. Caso contrário, esse parâmetro poderá ficar vazio.  
  
 *lcid*  
 O LCID usado para criar os erros retornados em *pInformation*.  
  
 *pInformation*  
 Um ponteiro para erro de informação retornado por execute. Se for NULL, nenhuma informação de erro será retornada.  
  
## <a name="remarks"></a>Comentários  
 O parâmetro *handlerString* pode ser nulo. O que acontece nesse caso depende de como o servidor RDS está configurado. Uma cadeia de caracteres do manipulador de "MSDFMAP. Handler" indica que o manipulador fornecido pela Microsoft (Msdfmap.dll) deve ser usado. Uma cadeia de caracteres do manipulador de "MASDFMAP. Handler, sample.ini" indica que o manipulador de Msdfmap.dll deve ser usado e que o argumento "sample.ini" deve ser passado para o manipulador. MSDFMAP.dll irá interpretar o argumento como uma direção para usar a sample.ini para verificar a conexão e as cadeias de caracteres de consulta.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataFactory (RDSServer)](./datafactory-object-rdsserver.md)