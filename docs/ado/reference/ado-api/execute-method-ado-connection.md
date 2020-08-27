---
description: Método Execute (conexão ADO)
title: Método Execute (conexão ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d5f0c63773a0eb07233ffff0eb74f39e45baf33
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973547"
---
# <a name="execute-method-ado-connection"></a>Método Execute (conexão ADO)
Executa a consulta especificada, a instrução SQL, o procedimento armazenado ou o texto específico do provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna uma referência de objeto de [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
#### <a name="parameters"></a>Parâmetros  
 *CommandText*  
 Um valor de **cadeia de caracteres** que contém a instrução SQL, o procedimento armazenado, uma URL ou um texto específico do provedor a ser executado. **Opcionalmente**, os nomes de tabela podem ser usados, mas somente se o provedor tiver reconhecimento de SQL. Por exemplo, se o nome de uma tabela de "Customers" for usado, o ADO precederá automaticamente a sintaxe padrão do SQL SELECT para formar e passará "SELECT * FROM Customers" como uma [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrução para o provedor.  
  
 *RecordsAffected*  
 Opcional. Uma variável **longa** para a qual o provedor retorna o número de registros afetados pela operação.  
  
 *Opções*  
 Opcional. Um valor **longo** que indica como o provedor deve avaliar o argumento CommandText. Pode ser um bitmask de um ou mais valores de [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) ou [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) .  
  
 **Observação** Use o **ExecuteOptionEnum** valor ExecuteOptionEnum **adExecuteNoRecords** para melhorar o desempenho, minimizando o processamento interno e para aplicativos dos quais você está portando Visual Basic 6,0.  
  
 Não use **adExecuteStream** com o método **Execute** de um objeto **Connection** .  
  
 Não use os valores de CommandTypeEnum de adCmdFile ou adCmdTableDirect com execute. Esses valores só podem ser usados como opções com o [método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) e métodos de [método Requery](../../../ado/reference/ado-api/requery-method.md) de um **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 O uso do método **Execute** em um objeto de [conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) executa qualquer consulta que você passa para o método no argumento CommandText na conexão especificada. Se o argumento CommandText especificar uma consulta de retorno de linha, todos os resultados gerados pela execução serão armazenados em um novo objeto **Recordset** . Se o comando não se destinar a retornar resultados (por exemplo, uma consulta SQL UPDATE), o provedor não retornará **nada** enquanto a opção **adExecuteNoRecords** for especificada; caso contrário, execute retorna um **conjunto de registros**fechado.  
  
 O objeto **Recordset** retornado é sempre um cursor somente leitura, somente avanço. Se você precisar de um objeto **Recordset** com mais funcionalidade, primeiro crie um objeto **Recordset** com as configurações de propriedade desejadas e use o método [Open Method (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) do objeto **Recordset** para executar a consulta e retornar o tipo de cursor desejado.  
  
 O conteúdo do argumento *CommandText* é específico para o provedor e pode ser a sintaxe SQL padrão ou qualquer formato de comando especial ao qual o provedor dá suporte.  
  
 Um evento ExecuteComplete será emitido quando esta operação for concluída.  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
