---
title: Requisitos de tipo definidos pelo usuário | Microsoft Docs
description: Este artigo descreve as decisões de design importantes que você precisa fazer ao criar um UDT para instalar o em SQL Server.
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
ms.openlocfilehash: b20192a3804dfba713b04706d528738ceb8768c3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727813"
---
# <a name="creating-user-defined-types---requirements"></a>Criar tipos definidos pelo usuário – Requisitos
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Você deve fazer várias decisões de design importantes ao criar um UDT (tipo definido pelo usuário) a ser instalado no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . De uma forma geral, é recomendável criar o UDT como uma estrutura, embora criá-lo como classe também seja uma opção. A definição do UDT precisa estar de acordo com as especificações para criação de UDTs para que seja registrado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="requirements-for-implementing-udts"></a>Requisitos para implementação de UDTs  
 Para ser executado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o UDT precisa implementar os seguintes requisitos na definição do UDT:  
  
 O UDT deve especificar o **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute**. O uso de **System. SerializableAttribute** é opcional, mas recomendado.  
  
-   O UDT deve implementar a interface **System. Data. SqlTypes. INullable** na classe ou estrutura criando um método nulo **estático** público (**compartilhado** no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic) **Null** . O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhece o valor nulo por padrão. Isso é necessário para que o código executado no UDT consiga reconhecer um valor nulo.  
  
-   O UDT deve conter um método de **análise** público **estático** (ou **compartilhado**) que ofereça suporte à análise de e um método **ToString** público para converter para uma representação de cadeia de caracteres do objeto.  
  
-   Um UDT com um formato de serialização definido pelo usuário deve implementar a interface **System. Data. ibinaryserializedmd** e fornecer um método **Read** e **Write** .  
  
-   O UDT deve implementar **System.Xml. Serialização. IXmlSerializable**ou todos os campos públicos e propriedades devem ser de tipos que são XML serializáveis ou decorados com o atributo **XmlIgnore** se for necessário substituir a serialização padrão.  
  
-   Deve haver apenas uma serialização de um objeto UDT. Haverá falha na validação se as rotinas de serialização ou desserialização reconhecerem mais de uma representação de um objeto específico.  
  
-   **SqlUserDefinedTypeAttribute. IsByteOrdered** deve ser **verdadeiro** para comparar dados em ordem de bytes. Se a interface IComparable não for implementada e **SqlUserDefinedTypeAttribute. IsByteOrdered** for **false**, as comparações de ordem de bytes falharão.  
  
-   Um UDT definido em uma classe deve ter um construtor público que não leve argumentos. Você tem a opção de criar construtores de classe sobrecarregados adicionais.  
  
-   O UDT precisa expor elementos de dados como campos públicos ou procedimentos de propriedade.  
  
-   Nomes públicos não podem ter mais de 128 caracteres e devem estar em conformidade com as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regras de nomenclatura para identificadores, conforme definido em [identificadores de banco de dados](../../relational-databases/databases/database-identifiers.md).  
  
-   colunas de **sql_variant** não podem conter instâncias de um UDT.  
  
-   Os membros herdados não são acessíveis a partir do [!INCLUDE[tsql](../../includes/tsql-md.md)] porque o sistema de tipos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não reconhece a hierarquia de herança entre UDTs. Entretanto, você pode usar a herança ao estruturar suas classes, além de chamar esses métodos na implementação de código gerenciado do tipo.  
  
-   Os membros não podem ficar sobrecarregados, com exceção do construtor de classe. Se você criar um método sobrecarregado, nenhum erro ocorrerá quando você registrar o assembly ou criar o tipo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A detecção do método sobrecarregado ocorre em tempo de execução, e não quando o tipo é criado. Os métodos sobrecarregados podem existir na classe, contanto que nunca sejam invocados. Quando você invoca o método sobrecarregado, ocorre um erro.  
  
-   Todos os membros **estáticos** (ou **compartilhados**) devem ser declarados como constantes ou somente leitura. Membros estáticos não podem ser mutáveis.  
  
-   Se o campo **SqlUserDefinedTypeAttribute. MaxByteSize** for definido como-1, o UDT serializado poderá ser tão grande quanto o limite de tamanho do objeto grande (LOB) (atualmente 2 GB). O tamanho de UDT não pode exceder o valor especificado no campo **MaxByteSized** .  
  
