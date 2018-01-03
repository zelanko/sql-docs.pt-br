---
title: "Executar método (Conexão ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords: Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 071e752063020ace305371f814f1b78224dbb9a4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="execute-method-ado-connection"></a>Executar método (Conexão ADO)
Executa a consulta especificada, instrução SQL, procedimento armazenado ou texto específico do provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um [Recordset Object (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) referência de objeto.  
  
#### <a name="parameters"></a>Parâmetros  
 *CommandText*  
 Um **cadeia de caracteres** valor que contém a instrução SQL, procedimento armazenado, uma URL ou texto específico do provedor para executar. **Opcionalmente,**, nomes de tabela podem ser usados mas somente se o provedor está ciente do SQL. Por exemplo, se um nome de tabela de "Clientes" é usado, ADO será automaticamente preceda a sintaxe SQL Select padrão para o formulário e passar "SELECT * FROM Customers" como um [!INCLUDE[tsql](../../../includes/tsql_md.md)] instrução para o provedor.  
  
 *RecordsAffected*  
 Opcional. Um **longo** variável na qual o provedor retorna o número de registros afetada a operação.  
  
 *Opções*  
 Opcional. Um **longo** valor que indica como o provedor deve avaliar o argumento CommandText. Pode ser um bitmask de um ou mais [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) ou [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores.  
  
 **Observação** Use o **ExecuteOptionEnum** valor **adExecuteNoRecords** para melhorar o desempenho, reduzindo o processamento interno e para aplicativos que você estiver portando do Visual Basic 6.0.  
  
 Não use **adExecuteStream** com o **Execute** método de um **Conexão** objeto.  
  
 Não use os valores de CommandTypeEnum de adCmdFile ou adCmdTableDirect com Execute. Esses valores podem ser usados apenas como opções com a [método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [método Requery](../../../ado/reference/ado-api/requery-method.md) métodos de um **registros**.  
  
## <a name="remarks"></a>Remarks  
 Usando o **Execute** método em um [Conexão Object (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) objeto executa qualquer consulta que você passa para o método no argumento CommandText sobre a conexão especificada. Se o argumento CommandText Especifica uma consulta de retorno de linha, os resultados que gera a execução são armazenados em uma nova **registros** objeto. Se o comando não se destina para retornar resultados (por exemplo, uma consulta de atualização do SQL) o provedor retorna **nada** desde que a opção **adExecuteNoRecords** for especificado; caso contrário, Execute retorna um fechado **registros**.  
  
 Retornado **registros** objeto é sempre um cursor somente leitura, somente encaminhamento. Se você precisar de um **Recordset** com mais funcionalidades de objeto, primeiro crie um **registros** do objeto com as configurações de propriedade desejados e use o **Recordset** objeto [ Método (conjunto de registros ADO) Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para executar a consulta e retorna o tipo de cursor desejados.  
  
 O conteúdo do *CommandText* argumento são específico para o provedor e pode ser sintaxe SQL padrão ou qualquer formato de comando especial que o provedor oferece suporte.  
  
 Um evento ExecuteComplete será emitido quando conclui a operação.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
