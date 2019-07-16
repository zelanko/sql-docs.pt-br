---
title: Método (conjunto de registros ADO) Open | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931901"
---
# <a name="open-method-ado-recordset"></a>Método Open (Conjunto de registros ADO)
Abre um cursor em uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Source*  
 Opcional. Um **Variant** que é avaliada como um válido [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto, uma instrução SQL, um nome de tabela, uma chamada de procedimento armazenado, uma URL ou o nome de um arquivo ou [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto que contém um persistentemente armazenado [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 *ActiveConnection*  
 Opcional. Qualquer um **Variant** que é avaliada como um válido [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) nome de variável de objeto, ou uma **cadeia de caracteres** que contém [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) parâmetros.  
  
 *CursorType*  
 Opcional. Um [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) valor que determina o tipo de cursor que o provedor deve usar ao abrir o **conjunto de registros**. O valor padrão é **adOpenForwardOnly**.  
  
 *LockType*  
 Opcional. Um [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valor que determina que tipo de bloqueio (simultaneidade) o provedor deve usar ao abrir o **conjunto de registros**. O valor padrão é **adLockReadOnly**.  
  
 *Opções*  
 Opcional. Um **longo** valor que indica como o provedor deve avaliar o *fonte* argumento se ele representa algo diferente de um **comando** objeto, ou que o **Recordset** deve ser restaurado de um arquivo de onde ele foi salvo anteriormente. Pode ser um ou mais [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) ou [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores, que podem ser combinados com um operador OR bit a bit.  
  
> [!NOTE]
>  Se você abrir um **conjunto de registros** de uma **Stream** que contém um persistente **conjunto de registros**, usando um [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valor de **adAsyncFetchNonBlocking** não terá efeito, a busca será síncrona e bloqueio.  
  
> [!NOTE]
>  O **ExecuteOpenEnum** valores de **adExecuteNoRecords** ou **adExecuteStream** não deve ser usado com **abrir**.  
  
## <a name="remarks"></a>Comentários  
 O cursor padrão para ADO **Recordset** é um cursor somente encaminhamento, somente leitura, localizado no servidor.  
  
 Usando o **aberto** método em um **conjunto de registros** objeto abre um cursor que representa os registros de uma tabela base, os resultados de uma consulta ou salvo anteriormente **conjunto de registros**.  
  
 Usar a opção *fonte* argumento para especificar uma fonte de dados usando um dos seguintes: um **comando** variável de objeto, uma instrução SQL, um procedimento armazenado, um nome de tabela, uma URL ou um nome de caminho de arquivo completo. Se *origem* é um nome de caminho de arquivo, ele pode ser um caminho completo ("c:\dir\file.rst"), um caminho relativo ("... \file.RST"), ou uma URL ("<https://files/file.rst>").  
  
 Não é uma boa ideia usar o *fonte* argumento do **abrir** método para executar uma consulta de ação que não retorna registros porque não há nenhuma maneira fácil de determinar se a chamada foi bem-sucedida. O **Recordset** retornado por como uma consulta será fechada. Para executar uma consulta que retorna registros, como uma instrução SQL INSERT, chame o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método de um **comando** objeto ou o [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto em vez disso.  
  
 O *ActiveConnection* argumento corresponde à [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade e especifica em qual conexão para abrir o **Recordset** objeto. Se você passar uma definição de conexão para esse argumento, o ADO abre uma nova conexão usando os parâmetros especificados. Depois de abrir o **conjunto de registros** com um cursor do lado do cliente, definindo o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade a ser **adUseClient**, você pode alterar o valor dessa propriedade para enviar atualizações para outro provedor. Ou você pode definir essa propriedade para **nada** (no Microsoft Visual Basic) ou nulo para desconectar o **conjunto de registros** de qualquer provedor. Alterando *ActiveConnection* para um cursor de servidor gera um erro, no entanto.  
  
 Para os outros argumentos que correspondem diretamente às propriedades de um **conjunto de registros** objeto (*fonte*, *CursorType*, e *LockType*), a relação dos argumentos para as propriedades é da seguinte maneira:  
  
-   A propriedade é leitura/gravação antes do **Recordset** objeto é aberto.  
  
-   As configurações de propriedade são usadas, a menos que você passe os argumentos correspondentes ao executar o **abrir** método. Se você passar um argumento, ela substitui a configuração de propriedade correspondente e a configuração da propriedade é atualizada com o valor do argumento.  
  
-   Depois de abrir o **Recordset** do objeto, essas propriedades se tornar somente leitura.  
  
> [!NOTE]
>  O **ActiveConnection** propriedade é somente leitura para **conjunto de registros** objetos cujo [origem](../../../ado/reference/ado-api/source-property-ado-recordset.md) propriedade é definida como válido **comando** objeto, mesmo se o **Recordset** objeto não está aberto.  
  
 Se você passar uma **comando** do objeto na *fonte* argumento e também passe um *ActiveConnection* argumento, um erro ocorre. O **ActiveConnection** propriedade da **comando** objeto já deve ser definido como válido **Conexão** cadeia de caracteres de conexão ou objeto.  
  
 Se você passar algo diferente de um **comando** do objeto na *fonte* argumento, você pode usar o *opções* argumento para otimizar a avaliação do *fonte*  argumento. Se o *opções* argumento não for definido, você pode enfrentar desempenho diminuído porque ADO deve fazer chamadas para o provedor para determinar se o argumento é uma instrução SQL, um procedimento armazenado, uma URL ou um nome de tabela. Se você souber o que *fonte* tipo você está usando, definindo o *opções* argumento instrui o ADO para ir diretamente para o código relevante. Se o *opções* argumento não corresponde a *origem* digitar, ocorrerá um erro.  
  
 Se você passar uma **Stream** do objeto na *origem* argumento, você não deve passar informações para os outros argumentos. Isso gerará um erro. O **ActiveConnection** informações não são mantidos quando um **conjunto de registros** é aberta a partir um **Stream**.  
  
 O padrão para o *opções* argumento é **adCmdFile** se nenhuma conexão é associado com o **conjunto de registros**. Isso geralmente será o caso de maneira persistente armazenadas **Recordset** objetos.  
  
 Se a fonte de dados não retornar nenhum registro, o provedor define tanto a [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propriedades a serem **verdadeiro**, e a posição do registro atual é indefinida. Você ainda pode adicionar novos dados nesse vazia **Recordset** se o tipo de cursor permite que ele do objeto.  
  
 Quando você ter concluído suas operações ao longo de um aberto **conjunto de registros** do objeto, use o [fechar](../../../ado/reference/ado-api/close-method-ado.md) associado de método para liberar todos os recursos do sistema. Um objeto de fechamento não o remove da memória; Você pode alterar suas configurações de propriedade e usar o **abrir** método para abri-lo novamente mais tarde. Para eliminar completamente um objeto da memória, defina a variável de objeto para *nada*.  
  
 Antes do **ActiveConnection** estiver definida, chame **aberto** com nenhum operandos para criar uma instância de um **conjunto de registros** criado acrescentando campos a serem o  **Conjunto de registros** [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção.  
  
 Se você tiver definido o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient**, você pode recuperar linhas de forma assíncrona em uma das duas maneiras. O método recomendado é definir *opções* à **adAsyncFetch**. Como alternativa, você pode usar a propriedade dinâmica "Processamento de conjunto de linhas assíncrono" na [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção, mas eventos recuperados relacionados podem ser perdidos se você não definir o *opções* parâmetro **adAsyncFetch**.  
  
> [!NOTE]
>  Busca de tela de fundo no provedor Remote MS é suportado somente por meio de **aberto** do método *opções* parâmetro.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Algumas combinações de [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) e [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores não são válidos. Para obter informações sobre quais opções não podem ser combinadas, consulte os tópicos para o [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md), e [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo dos métodos Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Exemplo dos métodos Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Exemplo dos métodos Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Salvar e abrir um exemplo dos métodos (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Método Open (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (registro ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Exemplo do método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
