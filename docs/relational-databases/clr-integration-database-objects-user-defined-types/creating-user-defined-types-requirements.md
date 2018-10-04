---
title: Requisitos de tipo definido pelo usuário | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6faf51099d0a5eced6543704d5f45b6fc922f522
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697110"
---
# <a name="creating-user-defined-types---requirements"></a>Criar tipos definidos pelo usuário – Requisitos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você deve tomar várias decisões de design importantes durante a criação de um tipo definido pelo usuário (UDT) a serem instalados em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De uma forma geral, é recomendável criar o UDT como uma estrutura, embora criá-lo como classe também seja uma opção. A definição do UDT precisa estar de acordo com as especificações para criação de UDTs para que seja registrado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="requirements-for-implementing-udts"></a>Requisitos para implementação de UDTs  
 Para ser executado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o UDT precisa implementar os seguintes requisitos na definição do UDT:  
  
 O UDT precisa especificar o **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**. O uso do **System.SerializableAttribute** é opcional, mas recomendada.  
  
-   O UDT precisa implementar o **System.Data.SqlTypes.INullable** interface na classe ou estrutura criando uma pública **estático** (**compartilhado** em [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic) **nulo** método. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhece o valor nulo por padrão. Isso é necessário para que o código executado no UDT consiga reconhecer um valor nulo.  
  
-   O UDT precisa conter um público **estáticos** (ou **compartilhado**) **analisar** método que dá suporte à análise de e uma pública **ToString** método para Convertendo em uma representação de cadeia de caracteres do objeto.  
  
-   Um UDT com um formato de serialização definida pelo usuário deve implementar o **System.Data.IBinarySerialize** interface e fornecer uma **leitura** e um **gravar** método.  
  
-   O UDT precisa implementar **System.Xml.Serialization.IXmlSerializable**, ou todas as propriedades e campos públicos devem ser de tipos que são serializáveis por XML ou decorados com o **XmlIgnore** se do atributo é necessário substituir a serialização padrão.  
  
-   Deve haver apenas uma serialização de um objeto UDT. Haverá falha na validação se as rotinas de serialização ou desserialização reconhecerem mais de uma representação de um objeto específico.  
  
-   **SqlUserDefinedTypeAttribute.IsByteOrdered** deve ser **verdadeiro** para comparar dados em ordem de byte. Se a interface IComparable não for implementada e **SqlUserDefinedTypeAttribute.IsByteOrdered** é **falso**, comparações de ordem de byte falharão.  
  
-   Um UDT definido em uma classe deve ter um construtor público que não leve argumentos. Você tem a opção de criar construtores de classe sobrecarregados adicionais.  
  
-   O UDT precisa expor elementos de dados como campos públicos ou procedimentos de propriedade.  
  
-   Nomes públicos não pode ter mais de 128 caracteres e deve estar de acordo com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regras de nomeação para identificadores conforme definido na [identificadores de banco de dados](../../relational-databases/databases/database-identifiers.md).  
  
-   **sql_variant** colunas não podem conter instâncias de um UDT.  
  
-   Os membros herdados não são acessíveis a partir do [!INCLUDE[tsql](../../includes/tsql-md.md)] porque o sistema de tipos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não reconhece a hierarquia de herança entre UDTs. Entretanto, você pode usar a herança ao estruturar suas classes, além de chamar esses métodos na implementação de código gerenciado do tipo.  
  
-   Os membros não podem ficar sobrecarregados, com exceção do construtor de classe. Se você criar um método sobrecarregado, nenhum erro ocorrerá quando você registrar o assembly ou criar o tipo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A detecção do método sobrecarregado ocorre em tempo de execução, e não quando o tipo é criado. Os métodos sobrecarregados podem existir na classe, contanto que nunca sejam invocados. Quando você invoca o método sobrecarregado, ocorre um erro.  
  
-   Qualquer **estáticos** (ou **compartilhado**) membros devem ser declarados como constantes ou somente leitura. Membros estáticos não podem ser mutáveis.  
  
-   Se o **SqlUserDefinedTypeAttribute.MaxByteSize** é definido como -1, o UDT serializado poderá ser tão grande quanto o limite de tamanho de objeto grande (LOB) (atualmente 2 GB). O tamanho do UDT não pode exceder o valor especificado na **MaxByteSized** campo.  
  
> [!NOTE]  
>  Embora não seja usada pelo servidor para realizar comparações, você pode, opcionalmente, implemente a **System. IComparable** interface, que expõe um único método, **CompareTo**. Isso é usado no lado do cliente em situações nas quais é desejável comparar ou ordenar valores UDT com precisão.  
  
## <a name="native-serialization"></a>Serialização nativa  
 A escolha dos atributos de serialização adequados para o UDT depende do tipo de UDT que você está tentando criar. O **nativos** utiliza uma estrutura muito simples que permite que o formato de serialização [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazene uma representação nativa eficiente do UDT em disco. O **nativo** formato é recomendado se o UDT for simple e contiver somente campos dos tipos a seguir:  
  
 **bool**, **byte**, **sbyte**, **short**, **ushort**, **int**, **uint**, **long**, **ulong**, **float**, **double**, **SqlByte**, **SqlInt16**, **SqlInt32**, **SqlInt64**, **SqlDateTime**, **SqlSingle**, **SqlDouble**, **SqlMoney**, **SqlBoolean**  
  
 Tipos de valores que são compostos de campos dos tipos mencionados acima são bons candidatos para **nativos** Formatar, como **structs** no Visual c# (ou **estruturas** conforme eles são conhecidos no Visual Basic). Por exemplo, um UDT especificado com o **nativos** formato de serialização pode conter um campo de outro UDT que também foi especificado com o **nativo** formato. Se a definição de UDT é mais complexa e contém os tipos de dados na lista acima, você deve especificar o **UserDefined** formato de serialização.  
  
 O **nativo** formato tem os seguintes requisitos:  
  
-   O tipo não deve especificar um valor para **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.MaxByteSize**.  
  
-   Todos os campos precisam ser serializáveis.  
  
-   O **StructLayoutAttribute** deve ser especificado como **LayoutKindSequential** se o UDT é definido em uma classe e não em uma estrutura. Esse atributo controla o layout físico dos campos de dados e é usado para obrigar os membros a ser dispostos na ordem em que aparecem. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa esse atributo para determinar a ordem dos campos para UDTs com vários valores.  
  
 Para obter um exemplo de um UDT definido com **nativos** serialização, consulte o UDT Point em [Codificando tipos](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="userdefined-serialization"></a>Serialização UserDefined  
 O **UserDefined** formato de configuração para o **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** fornece atributo ao desenvolvedor total controle sobre o formato binário. Ao especificar o **formato** propriedade como de atributo **UserDefined**, você deve fazer o seguinte em seu código:  
  
-   Especifique o valor opcional **IsByteOrdered** propriedade de atributo. O valor padrão é **false**.  
  
-   Especifique o **MaxByteSize** propriedade da **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**.  
  
-   Escrever código para implementar **leitura** e **escrever** métodos para o UDT Implementando a **System.Data.Sql.IBinarySerialize** interface.  
  
 Para obter um exemplo de um UDT definido com **UserDefined** serialização, consulte o UDT Currency em [Codificando tipos](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
> [!NOTE]  
>  Os campos UDT precisam usar serialização nativa ou serem persistidos para serem indexados.  
  
## <a name="serialization-attributes"></a>Atributos de serialização  
 Os atributos determinam como a serialização é usada para construir a representação de armazenamento de UDTs e transmiti-los por valor para o cliente. Você deve especificar o **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** ao criar o UDT. O **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** atributo indica que a classe é um UDT e especifica o armazenamento para o UDT. Opcionalmente, você pode especificar o **Serializable** do atributo, embora [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não requer isso.  
  
 O **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** tem as seguintes propriedades.  
  
 **Formato**  
 Especifica o formato de serialização, que pode ser **nativos** ou **UserDefined**, dependendo dos tipos de dados do UDT.  
  
 **IsByteOrdered**  
 Um **Boolean** valor que determina como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa comparações binárias no UDT.  
  
 **IsFixedLength**  
 Indica se todas as instâncias desse UDT têm a mesma extensão.  
  
 **MaxByteSize**  
 O tamanho máximo da instância, em bytes. Você deve especificar **MaxByteSize** com o **UserDefined** formato de serialização. Para um UDT com serialização definida pelo usuário especificado, **MaxByteSize** refere-se ao tamanho total do UDT em sua forma serializada conforme definido pelo usuário. O valor de **MaxByteSize** deve estar no intervalo de 1 a 8000 ou definido como -1 para indicar que o UDT é maior que 8000 bytes (o tamanho total não pode exceder o tamanho LOB máximo). Considere um UDT com uma propriedade de uma cadeia de caracteres de 10 caracteres (**System. Char**). Quando o UDT é serializado usando um BinaryWriter, o tamanho total da cadeia de caracteres serializada é de 22 bytes: 2 bytes por caractere Unicode UTF-16, multiplicados pelo número máximo de caracteres, mais 2 bytes de controle da sobrecarga ocasionada pela serialização de um fluxo binário. Portanto, ao determinar o valor de **MaxByteSize**, deve ser considerado o tamanho total do UDT serializado: o tamanho dos dados serializados em formato binário mais a sobrecarga ocasionada pela serialização.  
  
 **ValidationMethodName**  
 O nome do método usado para validar instâncias do UDT.  
  
### <a name="setting-isbyteordered"></a>Definindo IsByteOrdered  
 Quando o **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.IsByteOrdered** estiver definida como **verdadeiro**, você está garantindo que os dados binários serializados podem ser usados para semântica ordenação das informações. Assim, cada instância de um objeto UDT ordenado por byte pode ter somente uma representação serializada. Quando é executada uma operação de comparação no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nos bytes serializados, os resultados devem ser os mesmos de quando a operação de comparação ocorre em código gerenciado. Os recursos a seguir também são suportados quando **IsByteOrdered** é definido como **verdadeiro**:  
  
-   A capacidade de criar índices em colunas desse tipo.  
  
-   A capacidade de criar chaves primárias e estrangeiras, além de restrições CHECK e UNIQUE em colunas desse tipo.  
  
-   A capacidade de usar as cláusulas [!INCLUDE[tsql](../../includes/tsql-md.md)] ORDER BY, GROUP BY e PARTITION BY. Nesses casos, a representação binária do tipo é usada para determinar a ordem.  
  
-   A capacidade de usar operadores de comparação em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   A capacidade de persistir colunas computadas desse tipo.  
  
 Observe que tanto a **nativos** e **UserDefined** formatos de serialização suportam os seguintes operadores de comparação quando **IsByteOrdered** é definido como **true** :  
  
-   Igual a (=).  
  
-   Diferente de (!=)  
  
-   Maior que (>)  
  
-   Menor que (\<)  
  
-   Maior que ou igual a (>=)  
  
-   Menor que ou igual a (<=)  
  
### <a name="implementing-nullability"></a>Implementando a nulidade  
 Além de especificar corretamente os atributos dos assemblies, sua classe também precisa suportar a nulidade. Os UDTs carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhecem nulos, mas para o UDT reconheça um valor nulo, a classe deve implementar a **INullable** interface. Para obter mais informações e um exemplo de como implementar a nulidade em um UDT, consulte [Codificando tipos](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
### <a name="string-conversions"></a>Conversões de cadeia de caracteres  
 Para dar suporte à conversão de cadeia de caracteres de e para o UDT, você deve fornecer um **analisar** método e uma **ToString** método em sua classe. O **analisar** método permite que uma cadeia de caracteres a ser convertido em um UDT. Ele deve ser declarado como **estáticos** (ou **compartilhado** no Visual Basic) e usar um parâmetro de tipo **System.Data.SqlTypes.SqlString**. Para obter mais informações e um exemplo de como implementar o **analisar** e **ToString** métodos, consulte [Codificando tipos](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
## <a name="xml-serialization"></a>Serialização XML  
 Os UDTs precisam suportar a conversão de e para o **xml** tipo de dados por estar em conformidade com o contrato para serialização de XML. O **Serialization** namespace contém classes que são usadas para serializar objetos em fluxos ou documentos de formato XML. Você pode optar por implementar **xml** serialização usando o **IXmlSerializable** interface, que oferece formatação personalizada para serialização e desserialização XML.  
  
 Além de realizar conversões explícitas de UDT **xml**, a serialização XML permite que você:  
  
-   Use **Xquery** sobre os valores de instâncias UDT após a conversão para o **xml** tipo de dados.  
  
-   Usar UDTs em consultas parametrizadas e métodos de Web com XML Web Services Nativos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usar UDTs para receber um carregamento em massa de dados XML.  
  
-   Serializar DataSets que contêm tabelas com colunas de UDT.  
  
 Os UDTs não são serializados em consultas FOR XML. Para executar uma consulta FOR XML que exibe a serialização XML dos UDTs, converta explicitamente cada coluna UDT para o **xml** tipo de dados na instrução SELECT. Você também pode converter explicitamente as colunas a serem **varbinary**, **varchar**, ou **nvarchar**.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
