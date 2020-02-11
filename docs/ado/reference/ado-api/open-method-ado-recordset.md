---
title: Método Open (conjunto de registros ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16142f200e6fd6e7c141b4f1fe6d45fe8917bc28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931901"
---
# <a name="open-method-ado-recordset"></a>Método Open (Conjunto de registros ADO)
Abre um cursor em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>parâmetros  
 *Origem*  
 Opcional. Uma **variante** que é avaliada como um objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) válido, uma instrução SQL, um nome de tabela, uma chamada de procedimento armazenado, uma URL ou o nome de um objeto de arquivo ou de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) que contém um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)armazenado de forma persistente.  
  
 *ActiveConnection*  
 Opcional. Uma **variante** que é avaliada como um nome de variável de objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) válido ou uma **cadeia de caracteres** que contém parâmetros [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) .  
  
 *CursorType*  
 Opcional. Um valor [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) que determina o tipo de cursor que o provedor deve usar ao abrir o **conjunto de registros**. O valor padrão é **adOpenForwardOnly**.  
  
 *LockType*  
 Opcional. Um valor [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) que determina o tipo de bloqueio (simultaneidade) que o provedor deve usar ao abrir o **conjunto de registros**. O valor padrão é **adLockReadOnly**.  
  
 *Opções*  
 Opcional. Um valor **longo** que indica como o provedor deve avaliar o argumento de *origem* se ele representar algo diferente de um objeto de **comando** ou se o **conjunto de registros** deve ser restaurado de um arquivo em que foi salvo anteriormente. Pode ser um ou mais valores de [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) ou de [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) , que podem ser combinados com um operador OR bit a bit.  
  
> [!NOTE]
>  Se você abrir um **conjunto de registros** de um **fluxo** que contém um **conjunto de registros**persistente, usar um valor [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) de **adAsyncFetchNonBlocking** não terá nenhum efeito; a busca será síncrona e bloqueada.  
  
> [!NOTE]
>  Os valores de **ExecuteOpenEnum** de **adExecuteNoRecords** ou **adExecuteStream** não devem ser usados com **Open**.  
  
## <a name="remarks"></a>Comentários  
 O cursor padrão de um **conjunto de registros** ADO é um cursor somente de avanço, somente leitura localizado no servidor.  
  
 O uso do método **Open** em um objeto **Recordset** abre um cursor que representa os registros de uma tabela base, os resultados de uma consulta ou um **conjunto de registros**salvo anteriormente.  
  
 Use o argumento de *origem* opcional para especificar uma fonte de dados usando uma das seguintes opções: uma variável de objeto de **comando** , uma instrução SQL, um procedimento armazenado, um nome de tabela, uma URL ou um nome de caminho de arquivo completo. Se *Source* for um nome de caminho de arquivo, ele pode ser um caminho completo ("c:\dir\file.RST"), um caminho relativo (".. \File.RST ") ou uma URL ("<https://files/file.rst>").  
  
 Não é uma boa ideia usar o argumento de *origem* do método **Open** para executar uma consulta de ação que não retorna registros porque não há uma maneira fácil de determinar se a chamada foi bem-sucedida. O **conjunto de registros** retornado por tal consulta será fechado. Para executar uma consulta que não retorna registros, como uma instrução SQL INSERT, chame o método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) de um objeto **Command** ou o método [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) de um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) em vez disso.  
  
 O argumento *ActiveConnection* corresponde à propriedade [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) e especifica em qual conexão abrir o objeto **Recordset** . Se você passar uma definição de conexão para esse argumento, o ADO abrirá uma nova conexão usando os parâmetros especificados. Depois de abrir o **conjunto de registros** com um cursor do lado do cliente, definindo a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) como **adUseClient**, você pode alterar o valor dessa propriedade para enviar atualizações para outro provedor. Ou você pode definir essa propriedade como **Nothing** (no Microsoft Visual Basic) ou NULL para desconectar o **conjunto de registros** de qualquer provedor. No entanto, alterar a *ActiveConnection* para um cursor do lado do servidor gera um erro.  
  
 Para os outros argumentos que correspondem diretamente às propriedades de um objeto **Recordset** (*Source*, *CursorType*e *LockType*), a relação dos argumentos para as propriedades é a seguinte:  
  
