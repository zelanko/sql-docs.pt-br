---
title: "Usando as extensões do Visual C++ | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da6cd44f389b059a897ec464e1848cd9660b6c42
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="visual-c-extensions"></a>Extensões do Visual C++
## <a name="the-iadorecordbinding-interface"></a>A Interface IADORecordBinding
 O Microsoft Visual C++ Extensions para associar ADO ou ligação, campos de um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto para variáveis de C/C++. Sempre que a linha atual do que o limite **registros** for alterado, todos os campos associados no **Recordset** são copiados para as variáveis de C/C++. Se necessário, os dados copiados são convertidos para o tipo de dados declarado da variável C/C++.

 O **BindToRecordset** método o **IADORecordBinding** interface associa campos para variáveis de C/C++. O **AddNew** método adiciona uma nova linha ao limite **registros**. O **atualização** método preenche os campos em novas linhas do **registros**, ou atualiza campos em linhas existentes, com o valor das variáveis de C/C++.

 O **IADORecordBinding** interface é implementada pelo **registros** objeto. Você não codificar a implementação.

## <a name="binding-entries"></a>Entradas de vinculação
 As extensões do Visual C++ para ADO mapear campos de um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto para variáveis de C/C++. A definição de um mapeamento entre um campo e uma variável é chamada um *associação entrada*. Macros fornecem entradas de associação de dados numéricos, de comprimento fixo e comprimento variável. As entradas de associação e variáveis de C/C++ são declarados em uma classe derivada da classe de extensões do Visual C++, **CADORecordBinding**. O **CADORecordBinding** classe é definida internamente pelas macros de entrada de associação.

 ADO internamente mapeia os parâmetros nessas macros para OLE DB **DBBINDING** estrutura e cria um banco de dados OLE **acessador** objeto para gerenciar a movimentação e a conversão de dados entre variáveis e campos. OLE DB define dados como que consiste de três partes: um *buffer* onde os dados são armazenados; um *status* que indica se um campo com êxito foi armazenado em buffer, ou como a variável deve ser restaurada para o campo. e o *comprimento* dos dados. (Consulte [Obtendo e dados de configuração (OLE DB)](http://msdn.microsoft.com/en-us/4369708b-c9fb-4d48-a321-bf949b41a369)na referência do OLE DB do programador, para obter mais informações.)

## <a name="header-file"></a>Arquivo de cabeçalho
 Inclua o seguinte arquivo no seu aplicativo para usar as extensões do Visual C++ para ADO:

```
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>Campos de conjunto de registros de associação

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>Vincular campos de conjunto de registros a variáveis de C/C++

1.  Criar uma classe que deriva de **CADORecordBinding** classe.

2.  Especifique as entradas de associação e variáveis de C/C++ correspondentes na classe derivada. Colchete entradas de vinculação entre **BEGIN_ADO_BINDING** e **END_ADO_BINDING** macros. Não encerre as macros com vírgulas ou ponto e vírgula. Delimitadores apropriados são especificados automaticamente por cada macro.

     Especifique uma entrada de associação para cada campo a ser mapeada para uma variável de C/C++. Usar o membro apropriado do **ADO_FIXED_LENGTH_ENTRY**, **ADO_NUMERIC_ENTRY**, ou **ADO_VARIABLE_LENGTH_ENTRY** família de macros.

3.  Em seu aplicativo, crie uma instância da classe derivada de **CADORecordBinding**. Obter o **IADORecordBinding** de interface do **registros**. Em seguida, chame o **BindToRecordset** método para associar o **Recordset** campos para as variáveis de C/C++.

 Para obter mais informações, consulte o [exemplo de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md).

## <a name="interface-methods"></a>Métodos de interface
 O **IADORecordBinding** interface tem três métodos: **BindToRecordset**, **AddNew**, e **atualização**. O único argumento para cada método é um ponteiro para uma instância da classe derivada de **CADORecordBinding**. Portanto, o **AddNew** e **atualização** métodos não é possível especificar qualquer um dos parâmetros de seus namesakes de método do ADO.

## <a name="syntax"></a>Sintaxe
 O **BindToRecordset** método associa o **registros** campos com variáveis de C/C++.

```
BindToRecordset(CADORecordBinding *binding)
```

 O **AddNew** método invoca seu por homônimo ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método para adicionar uma nova linha para o **registros**.

```
AddNew(CADORecordBinding *binding)
```

 O **atualizar** método invoca seu por homônimo ADO [atualizar](../../../ado/reference/ado-api/update-method.md) método para atualizar o **registros**.

```
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>Macros de entrada de associação
 Macros de entrada de associação definem a associação de um **registros** campo e uma variável. Uma macro de início e fim delimita o conjunto de entradas de vinculação.

 Famílias de macros são fornecidas para os dados de comprimento fixo, como **adDate** ou **adBoolean**; numérico dados, tais como **adTinyInt**, **adInteger**, ou **adDouble**; e os dados de comprimento variável, como **adChar**, **adVarChar** ou **adVarBinary**. Todos os tipos numéricos, exceto para **adVarNumeric**, também são tipos de comprimento fixo. Cada família tem diferentes conjuntos de parâmetros para que você pode excluir as informações de associação não são de interesse.

 Para obter mais informações, consulte [tipos de dados do apêndice a:](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6), de referência do OLE DB do programador.

### <a name="begin-binding-entries"></a>Iniciar associação de entradas
 **BEGIN_ADO_BINDING**(*classe*)

### <a name="fixed-length-data"></a>Dados de comprimento fixo
 **ADO_FIXED_LENGTH_ENTRY**(*Ordinal, o tipo de dados, o Buffer, o Status de modificar*)

 **ADO_FIXED_LENGTH_ENTRY2**(*Ordinal, tipo de dados, Buffer, modificar*)

### <a name="numeric-data"></a>Dados numéricos
 **ADO_NUMERIC_ENTRY**(*Ordinal, tipo de dados, Buffer, precisão, escala, Status, modificar*)

 **ADO_NUMERIC_ENTRY2**(*Ordinal, o tipo de dados, o Buffer, precisão, escala, modificar*)

### <a name="variable-length-data"></a>Dados de comprimento variável
 **ADO_VARIABLE_LENGTH_ENTRY**(*Ordinal, tipo de dados, Buffer, tamanho, Status, comprimento, modificar*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*Ordinal, tipo de dados, Buffer, tamanho, Status, modificar*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*Ordinal, tipo de dados, Buffer, tamanho, comprimento, modificar*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*Ordinal, o tipo de dados, o Buffer, o tamanho, modificar*)

### <a name="end-binding-entries"></a>Entradas de associação de término
 **END_ADO_BINDING**)

|Parâmetro|Description|
|---------------|-----------------|
|*Classe*|Classe na qual as entradas de associação e variáveis de C/C++ são definidos.|
|*Ordinal*|Um número ordinal, contando a partir de um, do **registros** campo correspondente à sua variável de C/C++.|
|*Tipo de dados*|Tipo de dados ADO equivalente da variável C/C++ (consulte [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) para obter uma lista de tipos de dados válidos). O valor de **registros** campo será convertido para esse tipo de dados, se necessário.|
|*Buffer*|Nome da variável C/C++ em que o **registros** campo será armazenado.|
|*Tamanho*|Tamanho máximo em bytes do *Buffer*. Se *Buffer* conterá uma cadeia de caracteres de comprimento variável, espaço para um encerramento zero.|
|*Status*|Nome de uma variável que indica se o conteúdo de *Buffer* são válidos e se a conversão do campo a ser *DataType* foi bem-sucedida.<br /><br /> Os dois valores mais importantes para essa variável são **adFldOK**, que significa que a conversão foi bem sucedida; e **adFldNull**, que significa que o valor do campo deve ser uma VARIANTE do tipo VT_NULL e não simplesmente vazio.<br /><br /> Os valores possíveis para *Status* são listadas na tabela a seguir, "Valores de Status".|
|*Modificar*|Sinalizador booliano; Se for TRUE, indica o ADO tem permissão para atualizar o correspondente **registros** campo com o valor contido em *Buffer*.<br /><br /> Defina o booliano *modificar* parâmetro como TRUE para permitir que o ADO atualizar o campo associado e FALSE se você deseja examinar o campo, mas não alterá-lo.|
|*Precisão*|Número de dígitos que podem ser representados em uma variável numérica.|
|*Escala*|Número de casas decimais em uma variável numérica.|
|*Comprimento*|Nome de uma variável de quatro bytes que contém o comprimento real dos dados de *Buffer*.|

## <a name="status-values"></a>Valores de status
 O valor de *Status* variável indica se um campo foi copiado com êxito para uma variável.

 Ao definir os dados, *Status* pode ser definida como **adFldNull** para indicar o **registros** campo deve ser definido como null.

|Constante|Valor|Description|
|--------------|-----------|-----------------|
|**adFldOK**|0|Um valor de campo não-nulo foi retornado.|
|**adFldBadAccessor**|1|Associação era inválida.|
|**adFldCantConvertValue**|2|Valor não pôde ser convertido por razões diferentes de sinais incompatíveis ou dados de estouro.|
|**adFldNull**|3|Ao obter um campo, indica que um valor nulo foi retornado.<br /><br /> Ao definir um campo, indica que o campo deve ser definido como **nulo** quando o campo não é possível codificar **nulo** em si (por exemplo, uma matriz de caracteres ou um número inteiro).|
|**adFldTruncated**|4|Dígitos numéricos ou dados de comprimento variável foram truncados.|
|**adFldSignMismatch**|5|Valor é assinado e o tipo de dados da variável não está assinado.|
|**adFldDataOverFlow**|6|Valor é maior do que podem ser armazenados no tipo de dados da variável.|
|**adFldCantCreate**|7|Tipo de coluna desconhecido e o campo já está aberto.|
|**adFldUnavailable**|8|Não foi possível determinar o valor do campo — por exemplo, em um campo de novo, não atribuído sem nenhum valor padrão.|
|**adFldPermissionDenied**|9|Ao não atualizar, nenhuma permissão para gravar dados.|
|**adFldIntegrityViolation**|10|Durante a atualização, o valor do campo violaria integridade da coluna.|
|**adFldSchemaViolation**|11|Durante a atualização, o valor do campo violaria esquema da coluna.|
|**adFldBadStatus**|12|Ao atualizar o parâmetro de status inválido.|
|**adFldDefault**|13|Durante a atualização, um valor padrão foi usado.|

## <a name="see-also"></a>Consulte também
 [Exemplo de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) [cabeçalho de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)
