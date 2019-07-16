---
title: Executar método (Conexão ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4999b1e21ec145713cadae28ff7ee8a64dd460b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932899"
---
# <a name="execute-method-ado-connection"></a>Método Execute (conexão ADO)
Executa a consulta especificada, instrução SQL, procedimento armazenado ou texto específico do provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) referência de objeto.  
  
#### <a name="parameters"></a>Parâmetros  
 *CommandText*  
 Um **cadeia de caracteres** valor que contém a instrução SQL, procedimento armazenado, uma URL ou texto específico do provedor para executar. **Opcionalmente,** , nomes de tabela podem ser usados, mas somente se o provedor estiver ciente de SQL. Por exemplo, se um nome de tabela "Clientes" for usado, ADO será automaticamente preceda a sintaxe SQL Select padrão para formar e passar "SELECT * FROM Customers" como um [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução para o provedor.  
  
 *RecordsAffected*  
 Opcional. Um **longo** variável na qual o provedor retorna o número de registros afetada da operação.  
  
 *Opções*  
 Opcional. Um **longo** valor que indica como o provedor deve avaliar o argumento CommandText. Pode ser uma bitmask de um ou mais [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) ou [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores.  
  
 **Observação** Use o **ExecuteOptionEnum** valor **adExecuteNoRecords** para melhorar o desempenho, minimizando o processamento interno e para aplicativos que você estiver portando do Visual Basic 6.0.  
  
 Não use **adExecuteStream** com o **Execute** método de um **Conexão** objeto.  
  
 Não use os valores de CommandTypeEnum de adCmdFile ou adCmdTableDirect com Execute. Esses valores só podem ser usados como opções com o [método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [método Requery](../../../ado/reference/ado-api/requery-method.md) métodos de um **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 Usando o **Execute** método em um [o objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) objeto executa qualquer consulta que você passa para o método no argumento CommandText sobre a conexão especificada. Se o argumento de CommandText Especifica uma consulta de retorno de linha, qualquer resultado que gera a execução é armazenado em uma nova **Recordset** objeto. Se o comando não se destina para retornar resultados (por exemplo, uma consulta de atualização do SQL) o provedor retorna **nada** desde que a opção **adExecuteNoRecords** é especificado; caso contrário, Execute retorna um fechado **conjunto de registros**.  
  
 Retornado **Recordset** objeto é sempre um cursor de somente leitura, somente encaminhamento. Se precisar de um **conjunto de registros** objeto com mais funcionalidade, primeiro crie um **conjunto de registros** do objeto com as configurações de propriedade desejada, em seguida, use o **conjunto de registros** objeto [ Método (conjunto de registros ADO) Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) método para executar a consulta e retornar o tipo de cursor desejados.  
  
 O conteúdo a *CommandText* argumento são específico ao provedor e pode ser sintaxe SQL padrão ou qualquer formato de comando especial que o provedor oferece suporte.  
  
 Um evento ExecuteComplete será emitido quando conclui essa operação.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
