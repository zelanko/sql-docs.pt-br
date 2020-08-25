---
description: Objeto Recordset (ADO)
title: Objeto Recordset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
author: rothja
ms.author: jroth
ms.openlocfilehash: d9fade9e23303c9adaa22cad9822381fd10bb513
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772265"
---
# <a name="recordset-object-ado"></a>Objeto Recordset (ADO)
Representa o conjunto inteiro de registros de uma tabela base ou os resultados de um comando executado. A qualquer momento, o objeto **Recordset** refere-se apenas a um único registro dentro do conjunto como o registro atual.  
  
## <a name="remarks"></a>Comentários  
 Você usa objetos **Recordset** para manipular dados de um provedor. Ao usar o ADO, você manipula dados quase totalmente usando objetos **Recordset** . Todos os objetos **Recordset** consistem em registros (linhas) e campos (colunas). Dependendo da funcionalidade suportada pelo provedor, alguns métodos ou propriedades do **conjunto de registros** podem não estar disponíveis.  
  
 ActiveX. Recordset é o ProgID que deve ser usado para criar um objeto **Recordset** . Aplicativos existentes que fazem referência a ADOR desatualizadas. O ProgID do conjunto de registros continuará a funcionar sem recompilar, mas o novo desenvolvimento deve fazer referência a ADODB. Registros.  
  
 Há quatro tipos de cursor diferentes definidos no ADO:  
  
-   **Cursor dinâmico** Permite exibir adições, alterações e exclusões por outros usuários; permite todos os tipos de movimento por meio do **conjunto de registros** que não depende de indicadores; e permitirá indicadores se o provedor oferecer suporte a eles.  
  
-   **Cursor** do conjunto de chaves Comporta-se como um cursor dinâmico, exceto que ele impede que você veja os registros que outros usuários adicionam e impede o acesso a registros que outros usuários excluem. As alterações de dados por outros usuários ainda estarão visíveis. Ele sempre dá suporte a indicadores e, portanto, permite todos os tipos de movimento por meio do **conjunto de registros**.  
  
-   **Cursor estático** Fornece uma cópia estática de um conjunto de registros para que você use para localizar dados ou gerar relatórios; sempre permite indicadores e, portanto, permite todos os tipos de movimento por meio do **conjunto de registros**. Adições, alterações ou exclusões por outros usuários não estarão visíveis. Esse é o único tipo de cursor permitido quando você abre um objeto **Recordset** do lado do cliente.  
  
