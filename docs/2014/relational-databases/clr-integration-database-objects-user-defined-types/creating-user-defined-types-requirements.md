---
title: Requisitos de tipo definido pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- UDTs [CLR integration], requirements
- serialization
- Native serialization format [CLR integration]
- attributes [CLR integration]
- XML serialization [CLR integration]
- user-defined types [CLR integration], requirements
- user-defined serialization [CLR integration]
- user-defined types [CLR integration], Native serialization
- UDTs [CLR integration], Native serialization
ms.assetid: bedc3372-50eb-40f2-bcf2-d6db6a63b7e6
caps.latest.revision: 31
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ff2d8987dee15e39a5f85e4efc01f0bdaef27e06
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350068"
---
# <a name="user-defined-type-requirements"></a>Requisitos do tipo definido pelo usuário
  Você deve tomar várias decisões de design importantes durante a criação de um tipo definido pelo usuário (UDT) a serem instalados em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De uma forma geral, é recomendável criar o UDT como uma estrutura, embora criá-lo como classe também seja uma opção. A definição do UDT precisa estar de acordo com as especificações para criação de UDTs para que seja registrado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="requirements-for-implementing-udts"></a>Requisitos para implementação de UDTs  
 Para ser executado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o UDT precisa implementar os seguintes requisitos na definição do UDT:  
  
 O UDT precisa especificar o `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute`. O uso do `System.SerializableAttribute` é opcional, porém recomendado.  
  
-   O UDT precisa implementar a interface `System.Data.SqlTypes.INullable` na classe ou estrutura criando um método `static` (`Shared` no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic) `Null`. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhece o valor nulo por padrão. Isso é necessário para que o código executado no UDT consiga reconhecer um valor nulo.  
  
-   O UDT precisa conter um método `static` (ou `Shared`) `Parse` público que dê suporte a análise e um método `ToString` público para converter em uma representação de cadeia de caracteres do objeto.  
  
-   Um UDT com formato de serialização definido pelo usuário precisa implementar a interface `System.Data.IBinarySerialize` e fornecer um método `Read` e um `Write`.  
  
-   O UDT precisa implementar `System.Xml.Serialization.IXmlSerializable`, ou todos os campos e propriedades públicos precisam ser de tipos que sejam serializáveis por XML ou decorados com o atributo `XmlIgnore` se for necessário substituir a serialização padrão.  
  
-   Deve haver apenas uma serialização de um objeto UDT. Haverá falha na validação se as rotinas de serialização ou desserialização reconhecerem mais de uma representação de um objeto específico.  
  
-   `SqlUserDefinedTypeAttribute.IsByteOrdered` deve ser `true` para comparar dados em ordem de byte. Se a interface IComparable não estiver implementada e `SqlUserDefinedTypeAttribute.IsByteOrdered` for `false`, as comparações de ordem de byte falharão.  
  
-   Um UDT definido em uma classe deve ter um construtor público que não leve argumentos. Você tem a opção de criar construtores de classe sobrecarregados adicionais.  
  
-   O UDT precisa expor elementos de dados como campos públicos ou procedimentos de propriedade.  
  
-   Nomes públicos não pode ter mais de 128 caracteres e deve estar de acordo com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regras de nomeação para identificadores conforme definido na [identificadores de banco de dados](../databases/database-identifiers.md).  
  
-   As colunas `sql_variant` não podem conter instâncias de um UDT.  
  
-   Os membros herdados não são acessíveis a partir do [!INCLUDE[tsql](../../includes/tsql-md.md)] porque o sistema de tipos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não reconhece a hierarquia de herança entre UDTs. Entretanto, você pode usar a herança ao estruturar suas classes, além de chamar esses métodos na implementação de código gerenciado do tipo.  
  
-   Os membros não podem ficar sobrecarregados, com exceção do construtor de classe. Se você criar um método sobrecarregado, nenhum erro ocorrerá quando você registrar o assembly ou criar o tipo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A detecção do método sobrecarregado ocorre em tempo de execução, e não quando o tipo é criado. Os métodos sobrecarregados podem existir na classe, contanto que nunca sejam invocados. Quando você invoca o método sobrecarregado, ocorre um erro.  
  
-   Quaisquer membros `static` (ou `Shared`) precisam ser declarados como constantes ou somente leitura. Membros estáticos não podem ser mutáveis.  
  
-   Se o campo `SqlUserDefinedTypeAttribute.MaxByteSize` for definido para -1, o UDT serial poderá ser tão grande quanto o limite de tamanho para objetos grandes (LOB) (atualmente 2 GB). O tamanho do UDT não pode ultrapassar o valor especificado no campo `MaxByteSized`.  
  
