---
title: "Seção de dados | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fae3df37c9a83bdf97a7ae2a53bc76777b318546
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="data-section"></a>Seção de dados
A seção de dados define os dados do conjunto de linhas juntamente com quaisquer atualizações, inserções ou exclusões pendentes. A seção de dados pode conter zero ou mais linhas. Ele só pode conter dados de um conjunto de linhas em que a linha é definida pelo esquema. Além disso, conforme observado anteriormente, colunas sem dados podem ser omitidas. Se um atributo ou subelemento é usado na seção de dados e essa construção não foi definida na seção de esquema, ele será ignorado silenciosamente.  
  
## <a name="string"></a>Cadeia de caracteres  
 Os caracteres XML reservados nos dados de texto devem ser substituídos por entidades de caracteres apropriada. Por exemplo, o nome da empresa "De Joe garagem", a aspa simples deve ser substituída por uma entidade. A linha real seria semelhante à seguinte:  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 Os seguintes caracteres são reservados em XML e devem ser substituídos por entidades de caractere: {', ", &,\<, >}.  
  
## <a name="binary"></a>Binary  
 Dados binários são codificados bin.hex (ou seja, um byte é mapeado para dois caracteres, um caractere por nibble).  
  
## <a name="datetime"></a>DateTime  
 O formato VT_DATE variant não é diretamente suportado por tipos de dados XML-Data. O formato correto para datas com o componente de uma data e a hora é aaaa-mm-ddTHH.  
  
 Para obter mais informações sobre os formatos de data especificada por XML, consulte o [especificação W3C XML-Data](https://go.microsoft.com/fwlink/?LinkId=5692).  
  
 Quando a especificação de dados XML define dois tipos de dados equivalentes (por exemplo, i4 = = int), ADO será gravar o nome amigável mas lida em ambos.  
  
## <a name="managing-pending-changes"></a>Gerenciar alterações pendentes  
 Um conjunto de registros pode ser aberto no imediata ou modo de atualização em lotes. Quando eles são abertos no modo de atualização em lotes com cursores do lado do cliente, todas as alterações feitas ao conjunto de registros estão em um estado pendente até que o método UpdateBatch seja chamado. As alterações pendentes também são persistidos quando o conjunto de registros é salvo. Em XML, eles são representados pelo uso dos elementos "atualização" definido em urn: schemas-microsoft-com:rowset. Além disso, se um conjunto de linhas pode ser atualizado, a propriedade atualizável deve ser definida como true na definição da linha. Por exemplo, para definir que a tabela Transportadoras contém alterações pendentes, a definição de linha será aparência semelhante seguinte.  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 Isso informa ao provedor de persistência para dados de superfície para que o ADO pode construir um objeto Recordset atualizável.  
  
 Os dados de exemplo a seguir mostram como inserções, alterações e exclusões de examinar o arquivo persistente.  
  
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
  
 Uma atualização sempre contém os dados da linha original inteiro seguidos dos dados de linha alterada. A linha alterada pode conter todas as colunas ou apenas as colunas que realmente foram alterados. No exemplo anterior, a linha da transportadora 2 não é alterada, e somente a coluna de telefone foi alterado valores para 3 da transportadora e, portanto, é a única coluna incluída na linha alterada. As linhas inseridas para transportadoras 12, 13 e 14 são em lote juntos marca de rs: inserir em uma. Observe que as linhas excluídas podem também ser agrupadas, embora isso não é mostrado no exemplo anterior.  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