-   A propriedade é de leitura/gravação antes de o objeto **Recordset** ser aberto.  
  
-   As configurações de propriedade são usadas, a menos que você passe os argumentos correspondentes ao executar o método **Open** . Se você passar um argumento, ele substituirá a configuração de propriedade correspondente e a configuração de propriedade será atualizada com o valor do argumento.  
  
-   Depois de abrir o objeto **Recordset** , essas propriedades tornam-se somente leitura.  
  
> [!NOTE]
>  A propriedade **ActiveConnection** é somente leitura para objetos **Recordset** cuja propriedade [Source](../../../ado/reference/ado-api/source-property-ado-recordset.md) está definida como um objeto de **comando** válido, mesmo que o objeto **Recordset** não esteja aberto.  
  
 Se você passar um objeto de **comando** no argumento de *origem* e também passar um argumento *ActiveConnection* , ocorrerá um erro. A propriedade **ActiveConnection** do objeto **Command** já deve estar definida como uma cadeia de conexão ou objeto de **conexão** válido.  
  
 Se você passar algo diferente de um objeto de **comando** no argumento de *origem* , poderá usar o argumento *Options* para otimizar a avaliação do argumento de *origem* . Se o argumento *Options* não estiver definido, você poderá enfrentar um desempenho reduzido porque o ADO deve fazer chamadas ao provedor para determinar se o argumento é uma instrução SQL, um procedimento armazenado, uma URL ou um nome de tabela. Se você souber qual tipo de *fonte* está usando, definir o argumento *Options* instrui o ADO a saltar diretamente para o código relevante. Se o argumento *Options* não corresponder ao tipo *Source* , ocorrerá um erro.  
  
 Se você passar um objeto de **fluxo** no argumento de *origem* , não deverá passar informações para os outros argumentos. Isso vai gerar um erro. As informações de **ActiveConnection** não são mantidas quando um **conjunto de registros** é aberto a partir de um **fluxo**.  
  
 O padrão para o argumento *Options* será **adCmdFile** se nenhuma conexão estiver associada ao **conjunto de registros**. Normalmente, esse será o caso para objetos **Recordset** armazenados persistentemente.  
  
 Se a fonte de dados não retornar nenhum registro, o provedor definirá as propriedades [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) como **true**e a posição do registro atual será indefinida. Você ainda poderá adicionar novos dados a este objeto **Recordset** vazio se o tipo de cursor permitir.  
  
 Quando você tiver concluído suas operações em um objeto Open **Recordset** , use o método [Close](../../../ado/reference/ado-api/close-method-ado.md) para liberar todos os recursos do sistema associados. Fechar um objeto não o Remove da memória; Você pode alterar suas configurações de propriedade e usar o método **Open** para abri-lo novamente mais tarde. Para eliminar completamente um objeto da memória, defina a variável de objeto como *Nothing*.  
  
 Antes que a propriedade **ActiveConnection** seja definida, chame **Open** sem operandos para criar uma instância de um **conjunto de registros** criado acrescentando campos à coleção [campos](../../../ado/reference/ado-api/fields-collection-ado.md) do **conjunto de registros** .  
  
 Se você tiver definido a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) como **adUseClient**, poderá recuperar linhas de forma assíncrona de uma das duas maneiras. O método recomendado é definir *Opções* como **adAsyncFetch**. Como alternativa, você pode usar a propriedade dinâmica "processamento de conjunto de linhas assíncrono" na coleção [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) , mas eventos recuperados relacionados podem ser perdidos se você não definir o parâmetro *Options* como **adAsyncFetch**.  
  
> [!NOTE]
>  A busca em segundo plano no provedor remoto MS tem suporte apenas por meio do parâmetro *Options* do método **Open** .  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Determinadas combinações de valores [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) e [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) não são válidas. Para obter informações sobre quais opções não podem ser combinadas, consulte os tópicos para [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)e [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Exemplo dos métodos Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Exemplo dos métodos Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Exemplo dos métodos Save e Open (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Método Open (conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (registro ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (fluxo ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
