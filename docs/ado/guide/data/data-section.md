---
title: Seção de dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6a06b2291d07378b63907b4a195fa3902930078
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207765"
---
# <a name="data-section"></a>Seção de dados
A seção de dados define os dados do conjunto de linhas, juntamente com qualquer pendente atualizações, inserções ou exclusões. A seção de dados pode conter zero ou mais linhas. Ele pode conter apenas dados de um conjunto de linhas em que a linha é definida pelo esquema. Além disso, conforme observado anteriormente, as colunas, sem nenhum dado podem ser omitidas. Se um atributo ou o subelemento for usado na seção de dados e essa construção não foi definida na seção de esquema, ele será ignorado silenciosamente.  
  
## <a name="string"></a>Cadeia de caracteres  
 Os caracteres XML reservados nos dados de texto devem ser substituídos com entidades de caractere apropriado. Por exemplo, o nome da empresa "Garagem de José", a aspa simples deve ser substituída por uma entidade. A linha real seria semelhante ao seguinte:  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 Os seguintes caracteres são reservados no XML e deve ser substituídos por entidades de caractere: {",", &,\<, >}.  
  
## <a name="binary"></a>Binary  
 Dados binários são codificados hex (ou seja, os mapas de um byte em dois caracteres, um caractere por nibble).  
  
## <a name="datetime"></a>DateTime  
 O formato VT_DATE variant não é diretamente suportado pelos tipos de dados XML-Data. O formato correto para datas com o componente de uma data e a hora é aaaa-mm-ddTHH.  
  
 Para obter mais informações sobre formatos de data especificada por XML, consulte a [especificação W3C XML-Data](https://go.microsoft.com/fwlink/?LinkId=5692).  
  
 Quando a especificação de XML-Data define dois tipos de dados equivalente (por exemplo, i4 = = int), ADO será escrever o nome amigável, mas lidos em ambos.  
  
## <a name="managing-pending-changes"></a>Gerenciamento de alterações pendentes  
 Um conjunto de registros pode ser aberto no imediata ou modo de atualização em lotes. Quando eles são abertos no modo de atualização em lotes com cursores do lado do cliente, são todas as alterações feitas ao conjunto de registros em um estado pendente até que o método UpdateBatch seja chamado. As alterações pendentes também são persistidos quando o conjunto de registros é salvo. Em XML, eles são representados pelo uso de "atualização" elementos definidos no urn: schemas-microsoft-com:rowset. Além disso, se um conjunto de linhas pode ser atualizado, a propriedade atualizável deve ser definida como true na definição de linha. Por exemplo, para definir que a tabela Shippers (transportadores) contém as alterações pendentes, seria a definição de linha aparência semelhante seguinte.  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 Isso informa ao provedor de persistência para dados de superfície para que o ADO pode construir um objeto Recordset atualizável.  
  
 Os dados de exemplo a seguir mostram como inserções, as alterações e exclusões de examinar o arquivo persistente.  
  
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
  
 Uma atualização sempre contém os dados da linha original inteiro seguidos dos dados de linha alterada. A linha alterada pode conter todas as colunas ou apenas as colunas que realmente foram alterados. No exemplo anterior, a linha para a transportadora 2 não é alterada, e somente a coluna telefone alterou os valores para a transportadora 3 e, portanto, a única coluna incluída na linha alterada. As linhas inseridas para Shippers (transportadores), 12, 13 e 14 são em lote juntos marca do rs: inserir em uma. Observe que linhas excluídas podem também ser agrupadas, embora isso não é mostrado no exemplo anterior.  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