> [!NOTE]  
>  Apesar de ele não ser usado pelo servidor para executar comparações, você tem a opção de implementar a interface `System.IComparable`, que expõe um único método, o `CompareTo`. Isso é usado no lado do cliente em situações nas quais é desejável comparar ou ordenar valores UDT com precisão.  
  
## <a name="native-serialization"></a>Serialização nativa  
 A escolha dos atributos de serialização adequados para o UDT depende do tipo de UDT que você está tentando criar. O formato de serialização `Native` utiliza uma estrutura muito simples que permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazene uma representação nativa eficiente do UDT em disco. O formato `Native` será recomendado se o UDT for simples e contiver somente campos dos tipos a seguir:  
  
 **bool**, **byte**, **sbyte**, **short**, **ushort**, **int**, **uint**, **long**, **ulong**, **float**, **double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 Os tipos de valores compostos de campos dos tipos anteriores são ótimos candidatos ao formato `Native`, como `structs` no Visual C#, (ou `Structures` como são conhecidos no Visual Basic). Por exemplo, um UDT especificado com o formato de serialização `Native` pode conter um campo de outro UDT que também foi especificado com o formato `Native`. Se a definição de UDT for mais complexa e contiver tipos de dados na lista anterior, você precisará especificar o formato de serialização `UserDefined`.  
  
 O formato `Native` tem os requisitos a seguir:  
  
-   O tipo não deve especificar um valor para `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize`.  
  
-   Todos os campos precisam ser serializáveis.  
  
-   O `System.Runtime.InteropServices.StructLayoutAttribute` precisa ser especificado como `StructLayout.LayoutKindSequential` se o UDT for definido em uma classe, e não em uma estrutura. Esse atributo controla o layout físico dos campos de dados e é usado para obrigar os membros a ser dispostos na ordem em que aparecem. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa esse atributo para determinar a ordem dos campos para UDTs com vários valores.  
  
 Para obter um exemplo de um UDT definido com `Native` serialização, consulte o UDT Point em [Codificando tipos](creating-user-defined-types-coding.md).  
  
## <a name="userdefined-serialization"></a>Serialização UserDefined  
 A configuração do formato `UserDefined` para o atributo `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` proporciona ao desenvolvedor total controle do formato binário. Ao especificar a propriedade de atributo `Format` como `UserDefined`, você precisa seguir este procedimento no código:  
  
-   Especificar a propriedade de atributo `IsByteOrdered` opcional. O valor padrão é `false`.  
  
-   Especificar a propriedade `MaxByteSize` do `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute`.  
  
-   Escrever código para implementar os métodos `Read` e `Write` para o UDT implementando a interface `System.Data.Sql.IBinarySerialize`.  
  
 Para obter um exemplo de um UDT definido com `UserDefined` serialização, consulte o UDT Currency em [Codificando tipos](creating-user-defined-types-coding.md).  
  
> [!NOTE]  
>  Os campos UDT precisam usar serialização nativa ou serem persistidos para serem indexados.  
  
## <a name="serialization-attributes"></a>Atributos de serialização  
 Os atributos determinam como a serialização é usada para construir a representação de armazenamento de UDTs e transmiti-los por valor para o cliente. Você precisa especificar o `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` ao criar o UDT. O atributo `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` indica que a classe é um UDT e especifica o armazenamento para o UDT. Você tem a opção de especificar o atributo `Serializable`, apesar de que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não exige isso.  
  
 O `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` tem as propriedades a seguir.  
  
 `Format`  
 Especifica o formato de serialização, que pode ser `Native` ou `UserDefined`, dependendo dos tipos de dados do UDT.  
  
 `IsByteOrdered`  
 Um valor `Boolean` que determina como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa comparações binárias no UDT.  
  
 `IsFixedLength`  
 Indica se todas as instâncias desse UDT têm a mesma extensão.  
  
 `MaxByteSize`  
 O tamanho máximo da instância, em bytes. Você precisa especificar `MaxByteSize` com o formato de serialização `UserDefined`. Para um UDT com serialização definida pelo usuário especificada, `MaxByteSize` se refere ao tamanho total do UDT em sua forma serializada conforme definido pelo usuário. O valor de `MaxByteSize` precisa estar no intervalo de 1 a 8000 ou definido como -1 para indicar que o UDT tem tamanho maior do que 8000 bytes (o tamanho total não pode ultrapassar o tamanho de LOB máximo). Considere um UDT com a propriedade de uma cadeia de 10 caracteres (`System.Char`). Quando o UDT é serializado usando um BinaryWriter, o tamanho total da cadeia de caracteres serializada é de 22 bytes: 2 bytes por caractere Unicode UTF-16, multiplicados pelo número máximo de caracteres, mais 2 bytes de controle da sobrecarga ocasionada pela serialização de um fluxo binário. Portanto, ao determinar o valor de `MaxByteSize`, é necessário considerar o tamanho total do UDT serializado: o tamanho dos dados serializados em forma binária, mais a sobrecarga ocasionada pela serialização.  
  
 `ValidationMethodName`  
 O nome do método usado para validar instâncias do UDT.  
  
