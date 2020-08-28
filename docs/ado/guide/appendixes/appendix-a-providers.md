---
description: 'Apêndice A: provedores de dados e serviços'
title: 'Apêndice A: provedores | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
author: rothja
ms.author: jroth
ms.openlocfilehash: d50f77959b21031b03ae9591181c61a3419577fd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991167"
---
# <a name="appendix-a-data-and-service-providers"></a>Apêndice A: provedores de dados e serviços
Esta seção aborda três tipos de provedores: provedores de dados, provedores de serviços e componentes de serviço. Os provedores se enquadram em duas categorias: aquelas que fornecem dados e aqueles que fornecem serviços. Um *provedor de dados* possui seus próprios dados e os expõe em formato de tabela para seu aplicativo. Um *provedor de serviços* encapsula um serviço, produzindo e consumindo dados, aumentando os recursos em seus aplicativos ADO. Um provedor de serviços também pode ser definido como um *componente de serviço*, que deve funcionar em conjunto com outros provedores de serviços ou componentes.

## <a name="data-providers"></a>Provedores de Dados
 O ADO é poderoso e flexível, pois pode se conectar a qualquer um dos vários provedores de dados diferentes e ainda expor o mesmo modelo de programação, independentemente dos recursos específicos de qualquer provedor específico.

 No entanto, como cada provedor de dados é exclusivo, como seu aplicativo interage com o ADO variará um pouco pelo provedor de dados. As diferenças geralmente se enquadram em uma das três categorias:

-   Parâmetros de conexão na propriedade [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) .

-   Uso do objeto [Command](../../reference/ado-api/command-object-ado.md) .

-   Comportamento do [conjunto de registros](../../reference/ado-api/recordset-object-ado.md) específico do provedor.

 Os detalhes de cada um dos provedores de dados disponíveis atualmente na Microsoft são listados da seguinte maneira.

|Área|Tópico|
|----------|-----------|
|Bancos de dados ODBC|[Microsoft OLE DB Provider para ODBC](./microsoft-ole-db-provider-for-odbc.md)|
|Serviço de indexação da Microsoft|[Microsoft OLE DB Provider for Microsoft Indexing Service](./microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Serviço do Active Directory|[Provedor do Microsoft OLE DB para Microsoft Active Directory Service](./microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Bancos de dados do Microsoft Jet|[Provedor de OLE DB para Microsoft Jet](./microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Provedor Microsoft OLE DB para SQL Server](./microsoft-ole-db-provider-for-sql-server.md)|
|Bancos de dados Oracle|[Microsoft OLE DB Provider for Oracle](./microsoft-ole-db-provider-for-oracle.md)|
|Publicação na Internet|[Microsoft OLE DB Provider para publicação na Internet](./microsoft-ole-db-provider-for-internet-publishing.md)|
|Fontes de dados simples|[Provedor simples do Microsoft OLE DB](./microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>Propriedades dinâmicas específicas do provedor
 As coleções de [Propriedades](../../reference/ado-api/properties-collection-ado.md) dos objetos [Connection](../../reference/ado-api/connection-object-ado.md), [Command](../../reference/ado-api/command-object-ado.md)e [Recordset](../../reference/ado-api/recordset-object-ado.md) incluem propriedades dinâmicas específicas ao provedor. Essas propriedades fornecem informações sobre a funcionalidade específica para o provedor além das propriedades internas às quais o ADO dá suporte.

 Depois de estabelecer a conexão e criar esses objetos, use o método [Refresh](../../reference/ado-api/refresh-method-ado.md) na coleção **Properties** do objeto para obter as propriedades específicas do provedor. Consulte a documentação do provedor e o [Guia do programador de OLE DB](/previous-versions/windows/desktop/ms713643(v=vs.85)) para obter informações detalhadas sobre essas propriedades dinâmicas.

## <a name="service-providers"></a>Provedores de serviço
 Para usar um provedor de serviços, você deve fornecer uma palavra-chave. Você também deve estar ciente das propriedades dinâmicas específicas do provedor associadas a cada provedor de serviços. Os detalhes específicos do provedor são listados para cada provedor de serviços que está disponível atualmente na Microsoft:

-   [Microsoft Data Shaping Service para OLE DB](./microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Provedor de persistência do Microsoft OLE DB](./microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Provedor de comunicação remota do Microsoft OLE DB](./microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>Componentes do Serviço
 O [serviço de cursor para OLE DB](./microsoft-cursor-service-for-ole-db-ado-service-component.md) componente de serviço complementa as funções de suporte de cursor dos provedores de dados. Ele também requer uma palavra-chave e tem propriedades dinâmicas.

 Para obter mais informações sobre provedores de OLE DB, consulte [Microsoft OLE DB](/previous-versions/windows/desktop/ms722784(v=vs.85)).

## <a name="provider-commands"></a>Comandos do provedor
 Para cada provedor listado aqui, se seus aplicativos permitirem que os usuários insiram instruções SQL como os comandos do provedor, você deverá sempre validar a entrada do usuário e estar atento a possíveis ataques de hacker usando instruções SQL potencialmente perigosas, como, por exemplo `DROP TABLE t1` , como parte da entrada do usuário.

## <a name="see-also"></a>Consulte Também
 ADO ( [objeto de comando](../../reference/ado-api/command-object-ado.md) ) [objeto de conexão](../../reference/ado-api/connection-object-ado.md) do [Microsoft OLE DB Provider para a publicação na Internet provedor](./microsoft-ole-db-provider-for-internet-publishing.md) [microsoft OLE DB para Microsoft Active Directory Service](./microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [microsoft OLE DB Provider para microsoft Indexing](./microsoft-ole-db-provider-for-microsoft-indexing-service.md) provedor [Microsoft OLE DB Provider for ODBC](./microsoft-ole-db-provider-for-odbc.md) [provedor Microsoft OLE DB para Oracle](./microsoft-ole-db-provider-for-oracle.md) [provedor de OLE DB da](./microsoft-ole-db-provider-for-sql-server.md) Microsoft para SQL Server Microsoft OLE DB Provider para [Microsoft Jet](./microsoft-ole-db-provider-for-microsoft-jet.md) [Properties Collection (ADO)](../../reference/ado-api/properties-collection-ado.md) Recordset (ADO) conjunto de [registros Object](../../reference/ado-api/recordset-object-ado.md) ( [RDS](../../reference/rds-api/refresh-method-rds.md) )