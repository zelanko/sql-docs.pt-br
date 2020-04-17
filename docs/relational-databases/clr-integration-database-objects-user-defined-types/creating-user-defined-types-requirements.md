---
title: Requisitos de tipo definidos pelo usuário | Microsoft Docs
description: Este artigo descreve decisões importantes de design que você precisa tomar ao criar um UDT para instalar no SQL Server.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2b19a9179cba2225a2209255ce48220669e4bbef
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486963"
---
# <a name="creating-user-defined-types---requirements"></a>Criar tipos definidos pelo usuário – Requisitos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você deve tomar várias decisões importantes de design ao criar um tipo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]definido pelo usuário (UDT) a ser instalado em . De uma forma geral, é recomendável criar o UDT como uma estrutura, embora criá-lo como classe também seja uma opção. A definição do UDT precisa estar de acordo com as especificações para criação de UDTs para que seja registrado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="requirements-for-implementing-udts"></a>Requisitos para implementação de UDTs  
 Para ser executado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o UDT precisa implementar os seguintes requisitos na definição do UDT:  
  
 O UDT deve especificar o **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**. O uso do **System.SerializableAttribute** é opcional, mas recomendado.  
  
-   O UDT deve implementar a interface **System.Data.SqlTypes.INullable** na classe ou estrutura, criando um método **público estático** **(Compartilhado** no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic) **Null.** O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhece o valor nulo por padrão. Isso é necessário para que o código executado no UDT consiga reconhecer um valor nulo.  
  
-   O UDT deve conter um método público de **análise** **estática** (ou **compartilhado)** que suporte a análise e um método **tostring** público para converter em uma representação de string do objeto.  
  
-   Um UDT com um formato de serialização definido pelo usuário deve implementar a interface **System.Data.IBinarySerialize** e fornecer um **método** **De Leitura** e Gravação.  
  
-   O UDT deve implementar **o System.Xml.Serialization.IXmlSerializable**, ou todos os campos e propriedades públicas devem ser de tipos que são seriadificáveis ou decorados com o atributo **XmlIgnore** se a serialização padrão de substituição for necessária.  
  
-   Deve haver apenas uma serialização de um objeto UDT. Haverá falha na validação se as rotinas de serialização ou desserialização reconhecerem mais de uma representação de um objeto específico.  
  
-   **SqlUserDefinedTypeAttribute.IsByteOrdered** deve ser **verdadeiro** para comparar dados na ordem byte. Se a interface IComparável não for implementada e **SqlUserDefinedTypeAttribute.IsByteOrdered** for **falsa,** as comparações de pedidos de byte falharão.  
  
-   Um UDT definido em uma classe deve ter um construtor público que não leve argumentos. Você tem a opção de criar construtores de classe sobrecarregados adicionais.  
  
-   O UDT precisa expor elementos de dados como campos públicos ou procedimentos de propriedade.  
  
-   Os nomes públicos não podem ter mais de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 128 caracteres e devem estar em conformidade com as regras de nomeação para identificadores definidos em [Identificadores de Banco de Dados](../../relational-databases/databases/database-identifiers.md).  
  
-   **sql_variant** colunas não podem conter instâncias de um UDT.  
  
-   Os membros herdados não são acessíveis a partir do [!INCLUDE[tsql](../../includes/tsql-md.md)] porque o sistema de tipos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não reconhece a hierarquia de herança entre UDTs. Entretanto, você pode usar a herança ao estruturar suas classes, além de chamar esses métodos na implementação de código gerenciado do tipo.  
  
-   Os membros não podem ficar sobrecarregados, com exceção do construtor de classe. Se você criar um método sobrecarregado, nenhum erro ocorrerá quando você registrar o assembly ou criar o tipo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A detecção do método sobrecarregado ocorre em tempo de execução, e não quando o tipo é criado. Os métodos sobrecarregados podem existir na classe, contanto que nunca sejam invocados. Quando você invoca o método sobrecarregado, ocorre um erro.  
  
-   Todos os membros **estáticos** (ou **compartilhados)** devem ser declarados como constantes ou apenas como leitura. Membros estáticos não podem ser mutáveis.  
  
-   Se o campo **SqlUserDefinedTypeAttribute.MaxByteSize** estiver definido como -1, o UDT serializado pode ser tão grande quanto o limite de tamanho do objeto grande (LOB) (atualmente 2 GB). O tamanho do UDT não pode exceder o valor especificado no campo **MaxByteSized.**  
  
