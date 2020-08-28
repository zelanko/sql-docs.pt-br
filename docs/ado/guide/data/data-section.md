---
description: Seção de dados
title: Seção de dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
author: rothja
ms.author: jroth
ms.openlocfilehash: ac4febc789aca18401380ee8ada7b2ab7f9d30a3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991447"
---
# <a name="data-section"></a>Seção de dados
A seção de dados define os dados do conjunto de linhas junto com quaisquer atualizações, inserções ou exclusões pendentes. A seção de dados pode conter zero ou mais linhas. Ele só pode conter dados de um conjunto de linhas em que a linha é definida pelo esquema. Além disso, conforme observado anteriormente, as colunas sem dados podem ser omitidas. Se um atributo ou subelemento for usado na seção de dados e essa construção não tiver sido definida na seção de esquema, ela será silenciosamente ignorada.  
  
## <a name="string"></a>Cadeia de caracteres  
 Caracteres XML reservados em dados de texto devem ser substituídos por entidades de caracteres apropriadas. Por exemplo, no nome da empresa "João ' s garagem", a aspa simples deve ser substituída por uma entidade. A linha real seria semelhante ao seguinte:  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 Os seguintes caracteres são reservados em XML e devem ser substituídos por entidades de caracteres: {', ", &, \<,> }.  
  
## <a name="binary"></a>Binário  
 Os dados binários são de bin. Hex codificados (ou seja, um byte é mapeado para dois caracteres, um caractere por Nibble).  
  
## <a name="datetime"></a>Datetime  
 O formato da variante VT_DATE não é compatível diretamente com os tipos de dados XML-Data. O formato correto para datas com um componente de dados e hora é aaaa-mm-ddThh: mm: SS.  
  
 Para obter mais informações sobre formatos de data especificados pelo XML, consulte a [especificação de dados XML do W3C](https://go.microsoft.com/fwlink/?LinkId=5692).  
  
 Quando a especificação de dados XML define dois tipos de dados equivalentes (por exemplo, i4 = = int), o ADO gravará o nome amigável, mas será lido em ambos.  
  
## <a name="managing-pending-changes"></a>Gerenciando alterações pendentes  
 Um conjunto de registros pode ser aberto no modo de atualização imediata ou em lote. Quando eles são abertos no modo de atualização do lote com cursores do lado do cliente, todas as alterações feitas no conjunto de registros estão em um estado pendente até que o método UpdateBatch seja chamado. As alterações pendentes também são persistidas quando o conjunto de registros é salvo. Em XML, eles são representados pelo uso dos elementos "Update" definidos em urn: schemas-microsoft-com: Rowset. Além disso, se um conjunto de linhas puder ser atualizado, a propriedade Updatable deverá ser definida como true na definição da linha. Por exemplo, para definir que a tabela transportadoras contenha alterações pendentes, a definição de linha seria parecida com a seguinte.  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 Isso informa o provedor de persistência para dados de superfície para que o ADO possa construir um objeto Recordset atualizável.  
  
 Os dados de exemplo a seguir mostram como inserções, alterações e exclusões examinam o arquivo persistente.  
  
```  
<rs:data>  
  <z:row ShipperID="2" CompanyName="United Package"   
    Phone="(503) 555-3199"/>  
<rs:update>  
  <rs:original>  
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>  
  </rs:original>  
  <z:row Phone="(503) 552-7134"/>  
</rs:update>  
<rs:insert>  
  <z:row ShipperID="12" CompanyName="Lightning Shipping"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="13" CompanyName="Thunder Overnight"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="14" CompanyName="Blue Angel Air Delivery"   
    Phone="(505) 111-2222"/>  
</rs:insert>  
<rs:delete>  
  <z:row ShipperID="1" CompanyName="Speedy Express" Phone="(503) 555-9831"/>  
</rs:delete>  
</rs:data>  
```  
  
 Uma atualização sempre contém os dados de linha originais completos seguidos pelos dados de linha alterados. A linha alterada pode conter todas as colunas ou apenas as colunas que realmente foram alteradas. No exemplo anterior, a linha do transportadora 2 não é alterada e somente a coluna telefone tem valores alterados para o transportador 3 e, portanto, é a única coluna incluída na linha alterada. As linhas inseridas para as transportadoras 12, 13 e 14 são agrupadas em uma marca RS: INSERT. Observe que as linhas excluídas também podem ser agrupadas em lote, embora isso não seja mostrado no exemplo anterior.  
  
## <a name="see-also"></a>Consulte Também  
 [Persistência de registros em formato XML](./persisting-records-in-xml-format.md)