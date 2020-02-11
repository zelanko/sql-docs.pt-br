---
title: Usando ADO para publicação na Internet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: decbc7c3b377234d91fe6b3e662d9449298041c1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923612"
---
# <a name="using-ado-for-internet-publishing"></a>Usar o ADO para publicação na Internet
[O provedor de OLE DB para publicação na Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) mostra um exemplo específico de acesso a dados heterogêneos com o ADO. Embora os exemplos nesta seção sejam específicos ao uso do provedor de publicação na Internet, os princípios demonstrados devem ser semelhantes ao usar o ADO com outros provedores para dados heterogêneos, como um provedor para um armazenamento de email.  
  
## <a name="urls"></a>URLs  
 Os localizadores de recursos uniformes (URLs) podem ser usados como uma alternativa para cadeias de conexão e texto de comando para especificar fontes de dados e o local dos arquivos e diretórios. Você pode usar URLs com os objetos [Connection](../../../ado/reference/ado-api/connection-object-ado.md) e **Recordset** existentes e com os objetos **Record** e **Stream** .  
  
 Para obter mais informações sobre como usar URLs, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="record-fields"></a>Campos de registro  
 A diferença de distinção entre dados heterogêneos e dados homogêneos é que, para o primeiro, cada linha de dados, ou **registro**, pode ter um conjunto diferente de colunas ou **campos**. Para dados homogêneos, cada linha tem o mesmo conjunto de colunas. Para obter mais informações sobre os campos específicos do provedor de publicação da Internet, consulte [registros e campos extras fornecidos pelo provedor](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
### <a name="appending-new-fields"></a>Acrescentando novos campos  
 Vários objetos ADO foram aprimorados para trabalhar juntos com objetos **Record** e **Stream** .  
  
-   O método [Append](../../../ado/reference/ado-api/append-method-ado.md) da coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) , que cria e adiciona um objeto [Field](../../../ado/reference/ado-api/field-object.md) à coleção, também pode especificar o valor do **campo**.  
  
-   O método [Update](../../../ado/reference/ado-api/update-method.md) finaliza a adição ou exclusão de campos na coleção.  
  
-   Como um atalho e uma alternativa para o método **Append** , você pode criar campos atribuindo um valor a um campo indefinido ou excluído anteriormente.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [O Provedor OLE DB para publicação na Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [Registros e campos fornecidos pelo provedor](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [Histórico ADO](../../../ado/guide/ado-history.md)
