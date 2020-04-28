---
title: Usando extensões de Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a9d60695bd033bfc83e3a091490f27f9432782c0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926458"
---
# <a name="visual-c-extensions"></a>Extensões de Visual C++
## <a name="the-iadorecordbinding-interface"></a>A interface IADORecordBinding
 As extensões de Microsoft Visual C++ para ADO associado ou associam campos de um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) a variáveis C/C++. Sempre que a linha atual do **conjunto de registros** associado for alterada, todos os campos associados no **conjunto de registros** serão copiados para as variáveis C/C++. Se necessário, os dados copiados são convertidos no tipo de dados declarado da variável C/C++.

 O método **BindToRecordset** da interface **IADORecordBinding** associa campos a variáveis C/C++. O método **AddNew** adiciona uma nova linha ao conjunto de **registros**associado. O método **Update** popula campos em novas linhas do conjunto de **registros**ou atualiza campos em linhas existentes, com o valor das variáveis C/C++.

 A interface **IADORecordBinding** é implementada pelo objeto **Recordset** . Você não codifica a implementação por conta própria.

## <a name="binding-entries"></a>Entradas de associação
 As extensões de Visual C++ para campos de mapa ADO de um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para as variáveis C/C++. A definição de um mapeamento entre um campo e uma variável é chamada de *entrada de associação*. As macros fornecem entradas de associação para dados numéricos, de comprimento fixo e de comprimento variável. As entradas de associação e as variáveis C/C++ são declaradas em uma classe derivada da classe de extensões de Visual C++, **CADORecordBinding**. A classe **CADORecordBinding** é definida internamente pelas macros de entrada de associação.

 O ADO mapeia internamente os parâmetros dessas macros para uma estrutura OLE DB **DBBINDING** e cria um objeto **acessador** de OLE DB para gerenciar a movimentação e a conversão de dados entre campos e variáveis. OLE DB define os dados como consistentes em três partes: um *buffer* onde os dados são armazenados; um *status* que indica se um campo foi armazenado com êxito no buffer ou como a variável deve ser restaurada para o campo; e o *comprimento* dos dados. (Consulte [obter e definir dados (OLE DB)](https://msdn.microsoft.com/4369708b-c9fb-4d48-a321-bf949b41a369)na referência do programador de OLE DB, para obter mais informações.)

## <a name="header-file"></a>Arquivos de cabeçalho
 Inclua o seguinte arquivo em seu aplicativo para usar as extensões de Visual C++ para ADO:

```cpp
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>Ligando campos do conjunto de registros

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>Para associar campos do conjunto de registros a variáveis C/C++

1.  Crie uma classe derivada da classe **CADORecordBinding** .

2.  Especifique entradas de associação e variáveis do C/C++ correspondentes na classe derivada. Colchetes das entradas de associação entre **BEGIN_ADO_BINDING** e **END_ADO_BINDING** macros. Não encerre as macros com vírgulas ou ponto-e-vírgula. Os delimitadores apropriados são especificados automaticamente por cada macro.

     Especifique uma entrada de associação para cada campo a ser mapeado para uma variável C/C++. Use um membro apropriado da família de macros **ADO_FIXED_LENGTH_ENTRY**, **ADO_NUMERIC_ENTRY**ou **ADO_VARIABLE_LENGTH_ENTRY** .

3.  Em seu aplicativo, crie uma instância da classe derivada de **CADORecordBinding**. Obtenha a interface **IADORecordBinding** do **conjunto de registros**. Em seguida, chame o método **BindToRecordset** para associar os campos do **conjunto de registros** às variáveis C/C++.

 Para obter mais informações, consulte o [exemplo de extensões de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md).

## <a name="interface-methods"></a>Métodos de interface
 A interface **IADORecordBinding** tem três métodos: **BindToRecordset**, **AddNew**e **Update**. O único argumento para cada método é um ponteiro para uma instância da classe derivada de **CADORecordBinding**. Portanto, os métodos **AddNew** e **Update** não podem especificar nenhum dos parâmetros de seu método ADO namesakes.

## <a name="syntax"></a>Sintaxe
 O método **BindToRecordset** associa os campos do **conjunto de registros** às variáveis C/C++.

```cpp
BindToRecordset(CADORecordBinding *binding)
```

 O método **AddNew** invoca seu nome, o método ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) , para adicionar uma nova linha ao conjunto de **registros**.

```cpp
AddNew(CADORecordBinding *binding)
```

 O método **Update** invoca seu nome, o método [Update](../../../ado/reference/ado-api/update-method.md) do ADO, para atualizar o **conjunto de registros**.

```cpp
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>Macros de entrada de associação
 As macros de entrada de associação definem a associação de um campo de **conjunto de registros** e uma variável. Uma macro inicial e final delimita o conjunto de entradas de associação.

 Famílias de macros são fornecidas para dados de comprimento fixo, como **adDate** ou **adBoolean**; dados numéricos, como **adTinyInt**, **adInteger**ou **adDouble**; e dados de comprimento variável, como **adChar**, **adVarChar** ou **adVarBinary**. Todos os tipos numéricos, exceto para **adVarNumeric**, também são tipos de comprimento fixo. Cada família tem conjuntos de parâmetros diferentes para que você possa excluir informações de associação sem interesse.

 Para obter mais informações, consulte o [Apêndice a: tipos de dados](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6), da referência do programador de OLE DB.

### <a name="begin-binding-entries"></a>Iniciar entradas de associação
 **BEGIN_ADO_BINDING**(*Class*)

### <a name="fixed-length-data"></a>Dados de comprimento fixo
 **ADO_FIXED_LENGTH_ENTRY**(*ordinal, DataType, buffer, status, modificar*)

 **ADO_FIXED_LENGTH_ENTRY2**(*Ordinal, DataType, Buffer, Modify*)

### <a name="numeric-data"></a>Dados numéricos
 **ADO_NUMERIC_ENTRY**(*ordinal, DataType, buffer, precisão, escala, status, modificar*)

 **ADO_NUMERIC_ENTRY2**(*ordinal, DataType, buffer, precisão, escala, modificar*)

### <a name="variable-length-data"></a>Dados de comprimento variável
 **ADO_VARIABLE_LENGTH_ENTRY**(*Ordinal, DataType, Buffer, Size, Status, Length, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*Ordinal, DataType, Buffer, Size, Status, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*Ordinal, DataType, Buffer, Size, Length, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*Ordinal, DataType, Buffer, Size, Modify*)

### <a name="end-binding-entries"></a>Encerrar entradas de associação
 **END_ADO_BINDING**()

|Parâmetro|Descrição|
|---------------|-----------------|
|*Classe*|Classe na qual as entradas de associação e as variáveis C/C++ são definidas.|
|*Ordinal*|Número ordinal, contando de um, do campo **conjunto de registros** correspondente à sua variável C/C++.|
|*DataType*|Tipo de dados ADO equivalente da variável C/C++ (consulte [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) para obter uma lista de tipos de dados válidos). O valor do campo **conjunto de registros** será convertido nesse tipo de dados, se necessário.|
|*Completo*|Nome da variável C/C++ em que o campo do **conjunto de registros** será armazenado.|
|*Tamanho*|Tamanho máximo em bytes de *buffer*. Se o *buffer* contiver uma cadeia de caracteres de comprimento variável, deixe espaço para um zero de terminação.|
|*Status*|Nome de uma variável que indicará se o conteúdo do *buffer* é válido e se a conversão do campo em *DataType* foi bem-sucedida.<br /><br /> Os dois valores mais importantes para essa variável são **adFldOK**, o que significa que a conversão foi bem-sucedida; e **adFldNull**, o que significa que o valor do campo seria uma variante do tipo VT_NULL e não apenas vazio.<br /><br /> Os valores possíveis para *status* são listados na tabela a seguir, "valores de status".|
|*Modificar*|Sinalizador booliano; Se for TRUE, indicará que o ADO tem permissão para atualizar o campo **Recordset** correspondente com o valor contido no *buffer*.<br /><br /> Defina o parâmetro de *modificação* booliana como true para habilitar o ADO para atualizar o campo associado e false se você quiser examinar o campo, mas não alterá-lo.|
|*Precisão*|Número de dígitos que podem ser representados em uma variável numérica.|
|*Escala*|Número de casas decimais em uma variável numérica.|
|*Comprimento*|Nome de uma variável de quatro bytes que conterá o comprimento real dos dados no *buffer*.|

## <a name="status-values"></a>Valores de status
 O valor da variável *status* indica se um campo foi copiado com êxito para uma variável.

 Ao definir dados, o *status* pode ser definido como **adFldNull** para indicar que o campo do **conjunto de registros** deve ser definido como nulo.

|Constante|Valor|Descrição|
|--------------|-----------|-----------------|
|**adFldOK**|0|Um valor de campo não nulo foi retornado.|
|**adFldBadAccessor**|1|A associação era inválida.|
|**adFldCantConvertValue**|2|Não foi possível converter o valor por razões diferentes de incompatibilidade de sinal ou estouro de dados.|
|**adFldNull**|3|Ao obter um campo, indica que um valor nulo foi retornado.<br /><br /> Ao definir um campo, indica que o campo deve ser definido como **nulo** quando o campo não pode codificar o **valor nulo** (por exemplo, uma matriz de caracteres ou um número inteiro).|
|**adFldTruncated**|4|Os dados de comprimento variável ou os dígitos numéricos foram truncados.|
|**adFldSignMismatch**|5|O valor é assinado e o tipo de dados variable não está assinado.|
|**adFldDataOverFlow**|6|O valor é maior do que o pode ser armazenado no tipo de dados Variable.|
|**adFldCantCreate**|7|Tipo de coluna e campo desconhecido já aberto.|
|**adFldUnavailable**|8|O valor do campo não pôde ser determinado-por exemplo, em um campo novo e não atribuído sem valor padrão.|
|**adFldPermissionDenied**|9|Ao atualizar, não há permissão para gravar dados.|
|**adFldIntegrityViolation**|10|Ao atualizar, o valor do campo viola a integridade da coluna.|
|**adFldSchemaViolation**|11|Ao atualizar, o valor do campo violaria o esquema da coluna.|
|**adFldBadStatus**|12|Ao atualizar, parâmetro de status inválido.|
|**adFldDefault**|13|Ao atualizar, um valor padrão foi usado.|

## <a name="see-also"></a>Consulte Também
 [Exemplo de extensões de Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual C++ cabeçalho de extensões](../../../ado/guide/appendixes/visual-c-extensions-header.md)
