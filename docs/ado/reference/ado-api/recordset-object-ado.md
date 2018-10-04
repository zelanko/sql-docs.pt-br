---
title: O objeto de conjunto de registros (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bf2aab4e9f11ff3dae9852dd80007867fe5a462
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770824"
---
# <a name="recordset-object-ado"></a>Objeto Recordset (ADO)
Representa todo o conjunto de registros de uma tabela base ou os resultados de um comando executado. A qualquer momento, o **Recordset** objeto se refere a um único registro dentro do conjunto de como o registro atual.  
  
## <a name="remarks"></a>Comentários  
 Você usa **Recordset** objetos para manipular os dados de um provedor. Quando você usa ADO, você manipular os dados usando quase que totalmente **Recordset** objetos. Todos os **Recordset** objetos consistem em registros (linhas) e campos (colunas). Dependendo da funcionalidade com suporte pelo provedor, alguns **Recordset** métodos ou propriedades podem não estar disponíveis.  
  
 ADODB. Conjunto de registros é o ProgID que deve ser usado para criar uma **Recordset** objeto. Aplicativos existentes que fazem referência a objeto ADOR desatualizado. Conjunto de registros ProgID continuarão a funcionar sem recompilar, mas novos desenvolvimentos devem referenciar o objeto ADODB. Conjunto de registros.  
  
 Há quatro tipos diferentes de cursor definidos no ADO:  
  
-   **Cursor dinâmico** permite que você exiba as adições, alterações e exclusões por outros usuários; permite que todos os tipos de movimentação por meio de **Recordset** que não depende de indicadores; e permite que os indicadores se o provedor oferece suporte -los.  
  
-   **Cursor keyset** Behaves como um cursor dinâmico, exceto que ele impede que você veja registros que outros usuários, adicionar e impede o acesso a registros que excluem outros usuários. As alterações de dados por outros usuários ainda estarão visíveis. Ele sempre dá suporte a indicadores e, portanto, permite que todos os tipos de movimentação por meio de **conjunto de registros**.  
  
-   **Cursor estático** fornece uma cópia estática de um conjunto de registros para que você possa usar para localizar dados ou gerar relatórios; sempre permite indicadores e, portanto, permite que todos os tipos de movimentação por meio de **conjunto de registros**. Adições, alterações ou exclusões por outros usuários não será visíveis. Isso é o único tipo de cursor permitido quando você abre um lado do cliente **Recordset** objeto.  
  
-   **Cursor somente de avanço** permite que você apenas para rolar para frente por meio de **conjunto de registros**. Adições, alterações ou exclusões por outros usuários não será visíveis. Isso melhora o desempenho em situações em que você precisa fazer apenas uma única passagem por meio de um **conjunto de registros**.  
  
 Defina a [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) propriedade antes da abertura a **conjunto de registros** para escolher o tipo de cursor ou passar um *CursorType* argumento com o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)método. Alguns provedores não dão suporte a todos os tipos de cursor. Verifique a documentação do provedor. Se você não especificar um tipo de cursor, o ADO abre um cursor somente encaminhamento, por padrão.  
  
 Se o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) estiver definida como **adUseClient** para abrir um **conjunto de registros**, o **UnderlyingValue** propriedade [Campo](../../../ado/reference/ado-api/field-object.md) objetos não está disponível no retornado **Recordset** objeto. Quando usado com alguns provedores (como o Microsoft ODBC para OLE DB em conjunto com o Microsoft SQL Server), você pode criar **conjunto de registros** objetos independentemente definido anteriormente [Conexão](../../../ado/reference/ado-api/connection-object-ado.md)objeto, passando uma cadeia de caracteres de conexão com o **abra** método. ADO ainda cria uma [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto, mas ele não atribui o objeto a uma variável de objeto. No entanto, se você estiver abrindo vários **conjunto de registros** objetos sobre a mesma conexão, você deve criar explicitamente e abrir um **Conexão** objeto; este atribui o **Conexão**objeto para uma variável de objeto. Se você não usar essa variável de objeto ao abrir sua **conjunto de registros** objetos, ADO cria uma nova **Conexão** objeto para cada novo **Recordset**, mesmo se você passar o mesmo cadeia de caracteres de conexão.  
  
 Você pode criar tantos **Recordset** objetos conforme necessário.  
  
 Quando você abre um **conjunto de registros**, o registro atual é posicionado no primeiro registro (se houver) e o [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propriedades são definidas como **False**. Se não houver nenhum registro, o **BOF** e **EOF** configurações de propriedade são **verdadeiro**.  
  
 Você pode usar o [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**, **MoveNext**, e **MovePrevious** métodos; o [mover](../../../ado/reference/ado-api/move-method-ado.md) método; e o [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), e [filtro](../../../ado/reference/ado-api/filter-property.md) propriedades para reposicionar o registro atual, supondo que o provedor oferece suporte a relevantes funcionalidade. Somente de avanço **conjunto de registros** objetos dão suporte apenas a [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) método. Quando você usa o **mover** métodos para visitar cada registro (ou enumerar os **conjunto de registros**), você pode usar o **BOF** e **EOF** propriedades para determinar se você tiver movido para fora o início ou término do **conjunto de registros**.  
  
 Antes de usar qualquer funcionalidade de um **conjunto de registros** do objeto, você deve chamar o **dá suporte a** método no objeto para verificar se a funcionalidade está disponível ou com suporte. Você não deve usar a funcionalidade quando o **dá suporte a** método retornará false. Por exemplo, você pode usar o **MovePrevious** método apenas se `Recordset.Supports(adMovePrevious)` retorna **True**. Caso contrário, você receberá um erro, pois o **Recordset** objeto fechado e a funcionalidade renderizado indisponível na instância. Se não há suporte para um recurso que você está interessado, **dá suporte a** retornará false também. Nesse caso, você deve evitar chamar o método ou propriedade correspondente a **Recordset** objeto.  
  
 **Conjunto de registros** objetos podem dar suporte a dois tipos de atualização: imediatas e em lote. Em atualização imediata, todas as alterações de dados são gravadas imediatamente a fonte de dados depois de chamar o [atualização](../../../ado/reference/ado-api/update-method.md) método. Você também pode passar matrizes de valores como parâmetros com o [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) e **atualizar** métodos e atualizar simultaneamente vários campos em um registro.  
  
 Se um provedor oferecer suporte a atualização em lotes, você pode ter o provedor de alterações em mais de um registro de cache e, em seguida, transmiti-las em uma única chamada ao banco de dados com o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Isso se aplica às alterações feitas com o **AddNew**, **atualização**, e [excluir](../../../ado/reference/ado-api/delete-method-ado-recordset.md) métodos. Depois de chamar o **UpdateBatch** método, você pode usar o [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade para verificar se há quaisquer conflitos de dados para resolvê-los.  
  
> [!NOTE]
>  Para executar uma consulta sem usar um [comando](../../../ado/reference/ado-api/command-object-ado.md) do objeto, passe uma cadeia de caracteres de consulta para o **abra** método de um **conjunto de registros** objeto. No entanto, uma **comando** objeto é necessário quando você deseja manter o texto do comando e executá-la novamente ou use parâmetros de consulta.  
  
 O [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade controla as permissões de acesso.  
  
 O **campos** coleção é o membro padrão de **conjunto de registros** objeto. Como resultado, as duas instruções de código a seguir são equivalentes.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 Quando um **conjunto de registros** objeto é passado entre processos, somente os **conjunto de linhas** valores são marshaling e as propriedades da **Recordset** objeto são ignorados. Durante a Desempacotando, o **conjunto de linhas** seja descompactado em uma recém-criado **Recordset** objeto, que também define suas propriedades para os valores padrão.  
  
 O **Recordset** objeto é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Eventos, métodos e propriedades do objeto de conjunto de registros](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
