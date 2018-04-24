---
title: O objeto de campo | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b0fc2840f9cd1b9dde3e5a9a883f3f37ce816b8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="the-field-object"></a>O objeto de campo
Cada **campo** objeto geralmente corresponde a uma coluna em uma tabela de banco de dados. No entanto, um **campo** também pode representar um ponteiro para outro **registros**, chamado um capítulo. Exceções, como colunas de capítulo serão abordadas posteriormente neste guia.  
  
 Use o **valor** propriedade **campo** objetos para definir ou retornar dados para o registro atual. Dependendo da funcionalidade de provedor expõe, algumas coleções, métodos ou propriedades de um **campo** objeto pode não estar disponível.  
  
 Com as coleções, métodos e propriedades de um **campo** do objeto, você pode fazer o seguinte:  
  
-   Retornar o nome de um campo usando o **nome** propriedade.  
  
-   Exibir ou alterar os dados no campo usando o **valor** propriedade. **Valor** é a propriedade padrão do **campo** objeto.  
  
-   Retornar as características básicas de um campo usando o **tipo**, **precisão**, e **NumericScale** propriedades.  
  
-   Retornar o tamanho declarado de um campo usando o **DefinedSize** propriedade.  
  
-   Retornar o tamanho real dos dados em um determinado campo usando o **ActualSize** propriedade.  
  
-   Determinar quais tipos de funcionalidade tem suporte para um determinado campo usando o **atributos** propriedade e **propriedades** coleção.  
  
-   Manipular os valores dos campos que contêm dados binários longos ou tempo de caractere usando o **AppendChunk** e **GetChunk** métodos.  
  
 Resolver as discrepâncias em valores de campo durante a atualização em lotes usando o **OriginalValue** e **UnderlyingValue** propriedades, se o provedor oferece suporte a atualizações em lotes.  
  
## <a name="describing-a-field"></a>Que descreve um campo  
 Os tópicos a seguir será abordam propriedades do [campo](../../../ado/reference/ado-api/field-object.md) objeto que representam informações que descrevem o **campo** próprio objeto — ou seja, os metadados sobre o campo. Essas informações podem ser usadas para determinar quanto o esquema do **registros**. Essas propriedades incluem **tipo**, **DefinedSize** e **ActualSize**, **nome**, e **NumericScale**e **precisão**.  
  
### <a name="discovering-the-data-type"></a>Descobrir o tipo de dados  
 O **tipo** propriedade indica o tipo de dados do campo. O tipo de dados constantes enumeradas ADO com suporte são descritas na [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) no *referência do programador de ADO*.  
  
 Para tipos numéricos, de ponto flutuante **adNumeric**, você pode obter mais informações. O **NumericScale** propriedade indica o número de dígitos à direita da vírgula decimal será usado para representar valores para o **campo**. O **precisão** propriedade especifica o número máximo de dígitos usados para representar valores para o **campo**.  
  
### <a name="determining-field-size"></a>Determinar o tamanho do campo  
 Use o **DefinedSize** propriedade para determinar a capacidade de dados de um **campo** objeto.  
  
 Use o **ActualSize** propriedade para retornar o comprimento real de um **campo** valor do objeto. Todos os campos, o **ActualSize** propriedade é somente leitura. Se o ADO não é possível determinar o comprimento de **campo** valor do objeto, o **ActualSize** propriedade retorna **adUnknown**.  
  
 O **DefinedSize** e **ActualSize** propriedades têm finalidades diferentes. Por exemplo, considere um **campo** objeto com um tipo declarado de **adVarChar** e um **DefinedSize** valor da propriedade de 50, que contém um único caractere. O **ActualSize** valor de propriedade retornado é o comprimento em bytes do caractere único.  
  
### <a name="determining-field-contents"></a>Determinando o conteúdo do campo  
 O identificador da coluna da fonte de dados é representado pelo **nome** propriedade o **campo**. O **valor** propriedade o **campo** objeto retorna ou define o conteúdo de dados real do campo. Esta é a propriedade padrão.  
  
 Para alterar os dados em um campo, defina o **valor** propriedade igual a um novo valor do tipo correto. O tipo de cursor deve oferecer suporte a atualizações para alterar o conteúdo de um campo. Validação de banco de dados não é feita aqui no modo de lote, portanto, será necessário verificar se há erros quando você chamar **UpdateBatch** nesse caso. Alguns provedores também oferecem suporte a ADO **campo** do objeto **UnderlyingValue** e **OriginalValue** propriedades para ajudar a resolver conflitos durante a tentativa Execute atualizações em lotes. Para obter detalhes sobre como resolver esses conflitos, consulte [edição dados](../../../ado/guide/data/editing-data.md).  
  
> [!NOTE]
>  **Recordset Field** valores não podem ser definidos ao anexar novos **campos** para um **registros**. Em vez disso, novos **campos** pode ser anexada a um fechado **Recordset**. Em seguida, o **registros** deve ser aberto e, em seguida, só podem ser atribuídos valores esses **campos**.  
  
