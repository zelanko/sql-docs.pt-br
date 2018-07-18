---
title: Classes gerenciadas SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- .NET Framework [SQLXML], Managed Classes
- SQL Server .NET Data Provider
- Managed Classes [SQLXML], about managed classes
- providers [SQLXML], SQL Server .NET Data Provider
- data providers [SQLXML], SQL Server .NET Data Provider
- Managed Classes [SQLXML]
- XML [SQLXML]
- SQLXML Managed Classes
- providers [SQLXML], SQLXML Managed Classes
- data providers [SQLXML], SQLXML Managed Classes
- SQLXML, Managed Classes
ms.assetid: 73a5faeb-dabf-4895-acb5-a9651b646065
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 13212c73e4f12ed83e6677a8c819b3306eab3118
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38046154"
---
# <a name="sqlxml-40-net-framework-support---managed-classes"></a>Suporte a SQLXML 4.0 do .NET Framework – Classes gerenciadas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 suporta recursos que permitem escrever aplicativos para acessar dados XML de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], importar esses dados para o ambiente do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework, processá-los e enviar as atualizações de volta ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 
  
  As classes gerenciadas [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML expõem a funcionalidade do SQLXML 4.0 dentro do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Com as classes gerenciadas SQLXML, você pode escrever um aplicativo C# para acessar dados XML de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], trazer os dados para o ambiente .NET Framework, processar os dados e enviar as atualizações de volta para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como um DiffGram para aplicar as atualizações. Use um esquema de mapeamento ao aplicar atualizações a um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando classes gerenciadas SQLXML. Para obter um exemplo funcional, consulte [acessando a funcionalidade SQLXML no ambiente .NET](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 Para usar as classes gerenciadas SQLXML com o SQLXML 4.0, é necessário instalar o Microsoft Visual Studio.  
  
> [!NOTE]  
>  O .NET Framework inclui o .NET Data Provider do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esse provedor pode ser usado para acessar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no ambiente .NET; contudo, ele pode tratar somente consultas SQL tradicionais (ou seja, consultas de bancos de dados relacionais com a exceção de consultas XML FOR XML). Não é possível executar modelos XML ou consultas XPath do servidor no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

 Para obter informações sobre como acessar e modificar dados em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dentro de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework e sobre como usar DiffGrams para atualizar dados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabelas, consulte [acessando a funcionalidade SQLXML no ambiente .NET](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
> [!NOTE]  
>  Você também pode gravar aplicativos do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio para o carregamento em massa de documentos XML usando o recurso XML Bulk Load. Para obter mais informações, consulte [execução de carregar dados em massa de XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md). Você deve adicionar uma referência à DLL do XML Bulk Load (Xblkld4.dll) ao seu aplicativo. Esta é uma DLL COM para a qual o Visual Studio .NET cria automaticamente a biblioteca wrapper.  
  
  Esta seção fornece aplicativos de exemplo que demonstram como usar o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Classes gerenciadas SQLXML:  
 [Executando consultas SQL &#40;Classes gerenciadas SQLXML&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-sqlxml-managed-classes.md)  
  [Executando consultas SQL usando o método ExecuteXMLReader](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-sql-queries-by-using-the-executexmlreader-method.md)  
  [Processando XML no lado do cliente &#40;Classes gerenciadas SQLXML&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/processing-xml-on-the-client-side-sqlxml-managed-classes.md)  
  [Executando consultas XPath &#40;Classes gerenciadas SQLXML&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-sqlxml-managed-classes.md)  
  [Executando consultas XPath com Namespaces &#40;Classes gerenciadas SQLXML&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md)  
  [Executando os arquivos de modelo usando a propriedade CommandText](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandtext-property.md)  
  [Executando os arquivos de modelo usando a propriedade CommandStream](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/executing-template-files-by-using-the-commandstream-property.md)  
  [Aplicando uma transformação XSL &#40;Classes gerenciadas SQLXML&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/applying-an-xsl-transformation-sqlxml-managed-classes.md)  
  

  
  
