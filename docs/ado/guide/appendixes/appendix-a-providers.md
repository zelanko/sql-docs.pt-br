---
title: 'Apêndice a: provedores | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5110c06913325421aeeaa2d31295d7e2bc6bf59c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47645594"
---
# <a name="appendix-a-data-and-service-providers"></a>Apêndice a: dados e provedores de serviço
Esta seção aborda os três tipos de provedores: provedores de dados, provedores de serviços e componentes de serviço. Provedores se enquadram em duas categorias: àqueles que fornecem dados e aqueles fornecendo serviços. Um *provedor de dados* possui seus próprios dados e o expõe em formato de tabela para seu aplicativo. Um *provedor de serviços* encapsula um serviço, produzindo e consumindo dados, aumentando os recursos em seus aplicativos do ADO. Um provedor de serviços também pode ser ainda mais definido como um *componente de serviço*, que devem trabalhar junto com outros provedores de serviços ou componentes.

## <a name="data-providers"></a>Provedores de Dados
 ADO é poderoso e flexível, porque ele pode se conectar a qualquer um dos vários provedores de dados diferentes e ainda expor o mesmo modelo de programação, independentemente dos recursos específicos de qualquer provedor determinado.

 No entanto, como cada provedor de dados é exclusivo, como seu aplicativo interage com o ADO varia ligeiramente por provedor de dados. As diferenças geralmente se encaixam em uma das três categorias:

-   Parâmetros de Conexão na [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade.

-   [Comando](../../../ado/reference/ado-api/command-object-ado.md) uso do objeto.

-   Específico do provedor [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) comportamento.

 Detalhes de cada um dos provedores de dados disponíveis no momento da Microsoft estão listadas a seguir.

|Área|Tópico|
|----------|-----------|
|Bancos de dados ODBC|[Provedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Serviço de indexação da Microsoft|[Provedor Microsoft OLE DB para Microsoft Indexing Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Serviço do Active Directory|[Provedor Microsoft OLE DB para o serviço de diretório Microsoft Active Directory](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Bancos de dados Microsoft Jet|[Provedor OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Provedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|Bancos de dados Oracle|[Provedor Microsoft OLE DB para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|Publicação na Internet|[Provedor Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|Fontes de dados simples|[Microsoft OLE DB Provider simples](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>Propriedades dinâmicas específicas do provedor
 O [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleções da [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [comando](../../../ado/reference/ado-api/command-object-ado.md), e [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos incluem propriedades dinâmicas específicas para o provedor. Essas propriedades fornecem informações sobre a funcionalidade específica ao provedor além das propriedades internas que dá suporte à ADO.

 Depois de estabelecer a conexão e criar esses objetos, use o [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) método na **propriedades** coleção do objeto para obter as propriedades específicas do provedor. Consulte a documentação do provedor e o [guia do programador do DB OLE](http://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) para obter informações detalhadas sobre essas propriedades dinâmicas.

## <a name="service-providers"></a>Provedores de serviço
 Para usar um provedor de serviços, você deve fornecer uma palavra-chave. Você também deve estar ciente das propriedades dinâmicas específicas do provedor associadas com cada provedor de serviços. Detalhes específicos do provedor são listados para cada provedor de serviço que está disponível no momento da Microsoft:

-   [Microsoft Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Provedor de persistência do Microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Provedor de comunicação remota do Microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>Componentes de serviço
 O [Cursor Service para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) complementa o componente de serviço de funções de suporte de cursor de provedores de dados. Ele também requer uma palavra-chave e tem as propriedades dinâmicas.

 Para obter mais informações sobre provedores do OLE DB, consulte [do Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx).

## <a name="provider-commands"></a>Comandos de provedor
 Para cada provedor listado aqui, se seus aplicativos permitem aos usuários inserir instruções SQL que os comandos de provedor, você deve sempre validar a entrada do usuário e esteja atenta aos possíveis de ataques de hackers usando instruções SQL potencialmente perigosas, como `DROP TABLE t1`, como parte da entrada do usuário.

## <a name="see-also"></a>Consulte também
 [Comando (ADO) do objeto](../../../ado/reference/ado-api/command-object-ado.md) [o objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [provedor Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [provedor Microsoft OLE DB para o serviço de diretório Microsoft Active Directory ](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Microsoft OLE DB Provider para Microsoft Indexing Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [Microsoft OLE DB Provider for ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [Provedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [provedor Microsoft OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [ O objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
