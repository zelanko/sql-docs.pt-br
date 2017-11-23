---
title: "Abra o método (conjunto de registros ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_Open
- Recordset15::Open
helpviewer_keywords: Open method [ADO]
ms.assetid: 3236749c-4b71-4235-89e2-ccdfaaa9319d
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 3f223702a882910354d69fbcbfe5920e444000f7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="open-method-ado-recordset"></a>Método Open (conjunto de registros ADO)
Abre um cursor em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Open Source, ActiveConnection, CursorType, LockType, Options  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um **Variant** que é avaliada como uma opção válida [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto, uma instrução SQL, um nome de tabela, uma chamada de procedimento armazenado, uma URL ou o nome de um arquivo ou [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto que contém um armazenado persistentemente [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 *ActiveConnection*  
 Opcional. Qualquer um **Variant** que é avaliada como uma opção válida [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) nome de variável de objeto, ou um **cadeia de caracteres** que contém [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) parâmetros.  
  
 *CursorType*  
 Opcional. Um [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) valor que determina o tipo de cursor que o provedor deve usar ao abrir o **registros**. O valor padrão é **adOpenForwardOnly**.  
  
 *LockType*  
 Opcional. Um [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valor que determina que tipo de bloqueio (simultaneidade) o provedor deve ser usada ao abrir o **registros**. O valor padrão é **adLockReadOnly**.  
  
 *Opções*  
 Opcional. Um **longo** valor que indica como o provedor deve avaliar o *fonte* argumento representa algo diferente de um **comando** objeto, ou que o **Registros** devem ser restaurados de um arquivo de onde ele foi salvo anteriormente. Pode ser um ou mais [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) ou [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores, que podem ser combinados com um operador OR bit a bit.  
  
> [!NOTE]
>  Se você abrir um **registros** de um **fluxo** contendo um persistente **registros**usando um [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valor **adAsyncFetchNonBlocking** não tem efeito; a busca será síncrona e de bloqueio.  
  
> [!NOTE]
>  O **ExecuteOpenEnum** valores de **adExecuteNoRecords** ou **adExecuteStream** não deve ser usada com **abrir**.  
  
## <a name="remarks"></a>Comentários  
 O cursor padrão para ADO **registros** é um cursor somente de avanço, somente leitura, localizado no servidor.  
  
 Usando o **abrir** método em um **registros** objeto abre um cursor que representa os registros de uma tabela base, os resultados de uma consulta ou salvo anteriormente **registros**.  
  
 Use opcional *fonte* argumento para especificar uma fonte de dados usando um dos seguintes: um **comando** variável de objeto, uma instrução SQL, um procedimento armazenado, um nome de tabela, uma URL ou um nome de caminho completo do arquivo. Se *origem* é um nome de caminho de arquivo, ele pode ser um caminho completo ("c:\dir\file.rst"), um caminho relativo ("... \file.RST"), ou uma URL ("http://files/file.rst").  
  
 Não é recomendável usar o *fonte* argumento do **abrir** método para executar uma consulta de ação que não retorna registros porque não há nenhuma maneira fácil de determinar se a chamada foi bem-sucedida. O **registros** retornado por como uma consulta será fechada. Para executar uma consulta que não retorna registros, como uma instrução SQL INSERT, chame o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método de um **comando** objeto ou o [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) método de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto em vez disso.  
  
 O *ActiveConnection* argumento corresponde ao [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade e especifica em qual conexão para abrir o **registros** objeto. Se você passar uma definição de conexão para esse argumento, o ADO abre uma nova conexão usando os parâmetros especificados. Depois de abrir o **registros** com um cursor do lado do cliente, definindo a [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient**, você pode alterar o valor dessa propriedade para enviar atualizações para outro provedor. Ou você pode definir essa propriedade para **nada** (no Microsoft Visual Basic) ou NULL para desconectar o **registros** de qualquer provedor. Alterar *ActiveConnection* para um cursor do lado do servidor gerará um erro, no entanto.  
  
 Para os outros argumentos que correspondem diretamente às propriedades de um **registros** objeto (*fonte*, *CursorType*, e *LockType*), a relação dos argumentos para as propriedades é o seguinte:  
  
-   A propriedade é leitura/gravação antes do **registros** objeto é aberto.  
  
-   As configurações de propriedade são usadas, a menos que você passa os argumentos correspondentes ao executar o **abrir** método. Se você passar um argumento, ela substitui a configuração da propriedade correspondente e a configuração da propriedade é atualizada com o valor do argumento.  
  
-   Depois de abrir o **registros** do objeto, essas propriedades são somente leitura.  
  
> [!NOTE]
>  O **ActiveConnection** propriedade é somente leitura para **registros** objetos cujo [fonte](../../../ado/reference/ado-api/source-property-ado-recordset.md) está definida como uma opção válida **comando** objeto, mesmo que o **registros** objeto não está aberto.  
  
 Se você passar um **comando** objeto o *fonte* argumento e também passar um *ActiveConnection* argumento, um erro ocorre. O **ActiveConnection** propriedade o **comando** objeto já deve ser definido como uma opção válida **Conexão** cadeia de caracteres de conexão ou objeto.  
  
 Se você passar algo diferente de um **comando** objeto o *fonte* argumento, você pode usar o *opções* argumento para otimizar a avaliação do *fonte*  argumento. Se o *opções* argumento não estiver definido, você pode enfrentar desempenho reduzido porque ADO deve fazer chamadas para o provedor para determinar se o argumento é uma instrução SQL, um procedimento armazenado, uma URL ou um nome de tabela. Se você souber o que *fonte* tipo você está usando, definindo o *opções* argumento instrui o ADO para ir diretamente para o código relevante. Se o *opções* argumento não coincide com o *fonte* digitar, ocorrerá um erro.  
  
 Se você passar um **fluxo** objeto o *fonte* argumento, você não deve transmitir informações para os outros argumentos. Isso irá gerar um erro. O **ActiveConnection** informações não são mantidos quando um **Recordset** é aberto a partir um **fluxo**.  
  
 O padrão para o *opções* argumento é **adCmdFile** se nenhuma conexão é associado a **registros**. Isso normalmente é o caso de maneira persistente armazenadas **registros** objetos.  
  
 Define se a fonte de dados não retorna nenhum registro, o provedor de [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propriedades **True**, e a posição do registro atual é indefinida. Você ainda pode adicionar novos dados nesse vazio **registros** permite se o tipo de cursor do objeto.  
  
 Quando você ter concluído suas operações em aberto **registros** de objeto, use o [fechar](../../../ado/reference/ado-api/close-method-ado.md) associados de método para liberar quaisquer recursos do sistema. Fechar um objeto não o remove da memória; Você pode alterar suas configurações de propriedade e usar o **abrir** método para abri-lo novamente mais tarde. Para eliminar completamente um objeto da memória, defina a variável de objeto para *nada*.  
  
 Antes do **ActiveConnection** estiver definida, chame **abrir** com nenhuma operandos para criar uma instância de um **registros** criado acrescentando campos para o  **Conjunto de registros** [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção.  
  
 Se você tiver configurado o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient**, você pode recuperar linhas de forma assíncrona em uma das duas maneiras. O método recomendado é definir *opções* para **adAsyncFetch**. Como alternativa, você pode usar a propriedade dinâmica "Processamento de conjunto de linhas assíncrono" no [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção, mas eventos recuperados relacionados podem ser perdidas se você não definir a *opções* parâmetro **adAsyncFetch**.  
  
> [!NOTE]
>  Busca de plano de fundo no provedor MS Remote é suportado somente com o **abrir** do método *opções* parâmetro.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Algumas combinações de [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) e [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valores não são válidos. Para obter informações sobre quais opções não podem ser combinadas, consulte os tópicos para a [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md), e [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo dos métodos de abertura e fechamento (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Exemplo dos métodos de abertura e fechamento (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Exemplo dos métodos de abertura e fechamento (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Salve e abra o exemplo de métodos (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Método Open (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (ADO registro)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (fluxo de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