> [!NOTE]  
>  Embora não seja usado pelo servidor para realizar comparações, você pode opcionalmente implementar a interface **System.IComparável,** que expõe um único método, **CompareTo**. Isso é usado no lado do cliente em situações nas quais é desejável comparar ou ordenar valores UDT com precisão.  
  
## <a name="native-serialization"></a>Serialização nativa  
 A escolha dos atributos de serialização adequados para o UDT depende do tipo de UDT que você está tentando criar. O formato de serialização **Nativo** utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma estrutura muito simples que permite armazenar uma representação nativa eficiente do UDT em disco. O formato **Nativo** é recomendado se o UDT for simples e contiver apenas campos dos seguintes tipos:  
  
 **bool**, **byte**, **sbyte**, **short**, **ushort**, **int**, **uint**, **long**, **ulong**, **float**, **double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 Os tipos de valor que são compostos por campos dos tipos acima são bons candidatos para o formato **nativo,** como estruturas em Visual C#, (ou **Estruturas** como são **conhecidas** no Visual Basic). Por exemplo, um UDT especificado com o formato de serialização **Nativo** pode conter um campo de outro UDT que também foi especificado com o formato **Nativo.** Se a definição de UDT for mais complexa e contiver tipos de dados que não estão na lista acima, você deve especificar o formato de serialização **UserDefined.**  
  
 O formato **Nativo** tem os seguintes requisitos:  
  
-   O tipo não deve especificar um valor para **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**.  
  
-   Todos os campos precisam ser serializáveis.  
  