-   **Cursor de somente avanço** Permite que você role para frente pelo **conjunto de registros**. Adições, alterações ou exclusões por outros usuários não estarão visíveis. Isso melhora o desempenho em situações em que você precisa fazer uma passagem única por um **conjunto de registros**.  
  
 Defina a propriedade [CursorType](./cursortype-property-ado.md) antes de abrir o **conjunto de registros** para escolher o tipo de cursor ou passe um argumento *CursorType* com o método [Open](./open-method-ado-recordset.md) . Alguns provedores não dão suporte a todos os tipos de cursor. Verifique a documentação do provedor. Se você não especificar um tipo de cursor, o ADO abrirá um cursor de somente avanço por padrão.  
  
 Se a propriedade [CursorLocation](./cursorlocation-property-ado.md) for definida como **adUseClient** para abrir um **conjunto de registros**, a propriedade **subdependvalue** em objetos de [campo](./field-object.md) não estará disponível no objeto **Recordset** retornado. Quando usado com alguns provedores (como o provedor ODBC da Microsoft para OLE DB em conjunto com Microsoft SQL Server), você pode criar objetos **Recordset** independentemente de um objeto de [conexão](./connection-object-ado.md) definido anteriormente, passando uma cadeia de conexão com o método **Open** . O ADO ainda cria um objeto de [conexão](./connection-object-ado.md) , mas não atribui esse objeto a uma variável de objeto. No entanto, se você estiver abrindo vários objetos de **conjunto de registros** na mesma conexão, deverá criar e abrir explicitamente um objeto de **conexão** ; Isso atribui o objeto de **conexão** a uma variável de objeto. Se você não usar essa variável de objeto ao abrir seus objetos de **conjunto de registros** , o ADO criará um novo objeto de **conexão** para cada novo **conjunto de registros**, mesmo se você passar a mesma cadeia de conexão.  
  
 Você pode criar quantos objetos de **conjunto de registros** forem necessários.  
  
 Quando você abre um **conjunto de registros**, o registro atual é posicionado no primeiro registro (se houver) e as propriedades [BOF](./bof-eof-properties-ado.md) e [EOF](./bof-eof-properties-ado.md) são definidas como **false**. Se não houver nenhum registro, as configurações de propriedade **BOF** e **EOF** serão **verdadeiras**.  
  
 Você pode usar os métodos [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**, **MoveNext**e **MovePrevious** ; o método [move](./move-method-ado.md) ; e as propriedades [AbsolutePosition](./absoluteposition-property-ado.md), [AbsolutePage](./absolutepage-property-ado.md)e [Filter](./filter-property.md) para reposicionar o registro atual, supondo que o provedor dê suporte à funcionalidade relevante. Objetos **Recordset** somente de encaminhamento dão suporte apenas ao método [MoveNext](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) . Ao usar os métodos **move** para visitar cada registro (ou enumerar o **conjunto de registros**), você pode usar as propriedades **BOF** e **EOF** para determinar se você se moveu além do início ou do fim do **conjunto de registros**.  
  
 Antes de usar qualquer funcionalidade de um objeto de **conjunto de registros** , você deve chamar o método de **suporte** no objeto para verificar se a funcionalidade tem suporte ou está disponível. Você não deve usar a funcionalidade quando o método de **suporte** retornar false. Por exemplo, você pode usar o método **MovePrevious** somente se `Recordset.Supports(adMovePrevious)` retornar **true**. Caso contrário, você receberá um erro, pois o objeto **Recordset** pode ter sido fechado e a funcionalidade não foi processada na instância. Se não houver suporte para um recurso no qual você esteja interessado, o **suporte** retornará false também. Nesse caso, você deve evitar chamar a propriedade ou o método correspondente no objeto **Recordset** .  
  
 Os objetos **Recordset** podem dar suporte a dois tipos de atualização: imediata e em lote. Na atualização imediata, todas as alterações nos dados são gravadas imediatamente na fonte de dados subjacente depois que você chama o método [Update](./update-method.md) . Você também pode passar matrizes de valores como parâmetros com os métodos [AddNew](./addnew-method-ado.md) e **Update** e atualizar simultaneamente vários campos em um registro.  
  
 Se um provedor oferecer suporte à atualização em lotes, você poderá fazer com que o cache do provedor seja alterado para mais de um registro e, em seguida, transmiti-los em uma única chamada para o banco de dados com o método [UpdateBatch](./updatebatch-method.md) . Isso se aplica a alterações feitas com os métodos **AddNew**, **Update**e [delete](./delete-method-ado-recordset.md) . Depois de chamar o método **UpdateBatch** , você pode usar a propriedade [status](./status-property-ado-recordset.md) para verificar se há conflitos de dados a fim de resolvê-los.  
  
> [!NOTE]
>  Para executar uma consulta sem usar um objeto [Command](./command-object-ado.md) , passe uma cadeia de caracteres de consulta para o método **Open** de um objeto **Recordset** . No entanto, um objeto de **comando** é necessário quando você deseja manter o texto do comando e executá-lo novamente, ou usar parâmetros de consulta.  
  
 A propriedade [Mode](./mode-property-ado.md) governa as permissões de acesso.  
  
 A coleção **Fields** é o membro padrão do objeto **Recordset** . Como resultado, as duas instruções de código a seguir são equivalentes.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 Quando um objeto **Recordset** é passado entre os processos, somente os valores do **conjunto de linhas** são marshalled e as propriedades do objeto **Recordset** são ignoradas. Durante o desempacotamento, o **conjunto de linhas** é desempacotado em um objeto **Recordset** recém-criado, que também define suas propriedades com os valores padrão.  
  
 O objeto **Recordset** é seguro para scripts.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Recordset](./recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de conexão (ADO)](./connection-object-ado.md)   
 [Coleção Fields (ADO)](./fields-collection-ado.md)   
 [Coleção Properties (ADO)](./properties-collection-ado.md)   
 [Apêndice A: Provedores](../../guide/appendixes/appendix-a-providers.md)