> [!NOTE]  
>  Embora não seja usado pelo servidor para executar comparações, você pode, opcionalmente, implementar a interface **System. IComparable** , que expõe um único método, **CompareTo**. Isso é usado no lado do cliente em situações nas quais é desejável comparar ou ordenar valores UDT com precisão.  
  
## <a name="native-serialization"></a>Serialização nativa  
 A escolha dos atributos de serialização adequados para o UDT depende do tipo de UDT que você está tentando criar. O formato de serialização **nativa** utiliza uma estrutura muito simples que permite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazenar uma representação nativa eficiente do UDT no disco. O formato **nativo** é recomendado se o UDT for simples e contiver apenas campos dos seguintes tipos:  
  
 **bool**, **byte**, **sbyte**, **short**, **ushort**, **int**, **uint**, **long**, **ulong**, **float**, **double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 Os tipos de valor que são compostos de campos dos tipos acima são bons candidatos para o formato **nativo** , como **structs** no Visual C#, (ou **estruturas** como são conhecidos em Visual Basic). Por exemplo, um UDT especificado com o formato de serialização **nativa** pode conter um campo de outro UDT que também foi especificado com o formato **nativo** . Se a definição de UDT for mais complexa e contiver tipos de dados que não estão na lista acima, você deverá especificar o formato de serialização **UserDefined** .  
  
 O formato **nativo** tem os seguintes requisitos:  
  
-   O tipo não deve especificar um valor para **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute. MaxByteSize**.  
  
-   Todos os campos precisam ser serializáveis.  
  