### <a name="setting-isbyteordered"></a>Definindo IsByteOrdered  
 Quando a propriedade `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered` é definida como `true`, você está garantindo que os dados binários serializados possam ser usados para ordenação semântica das informações. Assim, cada instância de um objeto UDT ordenado por byte pode ter somente uma representação serializada. Quando é executada uma operação de comparação no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos bytes serializados, os resultados devem ser os mesmos de quando a operação de comparação ocorre em código gerenciado. Os recursos a seguir também são suportados quando `IsByteOrdered` é definido como `true`:  
  
-   A capacidade de criar índices em colunas desse tipo.  
  
-   A capacidade de criar chaves primárias e estrangeiras, além de restrições CHECK e UNIQUE em colunas desse tipo.  
  
-   A capacidade de usar as cláusulas [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY e PARTITION BY. Nesses casos, a representação binária do tipo é usada para determinar a ordem.  
  
-   A capacidade de usar operadores de comparação em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   A capacidade de persistir colunas computadas desse tipo.  
  
 Observe que tanto o formato de serialização `Native` quanto o `UserDefined` suporta os seguintes operadores de comparação quando `IsByteOrdered` é definido como `true`:  
  
-   Igual a (=).  
  
-   Diferente de (!=)  
  
-   Maior que (>)  
  
-   Menor que (\<)  
  
-   Maior que ou igual a (>=)  
  
-   Menor que ou igual a (<=)  
  
### <a name="implementing-nullability"></a>Implementando a nulidade  
 Além de especificar corretamente os atributos dos assemblies, sua classe também precisa suportar a nulidade. Os UDTs carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhecem a nulidade, mas para que o UDT reconheça um valor nulo, a classe precisa implementar a interface `INullable`. Para obter mais informações e um exemplo de como implementar a nulidade em um UDT, consulte [Codificando tipos](creating-user-defined-types-coding.md).  
  
### <a name="string-conversions"></a>Conversões de cadeia de caracteres  
 Para suportar a conversão de cadeia de caracteres para o UDT e do UDT, você precisa fornecer um método `Parse` e um método `ToString` em sua classe. O método `Parse` permite converter uma cadeia de caracteres em uma UDT. Ele precisa ser declarado como `static` (ou `Shared` no Visual Basic) e usar um parâmetro do tipo `System.Data.SqlTypes.SqlString`. Para obter mais informações e um exemplo de como implementar o `Parse` e `ToString` métodos, consulte [Codificando tipos](creating-user-defined-types-coding.md).  
  
## <a name="xml-serialization"></a>Serialização XML  
 Os UDTs precisam suportar a conversão de e para o tipo de dados `xml` cumprindo o contrato para serialização XML. O namespace `System.Xml.Serialization` contém classes que são usadas para serializar objetos em documentos ou fluxos de formato XML. Você pode optar por implementar a serialização `xml` usando a interface `IXmlSerializable` que oferece formatação personalizada para serialização e desserialização XML.  
  
 Além de executar conversões explícitas de UDT para `xml`, a serialização XML permite:  
  
-   Usar `Xquery` sobre valores de instâncias de UDT após a conversão para o tipo de dados `xml`.  
  
-   Usar UDTs em consultas parametrizadas e métodos de Web com XML Web Services Nativos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usar UDTs para receber um carregamento em massa de dados XML.  
  
-   Serializar DataSets que contêm tabelas com colunas de UDT.  
  
 Os UDTs não são serializados em consultas FOR XML. Para executar uma consulta FOR XML que exibe a serialização XML dos UDTs, converta explicitamente cada coluna de UDT no tipo de dados `xml` da instrução SELECT. Você também pode converter explicitamente as colunas em `varbinary`, `varchar` ou `nvarchar`.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um tipo definido pelo usuário](creating-user-defined-types.md)  
  
  