### <a name="getting-more-field-information"></a>Obter mais informações sobre o campo  
 Objetos de ADO têm dois tipos de propriedades: interna e dinâmicos. Neste ponto, apenas as propriedades internas do **campo** objeto foram discutidos.  
  
 Propriedades internas são as propriedades implementadas no ADO e imediatamente disponíveis para qualquer novo objeto, usando o `MyObject.Property` sintaxe. Eles não aparecem como **propriedade** objetos em um objeto **propriedades** coleção.  
  
 Propriedades dinâmicas são definidas pelo provedor de dados subjacente e aparecem no **propriedades** coleção do objeto ADO apropriado. Por exemplo, uma propriedade específica do provedor pode indicar se uma **registros** objeto oferece suporte a transações ou atualização. Essas propriedades adicionais serão exibidas como **propriedade** objetos em que **registros** do objeto **propriedades** coleção. Propriedades dinâmicas que podem ser referenciadas apenas por meio da coleção, usando a sintaxe `MyObject.Properties(0)` ou `MyObject.Properties("Name")`.  
  
 Não é possível excluir o tipo de propriedade.  
  
 Um dinâmico **propriedade** objeto tem quatro propriedades internas de seu próprio:  
  
-   O **nome** propriedade é uma cadeia de caracteres que identifica a propriedade.  
  
-   O **tipo** propriedade é um inteiro que especifica o tipo de dados da propriedade.  
  
-   O **valor** propriedade é um tipo variant que contém a configuração da propriedade. **Valor** é a propriedade padrão para um **propriedade** objeto.  
  
-   O **atributos** propriedade é um **longo** valor que indica as características da propriedade específica do provedor.  
  
 O **propriedades** coleta para o **campo** objeto contém metadados adicionais sobre o campo. O conteúdo desta coleção varia de acordo com o provedor. O exemplo de código a seguir examina o **propriedades** coleção do exemplo **registros** introduzido no começo desta seção. Primeiro examina o conteúdo da coleção. Esse código usa o [OLE DB Provider para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), portanto, o **propriedades** coleção contém informações relevantes para esse provedor.  
  
```  
'BeginFieldProps  
    Dim objProp As ADODB.Property  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
  
        For Each objProp In objFields(intLoop).Properties  
            Debug.Print vbTab & objProp.Name & " = " & objProp.Value  
        Next objProp  
    Next intLoop  
'EndFieldProps  
```  
  
### <a name="dealing-with-binary-data"></a>Trabalhar com dados binários  
 Use o [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) método em um **campo** objeto preenchê-lo com dados binários longos ou de caractere. Em situações em que a memória do sistema é limitada, você pode usar o **AppendChunk** método para manipular valores longos em partes em vez de em sua totalidade.  
  
 Se o **adFldLong** bit no **atributos** propriedade de um **campo** objeto é definido como **True**, você pode usar o  **AppendChunk** método para esse campo.  
  
 A primeira **AppendChunk** chamar em um **campo** objeto grava dados para o campo, substituindo os dados existentes. Subsequentes **AppendChunk** adicionam chamadas aos dados existentes. Se você está anexando um campo de dados e, em seguida, você pode definir ou ler o valor de outro campo no registro atual, o ADO pressupõe que você tiver terminado de anexar os dados para o primeiro campo. Se você chamar o **AppendChunk** método no primeiro campo novamente, ADO interpreta a chamada como um novo **AppendChunk** operação e substitui os dados existentes. Acessar campos em outros **registros** objetos que não são clones do primeiro **registros** objeto não interromperá **AppendChunk** operações.  
  
 Use o **GetChunk** método em um **campo** objeto recuperar parte ou todos os seus dados binários longos ou de caractere. Em situações em que a memória do sistema é limitada, você pode usar o **GetChunk** método para manipular valores longos em partes, em vez de em sua totalidade.  
  
 Os dados que um **GetChunk** chamada retorna é atribuído a *variável*. Se *tamanho* é maior do que os dados restantes, o **GetChunk** método retorna apenas os dados restantes sem preenchimento *variável* com espaços vazios. Se o campo estiver vazio, o **GetChunk** método retorna um valor nulo.  
  
 Cada subsequentes **GetChunk** chamada recupera dados a partir de onde o anterior **GetChunk** chamada parou. No entanto, se você estiver recuperando dados de um campo e, em seguida, definir ou ler o valor de outro campo no registro atual, o ADO pressupõe que você concluiu a recuperação de dados do primeiro campo. Se você chamar o **GetChunk** método no primeiro campo novamente, ADO interpreta a chamada como um novo **GetChunk** operação e começa a leitura do início dos dados. Acessar campos em outros **registros** objetos que não são clones do primeiro **registros** objeto não interromperá **GetChunk** operações.  
  
 Se o **adFldLong** bit no **atributos** propriedade de um **campo** objeto é definido como **True**, você pode usar o **GetChunk**  método para esse campo.  
  
 Se não houver nenhum registro atual quando você usa o **GetChunk** ou **AppendChunk** método em um **campo** do objeto, ocorrerá erro 3021 (não há registro atual).  
  
 Para obter um exemplo de como usar esses métodos para manipular dados binários, consulte o [método AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [método GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) exemplos de *referência do programador de ADO*.