-   O **System. Runtime. InteropServices. StructLayoutAttribute** deve ser especificado como **StructLayout. LAYOUTKINDSEQUENTIAL** se o UDT for definido em uma classe e não em uma estrutura. Esse atributo controla o layout físico dos campos de dados e é usado para obrigar os membros a ser dispostos na ordem em que aparecem. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa esse atributo para determinar a ordem dos campos para UDTs com vários valores.  
  
 Para obter um exemplo de um UDT definido com serialização **nativa** , consulte o ponto UDT em [codificação de tipos definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="userdefined-serialization"></a>Serialização UserDefined  
 A configuração de formato **UserDefined** para o atributo **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** fornece ao desenvolvedor controle total sobre o formato binário. Ao especificar a propriedade de atributo de **formato** como **UserDefined**, você deve fazer o seguinte no seu código:  
  
-   Especifique a propriedade opcional do atributo **IsByteOrdered** . O valor padrão é **false**.  
  
-   Especifique a propriedade **MaxByteSize** do **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute**.  
  
-   Escreva o código para implementar métodos de **leitura** e **gravação** para o UDT implementando a interface **System. Data. Sql. ibinaryserializedmd** .  
  
 Para obter um exemplo de um UDT definido com serialização **UserDefined** , consulte a moeda UDT na [codificação de tipos definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
> [!NOTE]  
>  Os campos UDT precisam usar serialização nativa ou serem persistidos para serem indexados.  
  
## <a name="serialization-attributes"></a>Atributos de serialização  
 Os atributos determinam como a serialização é usada para construir a representação de armazenamento de UDTs e transmiti-los por valor para o cliente. Você deve especificar o **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** ao criar o UDT. O atributo **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** indica que a classe é um UDT e especifica o armazenamento para o UDT. Opcionalmente, você pode especificar o atributo **Serializable** , embora [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não exija isso.  
  
 O **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** tem as seguintes propriedades.  
  
 **Formatar**  
 Especifica o formato de serialização, que pode ser **nativo** ou **userdefinido**, dependendo dos tipos de dados do UDT.  
  
 **IsByteOrdered**  
 Um valor **booliano** que determina como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o executa comparações binárias em UDT.  
  
 **IsFixedLength**  
 Indica se todas as instâncias desse UDT têm a mesma extensão.  
  
 **MaxByteSize**  
 O tamanho máximo da instância, em bytes. Você deve especificar **MaxByteSize** com o formato de serialização **UserDefined** . Para um UDT com serialização definida pelo usuário especificada, **MaxByteSize** refere-se ao tamanho total do UDT em seu formato serializado, conforme definido pelo usuário. O valor de **MaxByteSize** deve estar no intervalo de 1 a 8000 ou definido como-1 para indicar que o UDT é maior que 8000 bytes (o tamanho total não pode exceder o tamanho máximo de LOB). Considere um UDT com uma propriedade de uma cadeia de caracteres de 10 caracteres (**System. Char**). Quando o UDT é serializado usando um BinaryWriter, o tamanho total da cadeia de caracteres serializada é de 22 bytes: 2 bytes por caractere Unicode UTF-16, multiplicados pelo número máximo de caracteres, mais 2 bytes de controle da sobrecarga ocasionada pela serialização de um fluxo binário. Portanto, ao determinar o valor de **MaxByteSize**, o tamanho total do UDT serializado deve ser considerado: o tamanho dos dados serializados em formato binário mais a sobrecarga incorrida pela serialização.  
  
 **ValidationMethodName**  
 O nome do método usado para validar instâncias do UDT.  
  
### <a name="setting-isbyteordered"></a>Definindo IsByteOrdered  
 Quando a propriedade **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute. IsByteOrdered** é definida como **true**, você está em vigor garantindo que os dados binários serializados possam ser usados para a ordenação semântica das informações. Assim, cada instância de um objeto UDT ordenado por byte pode ter somente uma representação serializada. Quando é executada uma operação de comparação no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos bytes serializados, os resultados devem ser os mesmos de quando a operação de comparação ocorre em código gerenciado. Os recursos a seguir também têm suporte quando **IsByteOrdered** está definido como **true**:  
  
-   A capacidade de criar índices em colunas desse tipo.  
  
-   A capacidade de criar chaves primárias e estrangeiras, além de restrições CHECK e UNIQUE em colunas desse tipo.  
  
-   A capacidade de usar as cláusulas [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY e PARTITION BY. Nesses casos, a representação binária do tipo é usada para determinar a ordem.  
  
-   A capacidade de usar operadores de comparação em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   A capacidade de persistir colunas computadas desse tipo.  
  
 Observe que os formatos de serialização **nativo** e **userdefinido** dão suporte aos seguintes operadores de comparação quando **IsByteOrdered** é definido como **true**:  
  
-   Igual a (=).  
  
-   Diferente de (!=)  
  
-   Maior que (>)  
  
-   Menor que (\<)  
  
-   Maior que ou igual a (>=)  
  
-   Menor que ou igual a (<=)  
  
### <a name="implementing-nullability"></a>Implementando a nulidade  
 Além de especificar corretamente os atributos dos assemblies, sua classe também precisa suportar a nulidade. Os UDTs carregados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm reconhecimento de nulo, mas, para que o UDT reconheça um valor nulo, a classe deve implementar a interface **INullable** . Para obter mais informações e um exemplo de como implementar a nulidade em um UDT, consulte [codificação de tipos definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
### <a name="string-conversions"></a>Conversões de cadeia de caracteres  
 Para dar suporte à conversão de cadeia de caracteres de e para o UDT, você deve fornecer um método **Parse** e um método **ToString** em sua classe. O método **Parse** permite que uma cadeia de caracteres seja convertida em UDT. Ele deve ser declarado como **estático** (ou **compartilhado** em Visual Basic) e pegar um parâmetro do tipo **System. Data. SqlTypes. SqlString**. Para obter mais informações e um exemplo de como implementar os métodos **Parse** e **ToString** , consulte [codificação de tipos definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="xml-serialization"></a>Serialização XML  
 Os UDTs devem dar suporte à conversão de e para o tipo de dados **XML** , de acordo com o contrato de SERIALIZAÇÃO de XML. O **System.Xml. **O namespace de serialização contém classes que são usadas para serializar objetos em documentos ou fluxos de formato XML. Você pode optar por implementar a serialização **XML** usando a interface **IXmlSerializable** , que fornece formatação personalizada para serialização e desserialização de XML.  
  
 Além de executar conversões explícitas de UDT em **XML**, a serialização de XML permite que você:  
  
-   Use o **XQuery** sobre valores de instâncias UDT após a conversão para o tipo de dados **XML** .  
  
-   Usar UDTs em consultas parametrizadas e métodos de Web com XML Web Services Nativos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usar UDTs para receber um carregamento em massa de dados XML.  
  
-   Serializar DataSets que contêm tabelas com colunas de UDT.  
  
 Os UDTs não são serializados em consultas FOR XML. Para executar uma consulta FOR XML que exibe a serialização XML de UDTs, converta explicitamente cada coluna UDT para o tipo de dados **XML** na instrução SELECT. Você também pode converter explicitamente as colunas em **varbinary**, **varchar**ou **nvarchar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
