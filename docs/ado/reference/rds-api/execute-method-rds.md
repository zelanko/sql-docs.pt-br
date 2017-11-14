---
title: "Executar método (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 2d9c30e9-ab5b-4920-91b8-48454c2fb5d8
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 68796c4fa28d3ee553ccf7c44e9bbd9850f32fb7
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-rds"></a>Executar método (RDS)
Executa a solicitação e cria um conjunto de registros ADO para uso no ADO 2.5 e superior.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Execute(ConnectionString As String, HandlerString As String, QueryString As String, lFetchOptions As Long, Properties, TableId, lExecuteOptions As Long, pParameters, [lcid As Long], [pInformation])  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectionString*  
 Uma cadeia de caracteres usada para conexão com o provedor OLE DB em que a solicitação será enviada para execução. Se for especificado um manipulador usando *HandlerString* pode editar ou substituir a cadeia de caracteres de conexão.  
  
 *HandlerString*  
 Uma cadeia de caracteres de duas partes que identifica o manipulador a ser usado com essa execução. A cadeia de caracteres contém duas partes. A primeira parte contém o nome (ProgID) do manipulador a ser usado. A segunda parte contém argumentos a serem passados para o manipulador. Os detalhes de como a cadeia de caracteres de argumentos é interpretada são específicos para cada manipulador. As duas partes são separadas pela primeira instância de uma vírgula na cadeia de caracteres. A cadeia de caracteres de argumentos pode conter vírgulas adicionais. Os argumentos são opcionais.  
  
 *QueryString*  
 Um comando na linguagem de comando suportado pelo provedor OLE DB identificado na cadeia de conexão. Para provedores baseados em SQL, *QueryString* pode conter uma instrução de comando Transact-SQL, mas para provedores não-SQL (por exemplo, MSDataShape) isso pode não ser um [!INCLUDE[tsql](../../../includes/tsql_md.md)] instrução de consulta.  
  
 Se um manipulador está sendo usado, o manipulador pode alterar ou substituir o valor especificado aqui. Por exemplo, o manipulador geralmente substitui *QueryString* com uma cadeia de caracteres de consulta de seu arquivo. ini. Por padrão, o arquivo Msdfmap.ini é usado.  
  
 *lFetchOptions*  
 Indica o tipo de busca de maneira assíncrona.  
  
 Para obter mais informações, consulte [FetchOptions propriedade (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md).  
  
 *TableID*  
 Um **Variant** do tipo VT_EMPTY ou VT_BSTR. Se esse valor é do tipo VT_EMPTY, ele será ignorado. Se ela é do tipo VT_BSTR, o conjunto de registros é criado usando **adCmdTableDirect** e o valor especificado aqui e *QueryString* parâmetro é ignorado.  
  
 *lExecuteOptions*  
 Uma máscara de bits de opções de execução:  
  
 1 =*ReadOnly* o conjunto de registros será aberto usando **adLockReadOnly**.  
  
 2 =*NoBatch* o conjunto de registros será aberto usando **adLockOptimistic**.  
  
 4 =*AllParamInfoSupplied* o chamador garante que as informações de parâmetro para todos os parâmetros são fornecidas em *pParameters*.  
  
 8 =*GetInfo* informações de parâmetro para a consulta serão obtidas do provedor de OLE DB e retornadas no *pParameters* parâmetro. A consulta não é executada e nenhum conjunto de registros é retornado.  
  
 16 =*GetHiddenColumns* o conjunto de registros será aberto usando **adLockBatchOptimistic** e as colunas ocultas serão incluídas no conjunto de registros.  
  
 *ReadOnly*, *NoBatch* e *GetHiddenColumns* são opções mutuamente exclusivas; no entanto, ele não gera um erro para definir mais de uma. Se várias opções forem definidas, *GetHiddenColumns* tem precedência sobre todas as outras, seguido por *ReadOnly*. Se nenhuma opção for especificada, por padrão, o conjunto de registros é aberto usando **adLockBatchOptimistic** e colunas ocultas não são incluídas no conjunto de registros.  
  
 *pParameters*  
 Um **Variant** que contém uma matriz segura de definições de parâmetro. Se o *GetInfo* opção foi especificada no *lExecuteOptions*, esse parâmetro é usado para retornar as definições de parâmetro obtidas do provedor OLE DB. Caso contrário, esse parâmetro pode ser vazio.  
  
 *lcid*  
 O LCID usado para criar os erros que são retornados no *pInformation*.  
  
 *pInformation*  
 Um ponteiro para o erro de informações retornado pela execução. Se for NULL, nenhuma informação de erro é retornada.  
  
## <a name="remarks"></a>Comentários  
 O *HandlerString* parâmetro pode ser nulo. O que acontece nesse caso depende de como o servidor RDS é configurado. Uma cadeia de caracteres do manipulador de "MSDFMAP.handler" indica que o manipulador fornecido pela Microsoft (Msdfmap.dll) deve ser usado. Uma cadeia de caracteres do manipulador de "MASDFMAP.handler,sample.ini" indica que o manipulador Msdfmap.dll deve ser usado e que o argumento "sample.ini" deve ser passado para o manipulador. MSDFMAP.dll interpretará o argumento como uma direção para usar o sample.ini para verificar se as cadeias de caracteres de conexão e consulta.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)



