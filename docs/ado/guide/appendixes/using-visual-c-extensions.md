---
title: Usando extensões do Visual C++ | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 9f89b08d968b5f601c37f89b15196d6ef03db434
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702909"
---
# <a name="visual-c-extensions"></a>Extensões do Visual C++
## <a name="the-iadorecordbinding-interface"></a>A Interface IADORecordBinding
 O Microsoft Visual C++ Extensions para associar ADO ou bind, campos de um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto para variáveis de C/C++. Sempre que a linha atual do limite **conjunto de registros** for alterado, todos os campos associados na **Recordset** são copiados para as variáveis de C/C++. Se necessário, os dados copiados são convertidos para o tipo de dados declarado da variável C/C++.

 O **BindToRecordset** método o **IADORecordBinding** interface associa campos às variáveis de C/C++. O **AddNew** método adiciona uma nova linha ao limite **conjunto de registros**. O **atualização** método popula os campos em novas linhas da **conjunto de registros**, ou atualiza os campos em linhas existentes, com o valor das variáveis de C/C++.

 O **IADORecordBinding** interface é implementada pelo **Recordset** objeto. Você não codifique a implementação por conta própria.

## <a name="binding-entries"></a>Entradas de vinculação
 As extensões do Visual C++ para ADO mapear campos de um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto para variáveis de C/C++. A definição de um mapeamento entre um campo e uma variável é chamada um *associação de entrada*. Macros de fornecem entradas de associação para dados numéricos, de comprimento fixo e comprimento variável. As variáveis de C/C++ e entradas de vinculação são declaradas em uma classe derivada da classe de extensões do Visual C++, **CADORecordBinding**. O **CADORecordBinding** classe é definida internamente, as macros de entrada de associação.

 ADO internamente mapeia os parâmetros nessas macros para um banco de dados OLE **DBBINDING** estruturar e cria um banco de dados OLE **acessador** objeto para gerenciar a movimentação e a conversão de dados entre variáveis e campos. OLE DB define dados como que consiste de três partes: Um *buffer* onde os dados são armazenados; um *status* que indica se um campo foi armazenado com êxito no buffer ou como a variável deve ser restaurada para o campo; e o *comprimento* dos dados. (Consulte [dados de configuração (OLE DB) e Obtendo](https://msdn.microsoft.com/4369708b-c9fb-4d48-a321-bf949b41a369)na referência do OLE DB do programador, para obter mais informações.)

## <a name="header-file"></a>Arquivo de cabeçalho
 Inclua o seguinte arquivo em seu aplicativo para usar as extensões do Visual C++ para ADO:

```cpp
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>Campos de conjunto de registros de associação

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>Para associar campos de conjunto de registros a variáveis de C/C++

1.  Criar uma classe que deriva de **CADORecordBinding** classe.

2.  Especifique as entradas de associação e variáveis de C/C++ correspondentes na classe derivada. Entradas de vinculação entre de colchete **BEGIN_ADO_BINDING** e **END_ADO_BINDING** macros. Não encerre as macros com vírgulas ou ponto e vírgula. Delimitadores apropriados são especificados automaticamente por cada macro.

     Especifique uma entrada de associação para cada campo a ser mapeada para uma variável de C/C++. Use o membro apropriado dos **ADO_FIXED_LENGTH_ENTRY**, **ADO_NUMERIC_ENTRY**, ou **ADO_VARIABLE_LENGTH_ENTRY** família das macros.

3.  Em seu aplicativo, crie uma instância da classe derivada **CADORecordBinding**. Obter o **IADORecordBinding** da interface da **conjunto de registros**. Em seguida, chame o **BindToRecordset** método para associar a **Recordset** campos para as variáveis de C/C++.

 Para obter mais informações, consulte o [exemplo de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md).

## <a name="interface-methods"></a>Métodos de interface
 O **IADORecordBinding** interface possui três métodos: **BindToRecordset**, **AddNew**, e **atualização**. O único argumento para cada método é um ponteiro para uma instância da classe derivada **CADORecordBinding**. Portanto, o **AddNew** e **atualização** métodos não é possível especificar qualquer um dos parâmetros de seus namesakes de método do ADO.

## <a name="syntax"></a>Sintaxe
 O **BindToRecordset** método associa a **Recordset** campos com variáveis de C/C++.

```cpp
BindToRecordset(CADORecordBinding *binding)
```

 O **AddNew** método invoca seu nome em inglês sugere, o ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método para adicionar uma nova linha para o **conjunto de registros**.

```cpp
AddNew(CADORecordBinding *binding)
```

 O **atualize** método invoca seu nome em inglês sugere, o ADO [atualizar](../../../ado/reference/ado-api/update-method.md) método para atualizar o **conjunto de registros**.

```cpp
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>Macros de entrada de associação
 Macros de entrada de associação definem a associação de um **Recordset** campo e uma variável. Uma macro de início e fim delimita o conjunto de entradas de vinculação.

 Famílias de macros são fornecidas para os dados de comprimento fixo, como **adDate** ou **adBoolean**; numérico dados, como **adTinyInt**, **adInteger**, ou **adDouble**; e os dados de comprimento variável, como **adChar**, **adVarChar** ou **adVarBinary**. Todos os tipos numéricos, exceto para **adVarNumeric**, também são tipos de comprimento fixo. Cada família tem diferentes conjuntos de parâmetros para que você pode excluir as informações de associação não são de interesse.

 Para obter mais informações, consulte [apêndice a: Tipos de dados](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6), de referência do programador do OLE DB.

### <a name="begin-binding-entries"></a>Iniciar associação de entradas
 **BEGIN_ADO_BINDING**(*Class*)

### <a name="fixed-length-data"></a>Dados de comprimento fixo
 **ADO_FIXED_LENGTH_ENTRY**(*Ordinal, DataType, Buffer, Status, Modify*)

 **ADO_FIXED_LENGTH_ENTRY2**(*Ordinal, DataType, Buffer, Modify*)

### <a name="numeric-data"></a>Dados numéricos
 **ADO_NUMERIC_ENTRY**(*Ordinal, DataType, Buffer, Precision, Scale, Status, Modify*)

 **ADO_NUMERIC_ENTRY2**(*Ordinal, DataType, Buffer, Precision, Scale, Modify*)

### <a name="variable-length-data"></a>Dados de comprimento variável
 **ADO_VARIABLE_LENGTH_ENTRY**(*Ordinal, DataType, Buffer, Size, Status, Length, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*Ordinal, DataType, Buffer, Size, Status, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*Ordinal, DataType, Buffer, Size, Length, Modify*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*Ordinal, DataType, Buffer, Size, Modify*)

### <a name="end-binding-entries"></a>Entradas de associação de término
 **END_ADO_BINDING**()

|Parâmetro|Descrição|
|---------------|-----------------|
|*Classe*|Classe na qual as variáveis de C/C++ e entradas de vinculação são definidas.|
|*Ordinal*|Número ordinal, contando a partir de um, do **Recordset** campo correspondente à sua variável de C/C++.|
|*DataType*|Tipo de dados ADO equivalente da variável C/C++ (consulte [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) para obter uma lista de tipos de dados válidos). O valor de **conjunto de registros** campo será convertido para esse tipo de dados, se necessário.|
|*buffer*|Nome da variável C/C++ no qual o **Recordset** campo será armazenado.|
|*Tamanho*|Tamanho máximo em bytes do *Buffer*. Se *Buffer* conterá uma cadeia de caracteres de comprimento variável, fazer espaço para um terminação de zero.|
|*Status*|Nome de uma variável que indicará se o conteúdo do *Buffer* são válidos e se a conversão do campo a ser *DataType* foi bem-sucedida.<br /><br /> Os dois valores mais importantes para essa variável forem **adFldOK**, que significa que a conversão foi bem-sucedida; e **adFldNull**, que significa que o valor do campo seria uma VARIANTE do tipo VT_NULL e não simplesmente vazio.<br /><br /> Os valores possíveis para *Status* são listadas na tabela a seguir, "Valores de Status".|
|*Modificar*|Sinalizador booliano; Se for TRUE, indica o ADO tem permissão para atualizar o correspondente **conjunto de registros** campo com o valor contido no *Buffer*.<br /><br /> Defina o booliano *modificar* parâmetro como TRUE para permitir que o ADO atualizar o campo associado e FALSE se você quiser examinar o campo, mas não alterá-lo.|
|*Precisão*|Número de dígitos que podem ser representados em uma variável numérica.|
|*Escala*|Número de casas decimais em uma variável numérica.|
|*Comprimento*|Nome de uma variável de quatro bytes que contém o comprimento real dos dados no *Buffer*.|

## <a name="status-values"></a>Valores de status
 O valor de *Status* variável indica se um campo foi copiado com êxito a uma variável.

 Ao definir os dados, *Status* pode ser definido como **adFldNull** para indicar o **Recordset** campo deve ser definido como null.

|Constante|Valor|Descrição|
|--------------|-----------|-----------------|
|**adFldOK**|0|Um valor de campo de não-nulo foi retornado.|
|**adFldBadAccessor**|1|Associação era inválida.|
|**adFldCantConvertValue**|2|Valor não pôde ser convertido por razões diferentes de estouro de dados ou de incompatibilidade de sinal.|
|**adFldNull**|3|Ao obter um campo, indica que um valor nulo foi retornado.<br /><br /> Ao definir um campo, indica que o campo deve ser definido como **nulo** quando o campo não é possível codificar **nulo** em si (por exemplo, uma matriz de caracteres ou um número inteiro).|
|**adFldTruncated**|4|Dígitos numéricos ou dados de comprimento variável foram truncados.|
|**adFldSignMismatch**|5|Valor é assinado e o tipo de dados da variável não estiver assinado.|
|**adFldDataOverFlow**|6|Valor é maior do que podem ser armazenados no tipo de dados da variável.|
|**adFldCantCreate**|7|Tipo de coluna desconhecido e o campo já está aberto.|
|**adFldUnavailable**|8|Valor do campo não pôde ser determinado-por exemplo, em um campo de novo e não atribuído sem nenhum valor padrão.|
|**adFldPermissionDenied**|9|Ao atualizar, sem permissão para gravar dados.|
|**adFldIntegrityViolation**|10|Durante a atualização, o valor do campo violaria integridade da coluna.|
|**adFldSchemaViolation**|11|Durante a atualização, o valor do campo violaria o esquema de coluna.|
|**adFldBadStatus**|12|Ao atualizar o parâmetro de status inválido.|
|**adFldDefault**|13|Durante a atualização, um valor padrão foi usado.|

## <a name="see-also"></a>Consulte também
 [Exemplo de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) [cabeçalho de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)