-   O **System.Runtime.InteropServices.StructLayoutAttribute** deve ser especificado como **StructLayout.LayoutKindSequential** se o UDT for definido em uma classe e não em uma estrutura. Esse atributo controla o layout físico dos campos de dados e é usado para obrigar os membros a ser dispostos na ordem em que aparecem. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa esse atributo para determinar a ordem dos campos para UDTs com vários valores.  
  
 Para um exemplo de um UDT definido com serialização **nativa,** consulte o Ponto UDT em [Tipos definidos pelo usuário de codificação](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="userdefined-serialization"></a>Serialização UserDefined  
 A configuração de formato **'UsuárioDefinido** para o **microsoft.SqlServer.Server.Server.SqlUserDefinedTypeAttribute'** dá ao desenvolvedor controle total sobre o formato binário. Ao especificar a propriedade de atributo **Formato** como **UsuárioDefinido,** você deve fazer o seguinte em seu código:  
  
-   Especifique a propriedade de atributo **isbyteOrdered** opcional. O valor padrão é **false**.  
  
-   Especifique a propriedade **MaxByteSize** do **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**.  
  
-   Escreva código para implementar métodos **de Leitura** e **Gravação** para o UDT implementando a interface **System.Data.Sql.IBinarySerialize.**  
  
 Para um exemplo de um UDT definido com serialização **do UsuárioDefinido,** consulte o UDT de moeda em [tipos definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md)de codificação .  
  
> [!NOTE]  
>  Os campos UDT precisam usar serialização nativa ou serem persistidos para serem indexados.  
  
## <a name="serialization-attributes"></a>Atributos de serialização  
 Os atributos determinam como a serialização é usada para construir a representação de armazenamento de UDTs e transmiti-los por valor para o cliente. Você é obrigado a especificar o **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** ao criar o UDT. O atributo **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** indica que a classe é um UDT e especifica o armazenamento para o UDT. Você pode especificar opcionalmente o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **atributo Serializable,** embora não exija isso.  
  
 O **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** tem as seguintes propriedades.  
  
 **Formatar**  
 Especifica o formato de serialização, que pode ser **Nativo** ou **UsuárioDefinido,** dependendo dos tipos de dados do UDT.  
  
 **IsByteOrdered**  
 Um valor **booleano** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que determina como realiza comparações binárias no UDT.  
  
 **IsFixedLength**  
 Indica se todas as instâncias desse UDT têm a mesma extensão.  
  
 **MaxByteSize**  
 O tamanho máximo da instância, em bytes. Você deve especificar **MaxByteSize** com o formato de serialização **UserDefined.** Para um UDT com serialização definida pelo usuário especificada, **MaxByteSize** refere-se ao tamanho total do UDT em sua forma serializada, conforme definido pelo usuário. O valor de **MaxByteSize** deve estar na faixa de 1 a 8000, ou definido como -1 para indicar que o UDT é maior que 8000 bytes (o tamanho total não pode exceder o tamanho máximo do LOB). Considere um UDT com uma propriedade de uma seqüência de 10 caracteres **(System.Char**). Quando o UDT é serializado usando um BinaryWriter, o tamanho total da cadeia de caracteres serializada é de 22 bytes: 2 bytes por caractere Unicode UTF-16, multiplicados pelo número máximo de caracteres, mais 2 bytes de controle da sobrecarga ocasionada pela serialização de um fluxo binário. Portanto, ao determinar o valor do **MaxByteSize,** o tamanho total do UDT serializado deve ser considerado: o tamanho dos dados serializados em forma binária mais a sobrecarga incorrida pela serialização.  
  
 **ValidationMethodName**  
 O nome do método usado para validar instâncias do UDT.  
  
### <a name="setting-isbyteordered"></a>Definindo IsByteOrdered  
 Quando a propriedade **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered** é definida como **true,** você está de fato garantindo que os dados binários serializados possam ser usados para o pedido semântico das informações. Assim, cada instância de um objeto UDT ordenado por byte pode ter somente uma representação serializada. Quando é executada uma operação de comparação no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos bytes serializados, os resultados devem ser os mesmos de quando a operação de comparação ocorre em código gerenciado. Os seguintes recursos também são suportados quando **o IsByteOrdered** é definido como **true**:  
  
-   A capacidade de criar índices em colunas desse tipo.  
  
-   A capacidade de criar chaves primárias e estrangeiras, além de restrições CHECK e UNIQUE em colunas desse tipo.  
  
-   A capacidade de usar as cláusulas [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY e PARTITION BY. Nesses casos, a representação binária do tipo é usada para determinar a ordem.  
  
-   A capacidade de usar operadores de comparação em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   A capacidade de persistir colunas computadas desse tipo.  
  
 Observe que os formatos **de** serialização Nativo e **UsuárioDefinido** suportam os seguintes operadores de comparação quando **o IsByteOrdered** é definido **como true**:  
  
-   Igual a (=).  
  
-   Diferente de (!=)  
  
-   Maior que (>)  
  
-   Menor que (\<)  
  
-   Maior que ou igual a (>=)  
  
-   Menor que ou igual a (<=)  
  
### <a name="implementing-nullability"></a>Implementando a nulidade  
 Além de especificar corretamente os atributos dos assemblies, sua classe também precisa suportar a nulidade. Os UDTs [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carregados são de reconhecimento nulo, mas para que o UDT reconheça um valor nulo, a classe deve implementar a interface **INullable.** Para obter mais informações e um exemplo de como implementar a nulidade em um UDT, consulte [Codificação de Tipos Definidos pelo Usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
### <a name="string-conversions"></a>Conversões de cadeia de caracteres  
 Para suportar a conversão de strings para e a partir do UDT, você deve fornecer um método **Parse** e um método **ToString** em sua classe. O método **Parse** permite que uma string seja convertida em um UDT. Deve ser declarado como **estático** (ou **compartilhado** no Visual Basic), e tomar um parâmetro do tipo **System.Data.SqlTypes.SqlString**. Para obter mais informações e um exemplo de como implementar os métodos **Parse** e **ToString,** consulte [Tipos definidos pelo usuário de codificação](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="xml-serialization"></a>Serialização XML  
 Os UDTs devem suportar a conversão de e para o tipo de dados **xml,** conforme o contrato de serialização XML. O **namespace System.Xml.Serialization** contém classes usadas para serializar objetos em documentos ou fluxos de formato XML. Você pode optar por implementar a serialização **xml** usando a interface **IXmlSerializable,** que fornece formatação personalizada para serialização e desserialização xml.  
  
 Além de realizar conversões explícitas de UDT para **xml,** a serialização XML permite:  
  
-   Use **Xquery** sobre valores de instâncias UDT após a conversão para o tipo de dados **xml.**  
  
-   Usar UDTs em consultas parametrizadas e métodos de Web com XML Web Services Nativos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usar UDTs para receber um carregamento em massa de dados XML.  
  
-   Serializar DataSets que contêm tabelas com colunas de UDT.  
  
 Os UDTs não são serializados em consultas FOR XML. Para executar uma consulta FOR XML que exibe a serialização XML de UDTs, converta explicitamente cada coluna UDT para o tipo de dados **xML** na instrução SELECT. Você também pode converter explicitamente as colunas em **varbinary,** **varchar**ou **nvarchar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
