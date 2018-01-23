---
title: O objeto de conjunto de registros (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset
helpviewer_keywords: Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: dd263b08584b0ba13f6486e72bcf6c9f083ca896
ms.sourcegitcommit: b09bccd6dfdba55b022355e892c29cb50aadd795
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="recordset-object-ado"></a>Objeto de conjunto de registros (ADO)
Representa todo o conjunto de registros de uma tabela base ou os resultados de um comando executado. A qualquer momento, o **registros** objeto se refere a um único registro dentro do conjunto de como o registro atual.  
  
## <a name="remarks"></a>Remarks  
 Você usa **registros** objetos para manipular os dados de um provedor. Quando você usa ADO, você manipula dados quase inteiramente usando **registros** objetos. Todos os **registros** objetos consistem em registros (linhas) e campos (colunas). Dependendo da funcionalidade com suporte pelo provedor, alguns **registros** métodos ou propriedades podem não estar disponíveis.  
  
 ADODB. Conjunto de registros é o ProgID que deve ser usado para criar um **registros** objeto. Aplicativos existentes que fazem referência a objeto ADOR desatualizado. ProgID do conjunto de registros continuarão a funcionar sem recompilar, mas novos desenvolvimentos devem fazer referência a objeto ADODB. Conjunto de registros.  
  
 Há quatro tipos diferentes de cursor definidos no ADO:  
  
-   **Cursor dinâmico** permite que você exiba adições, alterações e exclusões por outros usuários; permite que todos os tipos de movimento por meio de **registros** que não depende de indicadores; e permite que os indicadores se o provedor oferece suporte -los.  
  
-   **Cursor keyset** Behaves como um cursor dinâmico, exceto que ela impede que você veja os registros que outros usuários adicionar e impede o acesso a registros que outros usuários excluírem. Alterações de dados por outros usuários ainda estarão visíveis. Ele sempre dá suporte a indicadores e, portanto, permite que todos os tipos de movimento por meio de **registros**.  
  
-   **Cursor estático** fornece uma cópia estática de um conjunto de registros para uso para encontrar dados ou gerar relatórios; sempre permite indicadores e, portanto, permite que todos os tipos de movimento por meio de **registros**. Adições, alterações ou exclusões por outros usuários não serão visíveis. Este é o único tipo de cursor permitido quando você abre um cliente **registros** objeto.  
  
-   **Cursor somente de avanço** permite apenas rolar para frente o **registros**. Adições, alterações ou exclusões por outros usuários não serão visíveis. Isso melhora o desempenho em situações em que você precisa fazer uma única passagem por meio de um **registros**.  
  
 Definir o [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) propriedade antes de abrir o **Recordset** para escolher o tipo de cursor ou passe um *CursorType* argumento com o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)método. Alguns provedores não oferecem suporte a todos os tipos de cursor. Verifique a documentação para o provedor. Se você não especificar um tipo de cursor, o ADO abre um cursor somente de encaminhamento por padrão.  
  
 Se o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) está definida como **adUseClient** para abrir um **registros**, o **UnderlyingValue** propriedade [Campo](../../../ado/reference/ado-api/field-object.md) objetos não está disponível em retornado **registros** objeto. Quando usado com alguns provedores (como o Microsoft ODBC Provider for OLE DB em conjunto com o Microsoft SQL Server), você pode criar **registros** objetos independentemente definido anteriormente [Conexão](../../../ado/reference/ado-api/connection-object-ado.md)objeto passando uma cadeia de caracteres de conexão com o **abrir** método. ADO ainda cria um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto, mas ele não atribui o objeto a uma variável de objeto. No entanto, se você está abrindo várias **registros** objetos sobre a mesma conexão, você deve criar explicitamente e abrir um **Conexão** objeto; essa atribui a **Conexão**objeto a uma variável de objeto. Se você não usar essa variável de objeto ao abrir o **registros** objetos, ADO cria um novo **Conexão** objeto para cada novo **registros**, mesmo se você passar o mesmo cadeia de caracteres de conexão.  
  
 Você pode criar tantas **registros** objetos conforme necessário.  
  
 Quando você abre um **registros**, o registro atual é posicionado no primeiro registro (se houver) e o [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propriedades são definidas como **False**. Se não houver nenhum registro a **BOF** e **EOF** as configurações de propriedade são **True**.  
  
 Você pode usar o [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**, **MoveNext**, e **MovePrevious** métodos; o [mover](../../../ado/reference/ado-api/move-method-ado.md) método; e o [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), e [filtro](../../../ado/reference/ado-api/filter-property.md) propriedades para reposicionar o registro atual, supondo que o provedor oferece suporte a relevantes funcionalidade. Somente avanço **registros** objetos oferecem suporte apenas a [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) método. Quando você usa o **mover** métodos para visitar cada registro (ou enumerar o **registros**), você pode usar o **BOF** e **EOF** propriedades para determinar se você tiver movido para fora o início ou término do **registros**.  
  
 Antes de usar qualquer funcionalidade de um **registros** do objeto, você deve chamar o **suporta** método no objeto para verificar se a funcionalidade está disponível ou com suporte. Você não deve usar a funcionalidade quando o **suporta** método retornará false. Por exemplo, você pode usar o **MovePrevious** somente se do método `Recordset.Supports(adMovePrevious)` retorna **True**. Caso contrário, você obterá um erro, porque o **registros** objeto fechado e a funcionalidade fique indisponível na instância. Se não há suporte para um recurso que lhe interessam, **suporta** retornará false também. Nesse caso, você deve evitar chamando o método ou propriedade correspondente no **registros** objeto.  
  
 **Conjunto de registros** objetos podem dar suporte a dois tipos de atualização: imediatas e em lotes. Em atualização imediata, todas as alterações de dados são gravadas imediatamente para a fonte de dados depois de você chamar o [atualização](../../../ado/reference/ado-api/update-method.md) método. Você também pode passar matrizes de valores como parâmetros com o [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) e **atualizar** métodos e atualizar simultaneamente vários campos em um registro.  
  
 Se um provedor oferece suporte a atualização em lotes, você pode ter o provedor de alterações em mais de um registro de cache e, em seguida, transmiti-los em uma única chamada para o banco de dados com o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Isso se aplica a alterações feitas com o **AddNew**, **atualização**, e [excluir](../../../ado/reference/ado-api/delete-method-ado-recordset.md) métodos. Depois de chamar o **UpdateBatch** método, você pode usar o [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade para verificar se há conflitos de dados para resolvê-los.  
  
> [!NOTE]
>  Para executar uma consulta sem usar um [comando](../../../ado/reference/ado-api/command-object-ado.md) de objeto, passe uma cadeia de caracteres de consulta para o **abrir** método de um **registros** objeto. No entanto, um **comando** objeto é necessário quando você deseja manter o texto de comando e execute novamente ou use parâmetros de consulta.  
  
 O [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade controla as permissões de acesso.  
  
 O **campos** coleção é o membro padrão da **registros** objeto. Como resultado, as duas instruções de código a seguir são equivalentes.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 Quando um **Recordset** objeto é transmitido entre processos, somente o **linhas** valores são o marshaling e as propriedades do **Recordset** objeto são ignorados. Durante Desempacotando, o **linhas** seja descompactado em criado recentemente **registros** objeto, que também define suas propriedades para os valores padrão.  
  
 O **registros** objeto é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Eventos, métodos e propriedades do objeto de conjunto de registros](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Coleção de campos (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
